# Bloc Library

[Official Bloc tutorial/documentation](https://bloclibrary.dev/#/gettingstarted)

Bloc consists of:

* bloc - Core bloc library
* flutter_bloc - Flutter widgets built to work with bloc

## Why Bloc?

Bloc makes it easy to separate presentation from business logic. 

It makes it possible to:

* know what state our application is in at any point in time
* easily test every case
* record every single user interaction
* work efficiently and reuse components

Bloc attempts to make state changes predictable by **regulating when a state change can occur** and **enforcing a single way to change state** throughout an entire application.

## Installation

We need to add the bloc pacakge and the flutter_bloc package to our ```pubspec.yaml``` file as a dependency:


```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter
  bloc: ^3.0.0
  flutter_bloc: ^3.2.0
```

After running ```flutter packages get``` we can import them into our ```main.dart``` file.

```dart
import 'package:bloc/bloc.dart';
import 'package:flutter_bloc/flutter_bloc.dart';
```

## Core concepts

### Events

Events are the **input** to a bloc. They are added in response to user interactions (button presses, page loads).

We need to define how users will interact with our app. For example, in a counter app, the user will have two buttons to increment and decrement the counter.

An **event** notifies our application of the increment and decrement so we need to define these events.

```dart
enum CounterEvent { increment, decrement }
```

Here we represent the events using an ```enum```, in more complex cases it might be necessary to use a ```class``` - especially if it's necessary to pass information to the bloc.

### States

States are the **input** to a bloc - they represent part of our applications state. UI components can be **notified** of states and redraw themselves based on the current state.

In the counter example, the state could for example simply be an integer representing the counter's current value.

### Transitions

A transition is the **change from one state to another.** A transition consists of:

* The current state
* The event
* The next state

For example, if a user opened the counter example app and tapped the increment button, we would see the following transition:

```dart
{
  "currentState": 0,
  "event": "CounterEvent.increment",
  "nextState": 1
}
```

Every state change is recorded, so we are able to easly track all user interactions & state changes in one place.

In addition, this makes things like [time travel debugging](https://en.wikipedia.org/wiki/Time_travel_debugging) possible.

### Streams

A stream is a sequence of asynchronous data. One way to think about it is that the stream is a pipe with water flowing through it and the water is the asynchronous data.

Creating a stream by writing an ```async*``` function:

```dart
Stream<int> countStream(int max) async* {
  for (int i = 0; i < max; i++>){
    yield i;
  }
}
```

By marking it as ```async*``` we can use the ```yield``` keyword and return a Stream of data. In that example, we return a Stream of integers.

Every time we ```yield``` in an async function we are **pushing that piece of data through the stream**.

We can receive the data from a stream like this:

```dart
Future<int> sumStream(Stream<int> stream) async {
  int sum = 0;
  await for (int value in stream){
    sum += value;
  }
  return sum;
}
```

By using an ```async``` function we can ```await``` a ```Future``` of integers.

Here is an example of these functions in use:

```dart
void main() async {
    /// Initialize a stream of integers 0-9
    Stream<int> stream = countStream(10);

    /// Compute the sum of the stream of integers
    int sum = await sumStream(stream);
    
    /// Print the sum
    print(sum); // 45
}
```

### Blocs

A **Bloc** - Business Logic Component - is a component which **converts a stream of incoming events** into a **stream of outgoing States**.

Every bloc must extends the base ```Bloc``` class which is part of the core bloc package.

```dart
import 'package:bloc/bloc.dart';

class CounterBloc extends Bloc<CounterEvent, int> {

}
```

We are declaring a bloc which converts ```CounterEvents``` into ```int```s.

**Every bloc must define an initial state which is the state before any events have been received**.

We will set the initial state of the bloc to the value 0.

```dart
@override
int get initialState => 0;
```

#### mapEventToState

Every Bloc must implement a function called ```mapEventToState```. The function takes the incoming ```event``` as an argument and must return a ```Stream``` of new ```states``` which is consumed by the presentation layer.

We can acess the current bloc state at any time using the ```state``` property.

By adding this function, we have a fully functioning ```CounterBloc```.

```dart
import 'package:bloc/bloc.dart';

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

Blocs will ignore duplicate states. If a Bloc yiels ```State nextState``` where ```state == nextState``` - then now transition will occur and no change will be made to the ```Stream<State>```.

#### How to notify a Bloc of an event?

Every bloc has an ```add``` method. ```Add``` takes an event and triggers mapEventToState.

```Add``` may be called **from the presentation layer** or **from within the bloc** and notifies the Bloc of a new ```event```.

Here's a small application which counts from 0 to 3.

```dart
void main() {
    CounterBloc bloc = CounterBloc();

    for (int i = 0; i < 3; i++) {
        bloc.add(CounterEvent.increment);
    }
}
```

The events will be processed in the order in which they were added. Newly added events are enqueued.

An event is considered fully processed **once mapEventToState** has finished executing.

#### Printing Transitions

The ```Transitions``` in this small application would be:

```dart
{
    "currentState": 0,
    "event": "CounterEvent.increment",
    "nextState": 1
}
{
    "currentState": 1,
    "event": "CounterEvent.increment",
    "nextState": 2
}
{
    "currentState": 2,
    "event": "CounterEvent.increment",
    "nextState": 3
}
```

We wouldn't be able to see these transitions unless we override ```onTransition```. This method can be overriden to handle every local bloc transition. ```onTransition``` is called **just before a Bloc's state has been updated**.

```onTransition``` is a **great place to add bloc-specific logging**.

```dart
@override
void onTransition(Transition<CounterEvent, int> transition) {
    print(transition);
}
```

#### Handling errors

We can also handle ```Exceptions``` at the bloc level.

```onError``` is a method that can be overriden to handle every local ```Bloc Exception```. By default **all exceptions will be ignored** and Bloc functionality will be unaffected,

```onError``` is a **great place to add bloc-specific error handling**.

By overriding ```onError``` we can do whatever we'd like whenever an ```Exception``` is thrown.

```dart
@override
void onError(Object error, StackTrace stackTrace) {
  print('$error, $stackTrace');
}
```

### BlocDelegate

In larger applications, it is fairly common to have many Blocs managing different parts of the application's state.

If we want to be able to do something in response to **all** ```Transitions``` we can simply create our own ```BlocDelegate```.

```dart
class SimpleBlocDelegate extends BlocDelegate {
  @override
  void onTransition(Bloc bloc, Transition transition){
    super.onTransition(bloc, transitiion);

    print(transition);
  }
}
```

Here we extend ```BlocDelegate``` and override the ```onTransition``` method. Now we need to tell Bloc to use our ```SimpleBlocDelegate``` - we just need to set the ```BlocSupervisor.delegate``` to our custom delegate.

```dart
void main() {
  BlocSupervisor.delegate = SimpleBlocDelegate();
  CounterBloc bloc = CounterBloc();

  for (int i = 0; i < 3; i++) {
    bloc.add(CounterEvent.increment);
  }
}
```

```BlocSupervisor``` is a singleton which oversees all Blocs and delegates responsibilites to the ```BlocDelegate```.


By overriding the ```onEvent``` method in our ```SimpleBlocDelegate``` we can do something wheneber any event is added, by overriding ```onError``` we can respond to all Exceptions thrown in a Bloc.

```dart
class SimpleBlocDelegate extends BlocDelegate {
  @override
  void onEvent(Bloc bloc, Object event) {
    super.onEvent(bloc, event);
    print(event);
  }

  @override
  void onTransition(Bloc bloc, Transition transition) {
    super.onTransition(bloc, transition);
    print(transition);
  }

  @override
  void onError(Bloc bloc, Object error, StackTrace stacktrace) {
    super.onError(bloc, error, stacktrace);
    print('$error, $stacktrace');
  }
}
```