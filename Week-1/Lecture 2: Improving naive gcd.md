# Lecture 2: Improving naive gcd
# Notes: Programming Concepts - GCD Algorithm and Loop Structures

## Overview
This lecture continues from a previous introduction to GCD (Greatest Common Divisor) and demonstrates how to progressively refine and optimize an algorithm while introducing new programming concepts.

## Basic GCD Algorithm

### Initial Approach
The naive algorithm follows the mathematical definition of GCD:
1. Create list `fm` - factors of m
2. Create list `fn` - factors of n  
3. Create list `cf` - common factors (elements in both fm and fn)
4. Return the largest value in cf (rightmost element since factors are added in ascending order)

## Algorithm Optimizations

### Optimization 1: Single Scan
Instead of two separate scans (1 to m, then 1 to n):
- Scan once from 1 to max(m,n)
- For each i, check if it divides m (add to fm) and if it divides n (add to fn)

### Optimization 2: Direct Common Factor Computation
- Skip creating separate lists fm and fn
- Directly compute common factors in one pass
- Scan from 1 to min(m,n) instead of max(m,n)
  - Any common factor must be ≤ min(m,n)

**Python Implementation:**
```python
def gcd(m,n):
    cf = []
    for i in range(1,min(m,n)+1):
        if (m%i) == 0 and (n%i) == 0:
            cf.append(i)
    return(cf[-1])
```

### Optimization 3: Eliminate List Storage
- We only need the largest common factor, not all of them
- Use variable `mrcf` (most recent common factor)
- Update mrcf each time a new common factor is found

**Python Implementation:**
```python
def gcd(m,n):
    for i in range(1,min(m,n)+1):
        if (m%i) == 0 and (n%i) == 0:
            mrcf = i
    return(mrcf)
```

### Optimization 4: Scan Backwards
- Start from min(m,n) and work backwards to 1
- First common factor found is the GCD
- Can return immediately without checking remaining values

**Python Implementation with While Loop:**
```python
def gcd(m,n):
    i = min(m,n)
    while i > 0:
        if (m%i) == 0 and (n%i) == 0:
            return(i)
        else:
            i = i-1
```

## New Programming Concepts

### While Loops
- **Syntax:** 
  ```python
  while condition:
      step 1
      step 2
      ...
      step k
  ```
- Used when number of iterations is unknown in advance
- Continues executing while condition is true
- Must ensure condition eventually becomes false to avoid infinite loops

### For vs While Loops
- **For loops:** Used when number of iterations is known (fixed repetitions)
- **While loops:** Used when stopping condition is dynamic

### Important Python Distinctions
- `=` : Assignment operator (assigns value to variable)
- `==` : Equality comparison operator (checks if values are equal)
- `i = i - 1` : Updates variable i by subtracting 1

### Loop Termination
- Critical to ensure while loops terminate
- Must make progress toward making condition false
- In the example: Starting with min(m,n) and decrementing by 1 guarantees reaching 0

## Key Insights

1. **Guaranteed Solution:** 1 is always a common factor, so GCD is always well-defined

2. **Computational Complexity:** Despite optimizations making code simpler, all versions still take time proportional to min(m,n) in worst case

3. **Trade-offs:** 
   - Simpler code is easier to understand and maintain
   - These optimizations don't significantly improve time complexity
   - A "dramatically different" and more efficient approach exists (teased for next lecture)

## Summary
The lecture demonstrates how iterative refinement can simplify code while maintaining functionality. It introduces while loops as a control structure for indefinite iteration and emphasizes the importance of ensuring loop termination. While the optimizations make the code cleaner, they don't fundamentally change the algorithm's efficiency - suggesting more advanced techniques will be covered later.

![](https://gist.githubusercontent.com/Yash-Kavaiya/3ef9bf4a89423647b953ba01f82fb478/raw/a56274f44b4bd55f2bd8d11c2c3013f5f120f4fc/Improving%2520naive%2520gcd.svg)
