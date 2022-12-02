```ts
type IsOddLength<X extends unknown[]> = X extends [boolean, ...infer V]
	? V["length"] extends 0
		? true
		: IsEvenLength<V>
	: false;

type IsEvenLength<X extends unknown[]> = X["length"] extends 0
	? true
	: X extends [boolean, boolean, ...infer V]
	? V["length"] extends 0
		? true
		: IsEvenLength<V>
	: false;

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
type OddNumberGenerator<
	X extends number,
	Y extends number[] = [1],
	Z extends number = never
> = Y["length"] extends X
	? Z | Y["length"]
	: OddNumber<X, [1, 1, ...Y], Z | Y["length"]>;

type a = OddNumberGenerator<1>; // 1
type b = OddNumberGenerator<3>; // 1 | 3
type c = OddNumberGenerator<5>; // 1 | 3 | 5
type d = OddNumberGenerator<7>; // 1 | 3 | 5 | 7
```
