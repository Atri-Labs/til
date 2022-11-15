# Common hydration issues

-   You are displaying time on a page. This page might have a different time on the client side, because the timezone of the server and the client/browser are different. Using a random generator will have a similar effect.
-   You are using `mdx` that wraps new line inside a `<p>` element. Hence, the following code might have unexpected behavior:

<!-- prettier-ignore-start -->
```mdx
Email us at

<a>
 team@atrilabs.com
</a>
```
<!-- prettier-ignore-end -->

The above code might render as shown below in the HTML:

```html
<p>
	Email us at

	<a> <p>team@atrilabs.com</p> </a>
</p>
```

Few more common hydration related issues can be found in the below link:

-   https://nextjs.org/docs/messages/react-hydration-error

-   https://blog.somewhatabstract.com/2022/01/03/debugging-and-fixing-hydration-issues/
