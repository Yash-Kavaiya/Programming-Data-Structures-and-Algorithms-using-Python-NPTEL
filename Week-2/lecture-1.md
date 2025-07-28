# NPTEL MOOC: Introduction to Python Programming
## Module: Basic Python Concepts

---

## 1. Structure of a Python Program

### 1.1 Typical Program Organization

A well-structured Python program follows this general pattern:

```python
# Function definitions at the top
def function_1(param1, param2):
    # Function body
    ...
    
def function_2(param1, param2):
    # Function body
    ...
    
# More function definitions
def function_k(param1, param2):
    # Function body
    ...

# Main program statements
statement_1
statement_2
...
statement_n
```

**Key Points:**
- **Function definitions** are placed at the beginning of the program
- The Python interpreter reads these definitions and stores them for future use
- **Actual program execution** begins with the first statement after all function definitions
- Functions are only executed when they are called

### 1.2 Program Execution Flow

1. **Top-to-bottom execution**: Python interpreter reads the file from top to bottom
2. **Function registration**: When encountering `def` statements, Python registers the function but doesn't execute it
3. **Statement execution**: Actual computation starts from the first non-function-definition statement

### 1.3 Mixed Structure (Not Recommended)

While Python allows mixing function definitions and statements:

```python
statement_1
def function_1(...):
    ...
statement_2
statement_3
def function_2(...):
    ...
statement_4
```

**Why avoid this pattern?**
- Makes code harder to read and understand
- Difficult to debug
- Poor maintainability
- Violates standard programming conventions

---

## 2. Assignment Statements

### 2.1 Basic Assignment Syntax

```python
variable_name = expression
```

**Components:**
- **Left-hand side (LHS)**: Always a variable name
- **Right-hand side (RHS)**: An expression that evaluates to a value
- **Assignment operator**: `=` (single equals sign)

### 2.2 Assignment Examples

```python
i = 5           # Assign integer 5 to variable i
j = 2 * i       # Evaluate 2*i (which is 10) and assign to j
j = j + 5       # Evaluate j+5 (10+5=15) and reassign to j
```

**Important:** Assignment is not the same as mathematical equality. `j = j + 5` means "take the current value of j, add 5, and store the result back in j"

---

## 3. Numeric Values in Python

### 3.1 Integer Type (`int`)

**Definition:** Whole numbers without decimal points

**Examples:**
- Positive integers: `178`, `4283829`, `1`
- Negative integers: `-3`, `-999`, `-1`
- Zero: `0`

**Internal Representation:**
- Stored as binary numbers (sequence of 0s and 1s)
- Can represent arbitrarily large integers (limited only by memory)

### 3.2 Floating-Point Type (`float`)

**Definition:** Numbers with decimal points or fractional parts

**Examples:**
- `37.82`, `3.14159`, `0.5`
- `-0.01`, `-273.15`
- Scientific notation: `1.23e-4` (equals 0.000123)

**Internal Representation:**
- Uses mantissa and exponent format (similar to scientific notation)
- Example: 6.02 × 10²³ → mantissa: 6.02, exponent: 23
- Limited precision (approximately 15-17 decimal digits)

### 3.3 Why Two Different Types?

1. **Storage efficiency**: Integers use exact representation
2. **Computational differences**: Integer arithmetic is exact, float arithmetic may have rounding errors
3. **Different use cases**: 
   - Use `int` for counting, indexing
   - Use `float` for measurements, scientific calculations

---

## 4. Operations on Numbers

### 4.1 Basic Arithmetic Operations

| Operator | Operation | Example | Result Type |
|----------|-----------|---------|-------------|
| `+` | Addition | `5 + 3` → `8` | int + int → int<br>float involved → float |
| `-` | Subtraction | `10 - 7` → `3` | Same as addition |
| `*` | Multiplication | `4 * 6` → `24` | Same as addition |
| `/` | Division | `7 / 2` → `3.5` | **Always returns float** |

**Special Note on Division:**
```python
7 / 3.5  # Result: 2.0 (float)
7 / 2    # Result: 3.5 (float)
8 / 4    # Result: 2.0 (float, not 2)
```

### 4.2 Integer Division and Modulo

| Operator | Operation | Example | Explanation |
|----------|-----------|---------|-------------|
| `//` | Integer division (quotient) | `9 // 5` → `1` | How many times 5 goes into 9 |
| `%` | Modulo (remainder) | `9 % 5` → `4` | Remainder when 9 is divided by 5 |

