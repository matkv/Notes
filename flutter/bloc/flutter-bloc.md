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

### MultiBlocProvider

```MultiBlocProvider``` merges multiple ```BlocProvider``` into one. It eliminates the need to nest multple ```BlocProviders```.

```dart
MultiBlocProvider(
  providers: [
    BlocProvider<BlocA>(
      create: (BuildContext context) => BlocA(),
    ),
    BlocProvider<BlocB>(
      create: (BuildContext context) => BlocB(),
    ),
    BlocProvider<BlocC>(
      create: (BuildContext context) => BlocC(),
    ),
  ],
  child: ChildA(),
)
```

### BlocListener

```BlocListener``` is a Flutter widget which takes a BlocWidgetListener and an optional Bloc and invokes the listener in response to state changes in the bloc.

It should be used for functionality that **needs to occur once per state change**, such as navigation, showing a ```SnackBar``` or a dialog.

```listener``` is only called once for each state change and is a void function. If the ```bloc``` parameter is omitted, BlocListener will automatically perform a lookup using BlocProvider and the current BuildContext.

```dart
BlocListener<BlocA, BlocAState>(
  listener: (context, state) {
    // do stuff here based on BlocA's state
  },
  child: Container(),
)
```

If we wish to provide a bloc that is otherwise not accessible via BlocProvider:

```dart
BlocListener<BlocA, BlocAState>(
  bloc: blocA,
  listener: (context, state) {
    // do stuff here based on BlocA's state
  }
)
```

And we can also only call the listener function based on a condition:

```dart
BlocListener<BlocA, BlocAState>(
  condition: (previousState, state) {
    // return true/false to determine whether or not
    // to call listener with state
  },
  listener: (context, state) {
    // do stuff here based on BlocA's state
  }
  child: Container(),
)
```

### MultiBlocListener

```MultiBlocListener``` merges multiple BlocListener widgets into one:

```dart
MultiBlocListener(
  listeners: [
    BlocListener<BlocA, BlocAState>(
      listener: (context, state) {},
    ),
    BlocListener<BlocB, BlocBState>(
      listener: (context, state) {},
    ),
    BlocListener<BlocC, BlocCState>(
      listener: (context, state) {},
    ),
  ],
  child: ChildA(),
)
```

### BlocConsumer

```BlocConsumer``` is analogous to a nested BlocListener or BlocBuilder but reduces the amount of boilerplate needed.

It should only be used when **it is necessary to both rebuild UI and execute other reactions to state changes in the bloc**.

```dart
BlocConsumer<BlocA, BlocAState>(
  listener: (context, state) {
    // do stuff here based on BlocA's state
  },
  builder: (context, state) {
    // return widget here based on BlocA's state
  }
)
```

For more control over when ```listener``` and ```builder``` are called, there are ```listenWhen``` and ```buildWhen```.

```dart
BlocConsumer<BlocA, BlocAState>(
  listenWhen: (previous, current) {
    // return true/false to determine whether or not
    // to invoke listener with state
  },
  listener: (context, state) {
    // do stuff here based on BlocA's state
  },
  buildWhen: (previous, current) {
    // return true/false to determine whether or not
    // to rebuild the widget with state
  },
  builder: (context, state) {
    // return widget here based on BlocA's state
  }
)
```

### RepositoryProvider

```RepositoryProvider``` is a Flutter widget which provides a repository to its children. A single instance of a repository can be provided to multiple widgets. BlocProvider should be used for blocs, RepositoryProvider should be used for repositories.

```dart
RepositoryProvider(
  builder: (context) => RepositoryA(),
  child: ChildA(),
);

```

From ```ChildA```, we can then retriebe the Repostory instance:

```dart
// with extensions
context.repository<RepositoryA>();

// without extensions
RepositoryProvider.of<RepositoryA>(context)

```

### MultiRepositoryProvider

```MultiRepositoryProvider``` merges multiple RepositoryProvider into one:

```dart
MultiRepositoryProvider(
  providers: [
    RepositoryProvider<RepositoryA>(
      builder: (context) => RepositoryA(),
    ),
    RepositoryProvider<RepositoryB>(
      builder: (context) => RepositoryB(),
    ),
    RepositoryProvider<RepositoryC>(
      builder: (context) => RepositoryC(),
    ),
  ],
  child: ChildA(),
)
```