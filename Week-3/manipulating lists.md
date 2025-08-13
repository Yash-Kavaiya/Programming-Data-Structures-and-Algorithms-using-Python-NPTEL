# manipulating lists

# Python Lists - Detailed Study Notes
*Based on NPTEL MOOC: Programming, Data Structures and Algorithms in Python*  
*Week 3, Lecture 2 - Madhavan Mukund, Chennai Mathematical Institute*

## 1. List Mutability - Core Concept

### Key Principle: Lists are Mutable Objects
- When you assign one list to another variable, both variables point to the **same list object**
- Changes made through one variable affect the other

### Example 1: Direct Element Assignment
```python
list1 = [1, 3, 5, 6]
list2 = list1
list1[2] = 7

# Result:
# list1 is now [1, 3, 7, 6]
# list2 is also [1, 3, 7, 6] (same object!)
```

### Example 2: Concatenation Creates New Lists
```python
list1 = [1, 3, 5, 6]
list2 = list1
list1 = list1[0:2] + [7] + list1[3:]

# Result:
# list1 is now [1, 3, 7, 6] (new object)
# list2 remains [1, 3, 5, 6] (original object)
```

**Important**: The `+` operator creates a **new list**, breaking the connection between variables.

## 2. List Extension Methods

### 2.1 Using `append()` - In-Place Addition
```python
list1 = [1, 3, 5, 6]
list2 = list1
list1.append(12)

# Result:
# list1 is now [1, 3, 5, 6, 12]
# list2 is also [1, 3, 5, 6, 12] (modified in place)
```

### 2.2 Using `extend()` - In-Place List Concatenation
```python
list1.extend([13, 14])  # Adds multiple elements from a list
# Equivalent to: list1 = list1 + [13, 14] (but in-place)
```

**Key Differences**:
- `append(v)`: Adds a single value `v`
- `extend(list2)`: Adds all elements from `list2`
- Both modify the original list (in-place operations)

### 2.3 Concatenation vs In-Place Operations
```python
# Creates NEW list (breaks connections)
list1 = list1 + [12]

# Modifies EXISTING list (maintains connections)  
list1.append(12)
```

## 3. List Functions and Methods

### 3.1 Removal Operations
```python
list1.remove(x)  # Removes FIRST occurrence of x
                 # Raises ValueError if x not found
```

**Safe removal pattern**:
```python
# Remove first occurrence safely
if x in list1:
    list1.remove(x)

# Remove ALL occurrences
while x in list1:
    list1.remove(x)
```

### 3.2 Other Important List Methods
```python
list1.reverse()     # Reverse list in place
list1.sort()        # Sort in ascending order (in place)
list1.index(x)      # Find leftmost position of x
                    # Raises ValueError if x not found
list1.rindex(x)     # Find rightmost position of x
```

**Safe index usage**:
```python
if x in list1:
    position = list1.index(x)
```

## 4. Object-Oriented Syntax Note

### Method Call Syntax
```python
# Python uses: object.method(arguments)
list1.append(x)

# Rather than: function(object, arguments)
# append(list1, x)  # This is NOT how Python works
```

**Explanation**:
- `list1` is an **object**
- `append()` is a **method** to update the object
- `x` is an **argument** to the method
- This object-oriented approach will be covered in detail later in the course

## 5. Slice Assignment - Advanced Manipulation

### 5.1 Basic Slice Replacement
```python
list1 = [1, 3, 5, 6]
list2 = list1
list1[2:] = [7, 8]  # Replace slice from position 2 onwards

# Result: Both list1 and list2 become [1, 3, 7, 8]
```

### 5.2 Expanding Lists with Slices
```python
list1 = [1, 3, 7, 8]
list1[2:] = [9, 10, 11]  # Replace 2 elements with 3 elements

# Result: [1, 3, 9, 10, 11] (list expanded)
```

### 5.3 Shrinking Lists with Slices
```python
list1[0:2] = [7]  # Replace 2 elements with 1 element

# Result: [7, 9, 10, 11] (list contracted)
```

**Warning**: Slice assignment can be confusing - use with care and ensure you understand the expected outcome.

## 6. List Membership Testing

### 6.1 The `in` Operator
```python
x in list1  # Returns True if x is found in list1
```

### 6.2 Practical Applications
```python
# Safe removal
if x in list1:
    list1.remove(x)

# Remove all occurrences
while x in list1:
    list1.remove(x)

# Safe index finding
if x in list1:
    position = list1.index(x)
```

## 7. Variable Initialization - Critical Requirement

### 7.1 The Problem
```python
# This will cause an error!
def factors(n):
    for i in range(1, n+1):
        if n % i == 0:
            flist.append(i)  # ERROR: flist is not defined
    return flist
```

### 7.2 The Solution
```python
# Correct version - initialize before use
def factors(n):
    flist = []  # Initialize empty list
    for i in range(1, n+1):
        if n % i == 0:
            flist.append(i)
    return flist
```

### 7.3 Why This Matters
- Python variables don't have predeclared types
- Python must know what type a variable is when methods are called
- `flist.append(i)` requires Python to know `flist` is a list
- **Always initialize variables before first use**

## 8. Key Takeaways and Best Practices

### 8.1 Memory and Reference Management
- Understand when operations create new objects vs modify existing ones
- Be especially careful with mutable objects in functions
- Use in-place operations when you want to maintain object references

### 8.2 Error Prevention
- Always check membership before using `remove()` or `index()`
- Initialize all variables before use
- Use meaningful variable names

### 8.3 Function Design
- If a function needs to return a modified list, decide whether to:
  - Modify the original list (in-place)
  - Return a new list (create copy)
- Document this behavior clearly

### 8.4 Documentation and Learning
- Python has many built-in list methods
- Consult Python documentation for complete method lists
- Experiment with the interactive interpreter to understand behavior
- Don't be afraid to test and explore!

## 9. Common Patterns and Idioms

### Building Lists in Functions
```python
def process_numbers(numbers):
    result = []  # Always initialize
    for num in numbers:
        if some_condition(num):
            result.append(processed_value)
    return result
```

### Safe List Manipulation
```python
# Safe removal of all occurrences
def remove_all(lst, value):
    while value in lst:
        lst.remove(value)

# Safe index finding
def find_position(lst, value):
    if value in lst:
        return lst.index(value)
    return -1  # or raise exception, or return None
```

---

*Note: This lecture emphasizes the fundamental concepts of list mutability and proper variable initialization - concepts that are crucial for avoiding common Python programming errors.*
