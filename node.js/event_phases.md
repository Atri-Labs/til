# NodeJS Event Loop Phases

## What happens when a NodeJS process starts?

Start App -> run root code -> run micro-tasks -> First cycle of event loop

-   On launch of your App, Node create a single thread.
-   The Event Loop gets initiated inside the thread.
-   Your root code executes before the Event Loop runs.
-   Each cycle of the Event Loop is called a **Tick**.
-   An Event Loop Tick is made up of multiple **phases**.

## Async functions in NodeJS

1. `setTimeout`
2. `setInterval`
3. `setImmediate`
4. `process.nextTick`
5. `Promise`

## Simplified view of event loop phases

1. Timers (setTimeout & setInterval is handled)
2. I/O Logic
3. Polling (incoming network requests are queued in the handle phase)
4. Check (setImmediate is handled)
5. Close (websocket close, child process exit are handled here)

## Micro-tasks

1. `process.nextTick`
2. `Promise`

`process.nextTick` is run before `Promise`.

The timers take some time to initialize when the event loop is initiated, hence, `setImmediate` might run before `setTimeout` even with time set as `0` milliseconds.

[YouTube video source](https://www.youtube.com/watch?v=ol56smloW2Q&list=PLISqeoHsXJYAIfu4-mgNY0tloWz2uut1t&index=1)
