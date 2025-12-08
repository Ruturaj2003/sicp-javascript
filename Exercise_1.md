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
```

---
### Exercise 1.4

Observe that our model of evaluation allows for applications whose function expressions
are compound expressions. Use this observation to describe the behavior of `a_plus_abs_b`:

```js
function plus(a, b) {
  return a + b;
}

function minus(a, b) {
  return a - b;
}

function a_plus_abs_b(a, b) {
  return (b >= 0 ? plus : minus)(a, b);
}
```



#### Explanation of `a_plus_abs_b` Function Behavior

The function `a_plus_abs_b` works by choosing which function to use—either **addition** or
**subtraction**—based on whether `b` is positive or negative. Instead of using multiple `if` statements, it uses the **ternary operator (conditional expression)** to select a function first (the function name is chosen, then combined with the later part and invoked with `a` and `b`).

* If `b` is positive → result is `a + b`
* If `b` is negative → result is `a - (-b)`



#### What I Learned

##### 1. Functions Can Be Treated Like Values

A function is not a “special” thing—it behaves just like a number or a string.

For example, just like you can:

* Store a number in a variable
* Pass a number to another function
* Return a number from a function

You can do the **same with functions**:

* Store a function in a variable
* Pass a function as an argument
* Return a function from another function



##### 2. A Conditional Expression (Ternary Operator) Can Return a Function

This is something I’ve actually used a lot in React:

```js
isLoggedIn ? CompA : CompB
```

Since React components are basically functions, this is the same idea:
the ternary operator returns **one of two functions**.



##### 3. The Chosen Function Is Applied Only After the Condition Is Evaluated

First, the condition is evaluated.
Then, **the selected function is applied** to `a` and `b`.
---
This is how the function always returns the **absolute value effect** without using any built-in function like `Math.abs`.
 
 ---

