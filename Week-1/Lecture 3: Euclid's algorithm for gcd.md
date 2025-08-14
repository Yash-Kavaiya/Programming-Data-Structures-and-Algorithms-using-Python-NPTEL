# Detailed Notes: Algorithms for GCD (Greatest Common Divisor)

## 1. Introduction to GCD
The **Greatest Common Divisor (GCD)** of two numbers m and n is the largest positive integer that divides both numbers without remainder.

### Basic Definition Approach
The most straightforward approach to find GCD involves:
1. Find all factors of m → store in a list
2. Find all factors of n → store in another list  
3. Extract common factors from both lists
4. Report the largest common factor

## 2. Progressive Simplifications

### First Simplification: Direct Common Factor Computation
- **Insight**: No need to compute factors separately
- **Method**: Single pass from 1 to min(m,n)
- Directly compute list of common factors without separately finding factors of m and n

### Second Simplification: Track Only Maximum
- **Insight**: We only need the greatest common factor, not the entire list
- **Method**: Keep track of the largest common factor seen so far in a single variable
- Report it at the end

### Third Simplification: Start from the End
- **Key Observation**: Since we want the *largest* common factor, start from the largest possible value
- **Method**: 
  - Start from min(m,n) and work backwards to 1
  - First common factor found will be the GCD
  - Note: 1 is guaranteed to be a common factor (worst case)

```python
# Working backwards approach
def gcd_backwards(m, n):
    for i in range(min(m,n), 0, -1):
        if m % i == 0 and n % i == 0:
            return i
```

### Efficiency Issue
All these naive approaches have the same worst-case efficiency: O(min(m,n)) - they potentially check all numbers from 1 to min(m,n).

## 3. Euclid's Algorithm - The Mathematical Breakthrough

### Core Mathematical Insight
**Theorem**: If d divides both m and n (where m > n), then d also divides (m - n)

**Proof**:
- If d divides m and n, then:
  - m = a·d for some integer a
  - n = b·d for some integer b
- Therefore: m - n = a·d - b·d = (a-b)·d
- So d divides (m - n) as well

**Conclusion**: gcd(m, n) = gcd(n, m - n)

### Version 1: Using Difference

#### Algorithm Steps:
1. Assume m ≥ n (swap if needed)
2. If n divides m, return n
3. Otherwise, compute gcd(n, m-n)

#### Python Implementation (Recursive):
```python
def gcd(m, n):
    # Assume m >= n
    if m < n:
        (m, n) = (n, m)  # Simultaneous assignment in Python
    
    if (m % n) == 0:
        return n
    else:
        diff = m - n
        # Note: diff might be > n, so we need max/min
        return gcd(max(n, diff), min(n, diff))
```

#### Python Implementation (Iterative):
```python
def gcd(m, n):
    if m < n:  # Assume m >= n
        (m, n) = (n, m)
    
    while (m % n) != 0:
        diff = m - n
        (m, n) = (max(n, diff), min(n, diff))
    
    return n
```

### Key Python Features Introduced:
1. **Comments**: Lines starting with `#` are ignored by Python
2. **Simultaneous Assignment**: `(m, n) = (n, m)` swaps values without temporary variable
3. **Recursion**: Function calling itself with smaller arguments

### Problem with Difference Method:
For numbers like gcd(101, 2), this method takes ~50 steps (101→99→97→...→3→1), which is worse than the naive approach in some cases.

## 4. Euclid's Algorithm - Optimized Version Using Remainder

### Enhanced Mathematical Insight
**Theorem**: If d divides both m and n, then d also divides the remainder of m÷n

**Proof**:
- m = q·n + r (where q is quotient, r is remainder, and r < n)
- If d divides m and n:
  - m = a·d and n = b·d
  - a·d = q·(b·d) + r
  - Therefore: r = d·(a - q·b)
- So d divides r as well

**Conclusion**: gcd(m, n) = gcd(n, r) where r = m % n

### Version 2: Using Remainder (Modulo)

#### Algorithm Steps:
1. Assume m ≥ n (swap if needed)
2. If n divides m, return n
3. Otherwise, let r = m % n
4. Return gcd(n, r)

#### Python Implementation (Recursive):
```python
def gcd(m, n):
    if m < n:  # Assume m >= n
        (m, n) = (n, m)
    
    if (m % n) == 0:
        return n
    else:
        return gcd(n, m % n)  # m%n < n, always!
```

#### Python Implementation (Iterative):
```python
def gcd(m, n):
    if m < n:  # Assume m >= n
        (m, n) = (n, m)
    
    while (m % n) != 0:
        (m, n) = (n, m % n)  # m%n < n, always!
    
    return n
```

### Advantages of Remainder Method:
- **No need for max/min**: Remainder is always less than divisor
- **Much faster convergence**: Each step significantly reduces the problem size

## 5. Efficiency Comparison

| Algorithm | Time Complexity | Example: gcd(101, 2) |
|-----------|----------------|---------------------|
| Naive (counting up) | O(min(m,n)) | ~2 steps |
| Naive (counting down) | O(min(m,n)) | ~2 steps |
| Euclid's (difference) | O(max(m,n)) worst case | ~50 steps |
| **Euclid's (remainder)** | **O(log(min(m,n)))** | **2 steps** |

### Key Efficiency Insight:
The remainder version of Euclid's algorithm takes time proportional to the **number of digits** in the numbers, not the numbers themselves.

**Example**: 
- For a billion (10⁹ ≈ 10 digits):
  - Naive algorithm: ~1 billion steps
  - Euclid's (remainder): ~10 steps

## 6. Important Programming Concepts

### Recursion
- Function calling itself with smaller arguments
- Must have a **base case** (termination condition)
- Must make **progress** toward the base case
- Example: In GCD, numbers get smaller until n divides m

### Loop Invariants
- While loops must make progress toward termination
- Similar to recursion's need for a base case
- Condition must eventually become false

### Algorithm Design Principles
1. **Correctness**: Does it produce the right answer?
2. **Efficiency**: How fast does it run?
3. **Clarity**: Is the code readable and maintainable?

## 7. Summary
Euclid's algorithm (remainder version) represents one of the first known algorithms in history and demonstrates:
- How mathematical insights can dramatically improve efficiency
- The power of recursion in problem-solving
- The importance of choosing the right approach (remainder vs. difference)
- Time complexity improvement from O(n) to O(log n)

This algorithm remains fundamental in computer science for:
- Cryptography (RSA algorithm)
- Simplifying fractions
- Solving linear Diophantine equations
- Various number theory applications

![](https://gist.githubusercontent.com/Yash-Kavaiya/be7de4e58cf76cc9bd897f3ce4329deb/raw/59495ca11953bd01fddf29e219bdaa086b10d8b8/Euclid's%2520algorithm.svg)
