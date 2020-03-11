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