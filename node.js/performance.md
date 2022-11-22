## Recommended practices:

1. Import all modules in the top of the module.
2. Try to avoid `JSON.stringify`, `JSON.parse` and `console.log`. You can wrap it inside `setTimeout`/`setImmediate` or use streaming JSON library.
3. Prefer `setTimeout` and `setImmediate` over `Promise`. It will prevent blocking the event phase from reaching the `Polling` phase.
4. Offload the heavy tasks to child processes.

[YouTube video source](https://www.youtube.com/watch?v=ol56smloW2Q&list=PLISqeoHsXJYAIfu4-mgNY0tloWz2uut1t&index=1)
