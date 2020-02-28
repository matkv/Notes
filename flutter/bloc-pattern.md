# Flutter BLoC Pattern

## **B**usiness **Lo**gic **C**omponent

The main idea is to separate the state from the UI.

A bloc (business logic component) is basically a box where **events** go in and a **state** comes out.

The bloc operates on these states to figure out which state it should output.

As an example we have the default Flutter app which increments a counter. We add another button that decrements that counter.

### Events

We create a new abstract class ```CounterEvent``` and two classes that inherit from it:

```dart
abstract class CounterEvent {}

class IncrementEvent extends CounterEvent {}

class DecrementEvent extends CounterEvent {}
```

We also create a file for our bloc. We need to import ```dart:async``` and our new ```CounterEvent``` class.

```dart
import 'dart:async';
import 'package:bloc_practice/counter_event.dart';

class CounterBloc{
  int _counter = 0;
}
```

Next, we create a ```StreamController```. It is basically a "box" that has an input & an output.

The input is the ```StreamSink``` and the output is the ```Stream```.

Whenever there is some input to the sink, it is automatically going to be outputted through the stream.

```dart
final _counterStateController = StreamController<int>();

  StreamSink<int> get _inCounter => _counterStateController.sink;

  Stream<int> get counter => _counterStateController.stream;
```

Only the stream, the output, is made public.

Now our widgets in the app can already listen to the value of the counter through the stream, but in order for out UI to be able to input the events for incrementing or decrementing the counter, we need an additional ```StreamController```.

```dart
//this exposes only a sink which is an input
  final _counterEventController = StreamController<CounterEvent>();
  Sink<CounterEvent> get counterEventSink => _counterEventController.sink;
```

Inside the constructor of the ```CounterBloc()```, we can listen to the output of the counter event stream:

```dart
CounterBloc(){

    //whenever there is a new event, we map it to a new state
    _counterEventController.stream.listen(_mapEventToState);j
  }

  void _mapEventToState(CounterEvent event){
    if (event is IncrementEvent) {
      _counter++;
    } else {
      _counter--;

      _inCounter.add(_counter); //we add the new counter value to the sink
    }
  }
```

By adding the new counter value to the sink of the counter state controller - it will be outputted through the stream.

Now our UI can basically communicate with the ```CounterBloc``` in two ways. The ```counter``` stream outputs data, the ```counterEventSink``` inputs events.

We also add a dispose function:

```dart
void dispose(){
    _counterStateController.close();
    _counterEventController.close();
  }
```

Now we just need to implement this bloc in our UI. 

We can delete the functions that increment and decrement the counter.

We create a new bloc:

```dart
final _bloc = CounterBloc();
```

We wrap our UI with a ```StreamBuilder``` which takes the _bloc.counter stream.

```dart
body: Center(
        child: StreamBuilder(
          stream: _bloc.counter,
          initialData: 0,
          builder: (BuildContext context, AsyncSnapshot<int> snapshot) {
            return Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Text(
                  'You have pushed the button this many times:',
                ),
                Text(
                  '${snapshot.data}',
                  style: Theme.of(context).textTheme.headline4,
                ),
              ],
            );
          },
        ),
      ),
```

We can read the data from the bloc using the snapshot.

The last thing we need to do is to pass the events into our bloc using the ```onPressed:``` events of the two buttons.

```dart
onPressed: () => _bloc.counterEventSink.add(IncrementEvent()),
```

We do the same thing for the decrement button.

At last, we override the dispose function to also dispose our _bloc streams:

```dart
@override
  void dispose() {    
    super.dispose();
    _bloc.dispose();
  }
```

In order to use the bloc pattern, we don't need to do all of this manually every time, we can use the bloc library.

## Bloc Library

[Youtube Tutorial](https://www.youtube.com/watch?v=nQMfaQeCL6M)