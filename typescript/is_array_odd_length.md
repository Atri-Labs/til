```ts
/**
 * Question: Create a Generic type called IsOddLength that
 * returns true if the provided array type is of odd length
 * otherwise false.
 *
 * Concepts: Recursion, Generics, Conditional type inference
 */

/**
 * Sample test cases
 */
type h = IsOddLength<[]>; // typeof h === false
type i = IsOddLength<[true]>; // typeof i === true
type j = IsOddLength<[true, true]>; // typeof j === false
type k = IsOddLength<[true, true, true]>; // typeof k === true
type l = IsOddLength<[true, true, true, true]>; // typeof l === false
```

```ts
/**
 * Solution
 */
type IsEvenLength<X extends unknown[]> = X["length"] extends 0
	? true
	: X extends [boolean, boolean, ...infer V]
	? V["length"] extends 0
		? true
		: IsEvenLength<V>
	: false;

type IsOddLength<X extends unknown[]> = X extends [boolean, ...infer V]
	? V["length"] extends 0
		? true
		: IsEvenLength<V>
	: false;
```
