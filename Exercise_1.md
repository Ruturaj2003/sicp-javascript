### Exercise 1.1

 **Below is a sequence of statements. What is the result printed by the interpreter in response to each statement? Assume that the sequence is to be evaluated in the order in which it is presented.**

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

```js
2 + (b > a ? b : a);
```

**Result:** `6`

```js
(a > b
  ? a
  : a < b
  ? b
  : -1)
*
(a + 1);
```

**Result:** `16`

---

### Exercise 1.2

**Translate the following expression into JavaScript**  
*(Original math equation I couldn't copy)*

**Result:**
```js
(5 + 4 + (2 - (3 - (6 + 4 / 5))))
/
(3 * (6 - 2) * (2 - 7));
```
---

### Exercise 1.3

**Declare a function that takes three numbers as arguments and returns the sum of the squares  
of the two larger numbers**

```js
function sumOfSqrOfG2(
  num1,
  num2,
  num3
) {
  const lowestNum =
    num1 < num2
      ? (num1 < num3 ? num1 : num3)
      : (num2 < num3 ? num2 : num3);

  const result =
    num1 * num1 +
    num2 * num2 +
    num3 * num3 -
    (lowestNum * lowestNum);

  return Result;
}






