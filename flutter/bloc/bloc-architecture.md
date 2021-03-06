# Bloc Architecture

Bloc allows us to split our application into three layers:

* Data
    * Data Provider
    * Repository
* Business Logic
* Presentation

## Data Layer

Responsible for retrieving/manipulating data from one or more sources.

### Data Provider

The data provider's responsibility is to provide raw data. The data provider should be generic and versatile.

It will usually expose simple APIs to perform CRUD (Create, read, update, delete) operations.

```dart
class DataProvider {
    Future<RawData> readData() async {
        // Read from DB or make network request etc...
    }
}
```

### Repository

The repository layer is a wrapper around one or more data prvoviders with which the Bloc Layer communicates.

```dart
class Repository {
    final DataProviderA dataProviderA;
    final DataProviderB dataProviderB;

    Future<Data> getAllDataThatMeetsRequirements() async {
        final RawDataA dataSetA = await dataProviderA.readData();
        final RawDataB dataSetB = await dataProviderB.readData();

        final Data filteredData = _filterData(dataSetA, dataSetB);
        return filteredData;
    }
}

```

## Bloc (Business Logic) Layer

The bloc layer responds to events from the presentation layer with new states. It can take data from one or more repositories.

It is basically the bridge between the user interface (presentation layer) and the data layer, taking events generated by user input and then communicates with the repository in order to build a new state for the presentation layer to consume.

```dart
class BusinessLogicComponent extends Bloc<MyEvent, MyState> {
    final Repository repository;

    Stream mapEventToState(event) async* {
        if (event is AppStarted) {
            try {
                final data = await repository.getAllDataThatMeetsRequirements();
                yield Success(data);
            } catch (error) {
                yield Failure(error);
            }
        }
    }
}
```

### Bloc-to-Bloc Communication

Every bloc has a state stream which other blocs can subscribe to. That way they can react to changes within the bloc.

Example: ```MyBloc``` has a dependency on ```OtherBloc``` and can ```add``` events in response to state changes in ```OtherBloc```. The ```StreamSubscription``` is closed in the ```close``` override in MyBloc in order to avoid memory leaks.

```dart
class MyBloc extends Bloc {
  final OtherBloc otherBloc;
  StreamSubscription otherBlocSubscription;

  MyBloc(this.otherBloc) {
    otherBlocSubscription = otherBloc.listen((state) {
        // React to state changes here.
        // Add events here to trigger changes in MyBloc.
    });
  }

  @override
  Future<void> close() {
    otherBlocSubscription.cancel();
    return super.close();
  }
}
```

## Presentation layer

The presentation layer figures out how to render itself based on one or more bloc states. In addition, it should handle user input.

Most application flows will start with a ```AppStart``` event which triggers the application to fetch some data to present to the user.

```dart
class PresentationComponent {
    final Bloc bloc;

    PresentationComponent() {
        bloc.add(AppStarted());
    }

    build() {
        // render UI based on bloc state
    }
}
```