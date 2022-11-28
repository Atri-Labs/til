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

#### `next/link`

-   The `Link` component from `next/link` invokes a series of nested functions `linkClicked` -> `navigate` -> `NextRouter.replace()` or `NextRouter.push()`.
-   Contexts used `RouterContext` and `AppRouterContext`:

```tsx
const pagesRouter = React.useContext(RouterContext);
const appRouter = React.useContext(AppRouterContext);
const router = pagesRouter ?? appRouter;
```

-   What does this mean?

```tsx
// We're in the app directory if there is no pages router.
const isAppRouter = !pagesRouter;
```

-   `AppRouterContext` contains value of type `AppRouterInstance`. `RouterContext` contains value of type `NextRouter`.

#### `packages/next/shared/lib/router/router.ts`

The `Router` class has `push` and `replace` methods that ultimately call `change` method. The `change` method tries to get the `routeInfo` using `getRouteInfo` method. If the route is not already in the `cachedRouteInfo` then `fetchComponent` method is called inside `getRouteInfo` method. Here is a weird part, this `cachedRouteInfo` is actually always `undefined` in `development` mode.

```tsx
let cachedRouteInfo =
	existingInfo &&
	!("initial" in existingInfo) &&
	process.env.NODE_ENV !== "development"
		? existingInfo
		: undefined;
```

The `routeInfo` is an instance of type `CompletePrivateRouteInfo`, that is something like this:

```tsx
this.fetchComponent(route).then<CompletePrivateRouteInfo>(
          (res) => ({
            Component: res.page,
            styleSheets: res.styleSheets,
            __N_SSG: res.mod.__N_SSG,
            __N_SSP: res.mod.__N_SSP,
          })
```

### After receiving the module from the server

The `__NEXT_P` is an array, with a new method attached called `push`. This `push` method is assigned a function called `register`.

### Variables attached to self

-   globalThis.\_\_NEXT_P
-   globalThis.\_\_NEXT_DATA\_\_
-   \_\_N_SSG (comes from destructured `routeInfo`)
-   \_\_N_SSP (comes from destructured `routeInfo`)

### Client side environment variables

-   \_\_NEXT_ROUTER_BASEPATH
-   \_\_NEXT_SCROLL_RESTORATION
-   \_\_NEXT_I18N_SUPPORT
