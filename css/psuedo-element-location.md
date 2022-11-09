Pseudo elements are located inside the reference element. `::before` means before all the content of reference element and `::after` means after all the content of the reference element.

Refer to the CSS below:

```css
.div::before {
	content: "";
	width: 100px;
	height: 100px;
}
.div::after {
	content: "";
	width: 100px;
	height: 100px;
}
```

Then the HTML in the Chrome Dev Tool will look like this:

```html
<div>
	::before
	<!-- Other content below -->
	::after
</div>
```

This implies that size related properties if provided in % are relative to the parent. Obviously this holds as long as the containing block of the pseudo element is reference element. Read more about containing block in this [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_block).

Also, you cannot access pseudo elements from javascript and can only be manipulated using CSS.
