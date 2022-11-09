# What is a controlled input?

Imagine you want user to write text in the input in a certain way, hence, on every keystroke you would like to run some logic that decides the character is acceptable or not. This is a solid case where you would like to use controlled components.

```tsx
// This is just a placeholder function to be used below
function processTextValue(value: string) {
	return value.replace("u", "k");
}

// This is just a placeholder function to be used below
function computeNewCursorPosition(e: KeyboardEvent) {
	return 7; // return new cursor position
}

function useSetCursor() {
	const fnRef = useRef<Function | null>();

	/**
	 * We call the function inside useLayoutEffect because we don't want
	 * to change the cursor position until React has processed the new text value
	 * set by the onChange callback.
	 */
	useLayoutEffect(() => {
		if (ref.current !== null) {
			ref.current();
		}
	}, []);

	return (fn) => {
		fnRef.current = fn;
	};
}

function ControlledInput() {
	const [value, setValue] = useState();

	const setCursorFn = useSetCursor();

	const onChange = useCallback(
		(e: KeyboardEvent) => {
			const newTextValue = processTextValue(e.target.value);
			const newCursorPosition = computeNewCursorPosition(e);
			setValue(newTextValue);
			setCursorFn(() => {
				// TODO: write correct code here
				e.selection.cursor = newCursorPosition;
			});
		},
		[setCursorFn]
	);

	return <input value={value} onChange={onChange} />;
}
```
