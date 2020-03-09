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

Bloc attempts to make state changes predictable by regulating when a state change can occur and enforcing a single way to change state throughout an entire application.

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