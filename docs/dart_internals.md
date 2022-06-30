# Dart Internals

## Dart Execution model

- When any Flutter or Dart application is started the thread(Isolate) is created. 

After the thread is created Dart automatically:
- Initializes two Queues, ***"MicroTask"*** and ***"Event"*** FIFO queues.
- executes the `main()` method and once it is completed
- lunches the **Event Loop**

**MicroTask Queue** - used for very short internal actions that need to run asynchronously, right after something else completes and givin the hand back to Event Queue.

**Event Queue** - used to reference operations that result from the external events (gesture, streams, timers, drawing...) and Futures.

**Futures** - correspond to a task that runs asynchronously and completes some point of time in future.

When you instantiate a new Future:
- and instance of that Future is created and recorded in an internal array, managed by Dart.
- the code that needs to be executed by this Future is directly pushed into the Even Queue
- the future instance is returned with a status(=incomplete)
- if any, the next synchronous code is executed (Not the code of the Future)

When that code will be executed and will complete or fail its `then()` or `catchError()` will directly be executed.

A Future is not executed in parallel but following the regular sequence of events, handed by the EventLoop.

## Async methods

- The outcome of the method is a `Future`.
- It runs synchronously the code of that method **up to the very first await** keyword, then it pauses the execution of the remainder of that method
- the next line of code will be run as soon as the `Future`, referenced by the `await` keyword, will ave completed.

An `async` method is NOT executed in parallel but following the regular sequence of events, handled by the Even Loop, too.

## Multi-Threading

An `Isolate` corresponds to the Dart version of the notion of Thread. "Isolates" in Flutter do not share memory. Interaction between "Isolates" is made via "messages" i terms of communication. 

- Each Isolate has its own Event Loop, thanks to it we can obtain parallel processing.




## References

[www.didierboelens.com](https://www.didierboelens.com/2019/01/futures-isolates-event-loop/)

