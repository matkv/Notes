# Summary

* Bloc library
    * Goal - separating presentation from business logic
    * Knowing the state of the application 
    * Recording user interaction
    * Reusing components

* bloc
    * Events: **Input** to a bloc - for example user interaction
    * States: **Output** of a bloc - represent part of our applications state, UI components are notified
    * Transition: **Change from one state to another**. Current state -> Event -> next state
    * Stream: Sequence of asynchronus data, can be "awaited" by an async function
    * Blocs: Business Logic component - converts a stream of **incoming events** into a stream of **outgoing states**. mapEventToState takes an event and returns a stream of new states. A bloc is notified of an event with the "add" method
    * BlocDelegate: makes it possible to implement functionality for **all** blocs at once.
* flutter_bloc
    * BlocBuilder: Flutter widget which requres a **Bloc** and a **builder** function
    * BlocProvider: Flutter widget which provides a bloc to its children. A single instance of a bloc can be provided to multiple widgets.
    * MultiBlocProvider: merges multiple BlocProvider into one.
    * BlocListener: invokes listener in response to state changes - used for functionality that **needs to occur once per state change**