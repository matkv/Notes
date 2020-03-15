# Testing

For this example, we will be using the ```CounterBloc```:

```dart
enum CounterEvent { increment, decrement }

class CounterBloc extends Bloc<CounterEvent, int> {
  @override
  int get initialState => 0;

  @override
  Stream<int> mapEventToState(CounterEvent event) async* {
    switch (event) {
      case CounterEvent.decrement:
        yield state - 1;
        break;
      case CounterEvent.increment:
        yield state + 1;
        break;
    }
  }
}
```

We need to add ```test``` and ```bloc_test``` to our pubspec.yaml:

```dart
dev_dependencies:
  test: ^1.3.0
  bloc_test: ^3.0.0
```

We create a file called ```counter_bloc_test.dart``` and import the packages:

```dart
import 'package:test/test.dart';
import 'package:bloc_test/bloc_test.dart';
```

Groups are used for organizing individual tests as well as for creating a context in which we can share a common ```setUp``` and ```tearDown``` across all of the individual tests:

```dart
void main() {
    group('CounterBloc', () {

    });
}
```

We start by creating an instance of our CounterBloc which will be used across all of our tests:

```dart
group('CounterBloc', () {
    CounterBloc counterBloc;

    setUp(() {
        counterBloc = CounterBloc();
    });
});
```

Now we can start writing out tests, here we test if the ```initialState``` of the CounterBloc is 0:

```dart
group('CounterBloc', () {
    CounterBloc counterBloc;

    setUp(() {
        counterBloc = CounterBloc();
    });

    test('initial state is 0', () {
        expect(counterBloc.initialState, 0);
    });
});
```

We can run the tests with the ```pub run test``` command.

Here are some more tests:

```dart
blocTest(
    'emits [0, 1] when CounterEvent.increment is added',
    build: () => counterBloc,
    act: (bloc) => bloc.add(CounterEvent.increment),
    expect: [0, 1],
);

blocTest(
    'emits [0, -1] when CounterEvent.decrement is added',
    build: () => counterBloc,
    act: (bloc) => bloc.add(CounterEvent.decrement),
    expect: [0, -1],
);
```