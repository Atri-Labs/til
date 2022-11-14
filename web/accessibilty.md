# Accessibility

## Tools

There are many tools and libraries that help us check accessibility in our web application. All these tools can be used in different ways:

1. If you want to check from command line using ESLint, you can use an ESLint plugin called [`eslint-plugin-jsx-a11y`](https://www.npmjs.com/package/eslint-plugin-jsx-a11y).

2. If you want to check accessibility issues at runtime during development, you can use [`@axe-core/react`](https://www.npmjs.com/package/@axe-core/react) library. The issues will be highlighted in the console of the browser.

3. Use browser extension such as `axe` or [`tota11y`](https://chrome.google.com/webstore/detail/tota11y-for-chrome/nkghaekndgmonifcpfgjmpfjlhnmflhp). It is easy to visualize issues using [`tota11y`](https://chrome.google.com/webstore/detail/tota11y-for-chrome/nkghaekndgmonifcpfgjmpfjlhnmflhp).

4. For color contrast related issues, use the browser extension [`High Contrast Browser Extension`](https://chrome.google.com/webstore/detail/high-contrast/djcfdncoelnlbldjfhinnjlhdjlikmph).

## Rules

1. The page must have a `h1` tag and then the headings must be contiguous in the page.

2. An `<img>` must have an `alt` attribute. If the `alt` attribute is set to empty string like `alt=""`, then the screen reader will skip announcing that image. This behavior is useful if the image is not important.

3. A page must use `HTML5` landmark regions like `header`, `nav`, `main`, `footer` etc. Alternatively, we can use `role` attribute to provide the same behavior. It is actually value of the `role` attribute, then helps screen reader to decide what to say during voice over.

4. Use good color contrast.

## Aria Attributes

-   [`aria-labelledby`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-labelledby) - Useful in situations like when `<label>` does not encapsulate a form element.

-   [`aria-describedBy`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-describedby) - Useful in situations when the written content is not suitable for screen readers and we want an alternate content to be read.

-   [`aria-live`](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Live_Regions) - Useful when content of an element will change over time, for example, username/password error messages during sign up.

Source for all this content is [in this video tutorial at egghead.io](https://egghead.io/courses/develop-accessible-web-apps-with-react).
