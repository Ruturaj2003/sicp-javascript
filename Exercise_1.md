### Exercise 1.1

#### Below is a sequence of statements. What is the result printed by the interpreter in response

to each statement? Assume that the sequence is to be evaluated in the order in which it is
presented.

```js
10;
```

**Result:** `10`

```js
5 + 3 + 4;
```

**Result:** `12`

```js
9 - 1;
```

**Result:** `8`

```js
6 / 2;
```

**Result:** `3`

```js
2 * 4 + (4 - 6);
```

**Result:** `6`

```js
const a = 3;
const b = a + 1;
a + b + a * b;
```

**Result:** `19`

```js
a === b;
```

**Result:** `false`

```js
b > a && b < a * b ? b : a;
```

**Result:** `4`

```js
a === 4
  ? 6
  : b === 4
  ? 6 + 7 + a
  : 25;
```

**Result:** `16`

---