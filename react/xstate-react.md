This post is about how to use `XState` library with `React`.

# What is XState?

It is an amazing state management library that manages charts using state charts, a extended version of state machines (a.k.a finite state automata). In plain words, we define a graph of states interconnected with each other. At one point of time, our state machine can be in one of the states and it can transition from one state to another upon some events. <b>An event causes transition from current state to a new state.</b> Some of the facts, like we can be at only one state at a time does not hold for state charts. You can learn details about state charts from [statecharts.dev](https://statecharts.dev). In the implementation of state charts by `XState` we can store information called `context` that persists across state transitions.

# XState and React

-   We generally define a state machine in one module using the `XState` library.
-   Rest of the `React` application can emit events that will lead to transition from current state to a new one. We generally call these events from the UI event listeners such as `MouseEvent`.
-   Upon receiving an event, the state machine transition from one state to another.
    -   We can define an action `function` that get executed during transition before we enter the new state and after we leave the old state. This `function` is a good choice to change the `context` of the machine.
    -   We can define functions that will be called upon when we exit or enter a state. These functions are generally referred to as `onEntry` and `onExit` functions. These functions are a good choice to inform rest of the application about the state change.
