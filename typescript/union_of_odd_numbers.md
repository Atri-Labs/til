```ts
/**
 * Question: Write a generic type called OddNumberGenerator that
 * generates union of odd numbers.
 *
 * Concepts: Recursion, Spread in tuple
 */
type a = OddNumberGenerator<1>; // 1
type b = OddNumberGenerator<3>; // 1 | 3
type c = OddNumberGenerator<5>; // 1 | 3 | 5
type d = OddNumberGenerator<7>; // 1 | 3 | 5 | 7
```

```ts
/**
 * Solution
 */
type OddNumberGenerator<
	X extends number,
	Y extends number[] = [1],
	Z extends number = never
> = Y["length"] extends X
	? Z | Y["length"]
	: OddNumberGenerator<X, [1, 1, ...Y], Z | Y["length"]>;
```
