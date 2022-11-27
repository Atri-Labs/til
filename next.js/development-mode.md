# Development Mode

## How does Next.JS detects & fetches a new page?

In a fresh NextJS project, I start the dev server by running yarn dev and add the following code to the pages/index.jsx:

```jsx
export default Home(){
 return <Link href="/abc">Go to abc</Link>
}
```

Suppose I create a new page in the `pages` directory called `abc.js` with the following code:

```jsx
export default AbcPage(){
 return <div>Welcome to ABC page.</div>
}
```

By looking at the output in the terminal, it seems the new page has not been compiled yet, and the moment I click on the abc in the home page, compilation happens and a abc.js chunk is downloaded in the browser.

##The question is, how did NestJS configure webpack to load chunks on-demand?##

### On the server side

Next.JS uses `webpack.MultiCompiler`. Also, Next.JS seems to be using it's own version of the `webpack-dev-server`. Whenever the `DevServer` receives request for a new page, the new entry is added to the webpack `entry` and `compiler.watching?.invalidate()` is called. This is made possible due to the Webpack's [dynamic entry](https://webpack.js.org/configuration/entry-context/#dynamic-entry) feature.

Next.JS has created many `webpack` loaders and one such loader is `next-client-pages-loader`. Next.JS uses another feature of Webpack called [inline](https://webpack.js.org/concepts/loaders/#inline) loaders. Using this feature, the `absolutePagePath` and `page` is passed to `next-client-pages-loader` that returns a code that looks like below:

```jsx
    (window.__NEXT_P = window.__NEXT_P || []).push([
      ${stringifiedPage},
      function () {
        return require(${stringifiedPageRequest});
      }
    ]);
    if(module.hot) {
      module.hot.dispose(function () {
        window.__NEXT_P.push([${stringifiedPage}])
      });
    }
```

When Webpack finds the `require` function on the above code, it imports that module as dependency of the above shown code. This is one of the secret sauce of the entire process.

### On the client side

The `Link` component from `next/link` invokes `NextRouter.replace()` or `NextRouter.push()`.

### After receiving the module from the server

The `__NEXT_P` is an array, with a new method attached called `push`. This `push` method is assigned a function called `register`.
