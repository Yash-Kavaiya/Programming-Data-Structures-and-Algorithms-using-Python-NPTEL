We are given a function:

```python
def g(y):
    b = 0
    while y >= 3:
        (y, b) = (y / 3, b + 1)
    return b
```

We are to find the value of `g(728)`.

---

### Let's understand what the function does:

* It initializes `b = 0`.
* Then it keeps dividing `y` by 3 while `y >= 3`, and increments `b` each time.
* When `y < 3`, it stops and returns `b`.

So `b` counts how many times `y` can be divided by 3 before dropping below 3.

This is essentially calculating the **floor of the base-3 logarithm** of `y`, i.e.

$$
g(y) = \left\lfloor \log_3(y) \right\rfloor
$$

---

### Let's compute:

We’ll simulate the loop with `y = 728`:

| Iteration | y                         | b |
| --------- | ------------------------- | - |
| 0         | 728                       | 0 |
| 1         | 728 / 3 = 242.666...      | 1 |
| 2         | 242.666 / 3 = 80.888...   | 2 |
| 3         | 80.888 / 3 = 26.962...    | 3 |
| 4         | 26.962 / 3 = 8.987...     | 4 |
| 5         | 8.987 / 3 = 2.9958... < 3 | 5 |

At this point, `y < 3`, so the loop ends.

---

### ✅ Final Answer:

$$
\boxed{5}
$$

We are given the Python function:

```python
def f(n):
    s = 0
    for i in range(2, n):
        if n % i == 0 and i % 2 == 1:
            s = s + 1
    return s
```

---

### 🔍 What does this function do?

It counts how many **odd** numbers `i` from 2 up to `n-1` **divide `n` exactly**.

So `f(n)` returns the **number of odd proper divisors** of `n` (excluding 1 and `n` itself).

---

### We are asked to find:

$$
f(90) - f(89)
$$

---

### Step 1: Compute `f(90)`

Find all **odd** integers `i` from 2 to 89 such that `90 % i == 0`.

Divisors of 90:
90 = 2 × 3 × 3 × 5 → Divisors = 1, 2, 3, 5, 6, 9, 10, 15, 18, 30, 45, 90

Odd proper divisors (between 2 and 89):

* 3
* 5
* 9
* 15
* 45

That’s **5** odd proper divisors.

✅ `f(90) = 5`

---

### Step 2: Compute `f(89)`

89 is a **prime number**, so it has no divisors between 2 and 88.
Thus, `f(89) = 0`

---

### Final Answer:

$$
f(90) - f(89) = 5 - 0 = \boxed{5}
$$
We are given the function:

```python
def h(n):
    s = True
    for i in range(1, n + 1):
        if i * i == n:
            s = False
    return s
```

---

### 🔍 What does this function do?

* It loops over all integers `i` from `1` to `n`, and checks whether `i * i == n`.
* If it finds such an `i`, then it sets `s = False`.
* Finally, it returns `s`.

So:

* If `n` **is a perfect square**, i.e., there exists some integer `i` such that `i*i == n`, then the function returns **False**.
* Otherwise, it returns **True**.

---

### ✅ Therefore, the function `h(n)` returns **False** **if and only if**:

$$
\boxed{\text{n is a perfect square}}
$$

✔️ Correct option: **n is a perfect square** ✅
We are given this recursive function:

```python
def foo(m):
    if m == 0:
        return 0
    else:
        return m + foo(m - 1)
```

---

### 🔍 Let’s understand what this function does.

It returns:

$$
\text{foo}(m) = m + (m - 1) + (m - 2) + \dots + 1 + 0
$$

So, it sums all integers from `0` to `m`.
This is the formula for the **sum of first m natural numbers**:

$$
\text{foo}(m) = \frac{m(m+1)}{2}
$$

---

### ✅ Now, evaluate the options:

1. ❌ **"foo(n) = factorial of n"** – Incorrect. Factorial is `n * (n - 1) * ... * 1`, not a sum.
2. ✅ **"foo(n) = n(n+1)/2"** – **Correct!**
3. ❌ "terminates for non-negative n with factorial" – Again, incorrect operation.
4. ✅ **"terminates for non-negative n with foo(n) = n(n+1)/2"** – **Correct again.**

---

### ✅ Final Correct Answer:

$$
\boxed{\text{The function terminates for non­negative n with foo(n) = } \frac{n(n+1)}{2}}
$$