**Relationship:** For any integers a and b (b ≠ 0):
```
a = (a // b) * b + (a % b)
```

### 4.3 Exponentiation

```python
3 ** 4    # 3 to the power 4 = 81
2 ** 10   # 2 to the power 10 = 1024
5 ** 0.5  # Square root of 5 ≈ 2.236
```

### 4.4 Mathematical Functions

To use advanced mathematical functions, import the math library:

```python
from math import *

# Now you can use:
sqrt(16)      # Square root: 4.0
log(10)       # Natural logarithm: 2.303...
sin(3.14159)  # Sine function: ≈ 0
cos(0)        # Cosine function: 1.0
floor(3.7)    # Floor function: 3
ceil(3.2)     # Ceiling function: 4
```

---

## 5. Names, Values, and Types

### 5.1 Dynamic Typing

**Key Concept:** Python uses dynamic typing
- Variable names don't have fixed types
- Types are associated with values, not names
- A name inherits its type from the value currently assigned to it

### 5.2 Type Flexibility Example

```python
i = 5        # i is now of type int
i = 7 * 1    # i is still int (7)
j = i / 3    # j is float (2.333...), division creates float
i = 2 * j    # i is now float (4.666...)
```

### 5.3 The `type()` Function

```python
type(5)           # <class 'int'>
type(3.14)        # <class 'float'>
type(True)        # <class 'bool'>

x = 10
type(x)           # <class 'int'>
x = 10.0
type(x)           # <class 'float'>
```

**Best Practice:** Although Python allows it, avoid assigning values of different types to the same variable name - it makes code harder to understand and maintain.

---

## 6. Boolean Values and Logic

### 6.1 Boolean Type (`bool`)

**Values:** Only two possible values
- `True`
- `False`

**Note:** Capitalization matters! `true` and `false` are not valid.

### 6.2 Logical Operators

#### NOT Operator
```python
not True   # False
not False  # True
```

#### AND Operator
```python
True and True    # True
True and False   # False
False and True   # False
False and False  # False
```

**Short-circuit evaluation:** If first operand is False, second is not evaluated

#### OR Operator
```python
True or True     # True
True or False    # True
False or True    # True
False or False   # False
```

**Short-circuit evaluation:** If first operand is True, second is not evaluated

---

## 7. Comparison Operators

### 7.1 Basic Comparisons

| Operator | Meaning | Example | Result |
|----------|---------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `<` | Less than | `3 < 5` | `True` |
| `>` | Greater than | `7 > 10` | `False` |
| `<=` | Less than or equal | `5 <= 5` | `True` |
| `>=` | Greater than or equal | `4 >= 8` | `False` |

### 7.2 Complex Comparisons

```python
# Combining comparisons with logical operators
n > 0 and m % n == 0    # Check if n is positive AND divides m

# Assigning boolean expressions to variables
divisor = (m % n == 0)  # divisor will be True or False
```

---

## 8. Practical Examples

### 8.1 Divisibility Checker

```python
def divides(m, n):
    """Check if m divides n evenly"""
    if n % m == 0:
        return True
    else:
        return False
```

**More concise version:**
```python
def divides(m, n):
    """Check if m divides n evenly"""
    return n % m == 0
```

### 8.2 Even/Odd Checkers

```python
def even(n):
    """Check if n is even"""
    return divides(2, n)

def odd(n):
    """Check if n is odd"""
    return not divides(2, n)
```

---

## Summary of Key Concepts

1. **Program Structure**
   - Organize with function definitions first, then main program statements
   - Python executes top-to-bottom, registering functions for later use

2. **Assignment Statements**
   - Use `=` to assign values to names
   - Right-hand side is evaluated first

3. **Numeric Types**
   - `int`: Whole numbers, exact representation
   - `float`: Decimal numbers, approximate representation
   - Division (`/`) always produces float

4. **Type System**
   - Python uses dynamic typing
   - Names inherit types from their values
   - Use `type()` to check types

5. **Boolean Logic**
   - Two values: `True` and `False`
   - Operators: `not`, `and`, `or`
   - Comparison operators produce boolean results

6. **Best Practices**
   - Keep consistent types for variables
   - Use meaningful variable names
   - Structure programs clearly with functions at the top

---

## Practice Exercises

1. Write a function to check if a number is divisible by both 3 and 5
2. Create a function that returns the type of a mathematical operation's result
3. Implement a function to determine if a year is a leap year using boolean logic
4. Write a program that demonstrates type changes through various operations
