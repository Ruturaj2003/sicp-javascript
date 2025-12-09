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

This is how the function always returns the **absolute value effect** without using any built-in function like `Math.abs`.
 
 ---



## Exercise 1.5

Ben Bitdiddle has invented a test to determine whether the interpreter he is faced with is
using **applicative-order evaluation** or **normal-order evaluation**. He declares the following
two functions:

```js
function p() {
  return p();
}

function test(x, y) {
  return x === 0 ? 0 : y;
}
```

Then he evaluates the statement:

```js
test(0, p());
```

### Questions

* What behavior will Ben observe with an interpreter that uses **applicative-order evaluation**?
* What behavior will he observe with an interpreter that uses **normal-order evaluation**?

Explain your answer.

*(Assume that the evaluation rule for conditional expressions is the standard one.)*


#### **Solution**

This exercise shows the difference between **applicative-order evaluation** and **normal-order evaluation**.

##### **Applicative-Order Evaluation (what JavaScript uses)**

In applicative order, the interpreter **evaluates all arguments before calling the function**.

So when evaluating:

* `test(0, p())`

The interpreter will:

1. Try to evaluate `0` → this is fine.
2. Then try to evaluate `p()` **before** entering `test`.
3. But `p()` calls itself forever and never returns.

So the program gets **stuck in an infinite loop** and never reaches the `test` function body.

**Result:** Infinite loop (program never finishes).


##### **Normal-Order Evaluation**

In normal order, the interpreter **does NOT evaluate arguments first**. It substitutes them into the function body and only evaluates them if they are actually needed.

So for:

* `test(0, p())`

The interpreter:

1. Enters the function body first.
2. Checks the condition: `x === 0` → this is true.
3. Since the condition is true, it immediately returns `0`.
4. The expression `p()` is **never evaluated**.

**Result:** The program returns `0` with no infinite loop.

---

### Exercise 1.7

The `is_good_enough` test used in computing square roots is not very effective for finding the square roots of **very small numbers**. Also, in real computers, arithmetic operations are almost always performed with **limited precision**. This makes our test inadequate for **very large numbers** as well.

Explain these statements, with examples showing how the test fails for small and large numbers.

An alternative strategy for implementing `is_good_enough` is to watch how the **guess changes from one iteration to the next** and to stop when the change is a very small **fraction of the guess**.

Design a square-root function that uses this kind of end test. Does this work better for small and large numbers?

---

### Answer

#### 1. Why the Original `is_good_enough` Test Fails for Very Small Numbers

The original test checks whether the absolute difference between `guess²` and `x` is smaller than `0.001`:

```
|guess² - x| < 0.001
```

This test fails for **very small numbers** because `0.001` is a **huge threshold** when compared to tiny values.

#### Example

Suppose we want to compute:

```
sqrt(0.0001)
```

The correct answer is:

```
0.01
```

Now assume the iterative guess becomes:

```
guess = 0.03
```

Then:

```
guess² = 0.0009
|0.0009 - 0.0001| = 0.0008
```

Since:

```
0.0008 < 0.001
```

the program incorrectly decides that the answer is **good enough** and stops, even though `0.03` is **three times larger than the correct value `0.01`**.

#### Conclusion

When the number itself is smaller than the fixed threshold (`0.001`), the program **stops too early**, producing a **poor result**.

---

#### 2. Why the Test Also Fails for Very Large Numbers

As stated in the question, real computers use **limited precision** to represent numbers. For extremely **large values**, squaring a large `guess` produces numbers so big that the computer:

* Cannot track **tiny differences accurately**
* Must **round off** small decimal values

#### Example

Consider a guess like:

```
1334343443.2342
```

Squaring this value results in a massive number where:

* Small decimal changes are **lost due to rounding**
* The expression `|guess² - x|` may:

  * Become `0` too early
  * Never become smaller than `0.001`
  * Or behave **unpredictably**

This makes the test:

```
|guess² - x| < 0.001
```

**unreliable** for very large numbers.

#### Important Clarification

The problem is **not merely that large numbers are inaccurate**. The real issue is that **floating-point numbers lose the ability to represent very small differences at large scales**.

---

#### 3. Improved `is_good_enough` Strategy (Change-Based Test)

Instead of checking how close `guess²` is to `x`, a better approach is to check:

> **How much the guess itself changes between iterations**

#### Key Idea

* Stop when the **new guess is almost the same as the old guess**
* The difference must be a **fraction of the guess**, not a fixed number

#### Example

Let the threshold be **1% of the old guess**.

If:

```
old_guess = 10
new_guess = 9.1
threshold = 10 × 0.01 = 0.1
```

Then:

```
|10 - 9.1| = 0.9 > 0.1   Not close enough
```

But if:

```
old_guess = 10
new_guess = 10.02
```

Then:

```
|10 - 10.02| = 0.02 < 0.1   Close enough, stop
```

#### In Simple Words

> Stop when the change between two consecutive guesses is **very small compared to the size of the current guess**.

---

#### 4. Why This Method Works Better

This improved method:

* Does **not stop early** for small numbers
* Does **not loop endlessly** for large numbers
* Automatically **adapts to the scale of the number**
* Uses a **dynamic threshold** instead of a fixed constant





