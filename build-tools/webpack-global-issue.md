It's well known that `Webpack` hoists all the ES6 styled imports to the top of the module. This can pose challenges if we intend to run the `React` code in the `NodeJS` world such as `HookWebpackError: window not defined`.

Even the code below will node come to rescue because all the imports will execute first and then the `global.window = undefined` statement.

```js
global.window = undefined;

import { abc } from "xyz";
```

The only way out is to define `global.window` in the entry JS/TS module before actually touching any `React` code.
