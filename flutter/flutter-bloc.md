# Flutter Bloc Core Concepts

## Bloc Widgets

### BlocBuilder

```BlocBuilder``` is a Flutter widget which requires a ```Bloc``` and a ```builder``` function.

It handles building the widget in response to new states. It is very similar to ```StreamBuilder```, but has a more simple API to reduce the amount of boilerplate code needed. 

The ```builder``` function will most likely be called many times and should be a **pure function** (return value is always the same for the same arguments, no side effects). 

If the bloc parameter is omitted, ```BlocBuilder``` will automatically do a lookup using ```BlocProvider``` and the current ```BuildContext```.

```dart
BlocBuilder<BlocA, BlocAState>(
  builder: (context, state) {
    // return widget here based on BlocA's state
  }
)
```

We can, however, provide a bloc as a parameter. We should only do this if we wish to provide a bloc that will be scoped to a single widget and isn't accessible via a parent BlocProvider + the current BuildContext.

```dart
BlocBuilder<BlocA, BlocAState>(
  bloc: blocA, // provide the local bloc instance
  builder: (context, state) {
    // return widget here based on BlocA's state
  }
)
```

If we want control over when the builder function is called, we can provide an optional ```condition```. The condition takes the previous bloc state and current bloc state and returns a boolean.

If the condition returns true, builder **will be called** and the widget will rebuild. If it is false, builder **will not be called** and **no rebuild will occur**.

```dart
BlocBuilder<BlocA, BlocAState>(
  condition: (previousState, state) {
    // return true/false to determine whether or not
    // to rebuild the widget with state
  },
  builder: (context, state) {
    // return widget here based on BlocA's state
  }
)
```

### BlocProvider

```BlocProvider``` is a Flutter widget which provides a bloc to its children - via ```BlocProvider.of<T>(context)```.

It is used as a dependency injection (DI) widget so **a single instance of a bloc can be provided to multiple widgets** within a subtree.

In most cases, ```BlocProvider``` should be used to create new blocs which will be made available to the subtree.

```dart
BlocProvider(
  create: (BuildContext context) => BlocA(),
  child: ChildA(),
);
```

Since BlocProvider is responsible for creating the bloc, it will automatically handle closing it.

In some cases, ```BlocProvider``` can be used to provide an **existing bloc** to a new portion of the widget tree. Most commonly, this is used when an existing bloc needs to made available to a new route. In this case, ```BlocProvider``` will **not** automatically close the bloc since it did not create it.

```dart
BlocProvider.value(
  value: BlocProvider.of<BlocA>(context),
  child: ScreenA(),
);
```

So now, from either ```ChildA```, or ```ScreenA``` we can retrieve ```BlocA``` with:

```dart
//with extensions
context.bloc<BlocA>();

//without extensions
BlocProvider.of<BlocA>(context)
```