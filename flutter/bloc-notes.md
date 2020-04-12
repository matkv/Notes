# Bloc

Events -> Bloc -> State

The events & states can be complex classes or something simple like just an integer for the state.

This bloc takes a `CounterEvent` and returns an integer as the state.

```dart
class CounterBloc extends Bloc<CounterEvent, int>
```

The `initialState` value represents the state of the bloc before any interaction with it.

The `mapEventToState` function returns a **stream** of, in this case, integers.

```dart
Stream<int> mapEventToState(CounterEvent event) async* {}
```

In the UI, we can create a new bloc `final counterBloc = CounterBloc();` and then we can add events using the `counterBloc.add(Counterevent.increment)` function.

The bloc is not connected at all to the Flutter framework, all the logic is contained within it. This is means it can for example be reused in multiple projects.

## Async bloc

Let's say we want to get our counter value by making a asynchronous request to some external source.

We need to change how we actually represent the state:

```dart
abstract class CounterState{}

class CounterLoadInProgress extends CounterState{}

class CounterLoadSucess extends CounterState{
    CounterLoadSucess(this.count);

    final int count;
}

class CounterLoadFailure extends CounterState {}
```

Then we change the state of the bloc to this CounterState class. Lets say we have some `_counterService` that is responsible for writing and loading the data to/from the external source.

In the `mapEventToState` function we can use helper functions, for example for the increment event, like this:

```dart
Stream<CounterState> _mapIncrementToState() async* {
    yield CounterLoadInProgress();
    try{
        final asyncCount = await _counterService.increment();
        yield CounterLoadSucess(asyncCount);
    } catch(_) {
        yield CounterLoadFailure();
    }
}
```

## Testing

For testing, we use the `bloc_test` package. We add the `test` and `bloc_test` packages to the `dev_dependencies` in the `pubspec.yaml` file.

Here's what an example test would look like:

```dart
void main(){
    group('CounterBloc', (){
        blocTest(
            'emits [0] when no events are added',
            build: () => CounterBloc(),
            expect: [0],
        );
    });
}
```

`'emits [0] when no events are added',` - this is the description of the test. For `build` we have to return the bloc that will be tested, and for `expect` we set the state that we expect the bloc to have.

We can run the test with `pub run test`.

Here is what the test would look like for the increment event. With the `act` option we can additionally interact with the bloc.

```dart
void main(){
    group('CounterBloc', (){
        blocTest(
            'emits [0, 1] when CounterEvent.increment is added',
            build: () => CounterBloc(),
            act: (counterBloc) => counterBloc.add(CounterEvent.increment),
            expect: [0,1],
        );
    });
}
```

### Async testing

In order to test the async version of the bloc, we use the `mockito` package, which we also need to add to our dev_dependencies. Mockito is useful for mocking services that the test isn't testing.

```dart
class MockCounterService extends Mock implements CounterService {}

...
blocTest(
    'emits [CounterLoadInProgress(), CounterLoadSuccess(1)] when CounterEvent.increment is added',
    build: () {
        final counterService = MockCounterService();
        when(counterService.increment).thenAnswer((_) => Future.value(1));
        return CounterBloc(counterService);
    }
    act: (counterBloc) => counterBloc.add(CounterEvent.increment),
    expect: [CounterLoadInProgress(), CounterLoadSuccess(1)],
        );
```

We create an instance of this mockito class, and then we can say: when we get an increment event, we want the service to return a ```Future``` with the value of 1.

## Flutter bloc

To actually use the bloc pattern within a Flutter app, we need the ```flutter_bloc``` package.

Bloc actually uses ```Provider``` as a dependency. So it's less about a decision between using the bloc library **or** provider, the two can work together nicely. Provider is useful for making our bloc available in the widget tree.

### BlocProvider

The goal is to use a single dependency injection system.

```dart
BlocProvider{
    create: (BuildContext context){
        return MyBloc();
    }
    child: ChildWidget();
}
```

Or:

```dart
...

return MaterialApp(
    home: BlocProvider(
        create: (_) => CounterBloc(),
        child: CounterPage(),
    ),

...
)
```

Inside the child widget we can access the bloc using the ```BlocProvider```:

```dart
//inside the build function of the child widget

final myBloc = BlocProvider.of<MyBloc>(context);
```

By default, ```BlocProvider``` also automatically closes & disposes the provided bloc for us, we don't need to do it manually do it. 

#### MultiBlocProvider

If we want to provide multiple blocs we can use ```MultiBlocProvider```. This is equivalent to nesting them, but easier to read.

```dart
MultiBlocProvider(
    providers: [
        BlocProvider<BlocA>(
            create: (_) => BlocA();
        ),

        BlocProvider<BlocB>(
            create: (_) => BlocB();
        )
    ]
    child: ChildWidget(),
)
```

### BlocBuilder

[Stopped at 20:09](https://www.youtube.com/watch?v=knMvKPKBzGE)