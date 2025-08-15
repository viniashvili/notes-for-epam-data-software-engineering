# Python

## *Lambda Functions*

### **What is a Lambda Function**

* A lambda function is a small anonymous function defined with the `lambda` keyword.
* It can take any number of arguments but has only one expression.
* The expression is evaluated and returned automatically.
* Useful for short, simple functions that are used temporarily.

---

### **Syntax of Lambda Function**

```python
lambda arguments: expression
```

* `arguments` — input parameters, can be zero or more.
* `expression` — single expression that is evaluated and returned.
* No need to use `return` keyword.
* Lambda functions are anonymous (no function name).

---

### **Examples**

* Simple lambda that adds two numbers:

```python
add = lambda x, y: x + y
print(add(2, 3))  # Output: 5
```

* Lambda with no arguments returning a constant:

```python
const = lambda: 42
print(const())  # Output: 42
```

* Using lambda inside built-in functions like `sorted`:

```python
points = [(2, 3), (1, 5), (4, 1)]
sorted_points = sorted(points, key=lambda x: x[1])
print(sorted_points)  # Output: [(4, 1), (2, 3), (1, 5)]
```

---

### **When to Use Lambda Functions**

* For small, throwaway functions used only once.
* When passing a simple function as an argument (e.g., to `map()`, `filter()`, `sorted()`).
* To keep code concise and avoid defining a separate named function.

---

### **Limitations of Lambda Functions**

* Limited to a single expression — no statements or multiple lines.
* Cannot contain commands like loops, `if` statements (though ternary operator works).
* Harder to debug because they are anonymous.
* For complex functions, prefer defining a regular function with `def`.

---

### **Lambda vs Regular Function**

| Feature    | Lambda                 | Regular Function        |
| ---------- | ---------------------- | ----------------------- |
| Definition | Anonymous, inline      | Named, can be multiline |
| Body       | Single expression only | Multiple statements     |
| Usage      | Simple, short-term use | Complex, reusable logic |
| Debugging  | Difficult              | Easier                  |

---

## *Recursion*

### **What is Recursion**

* Recursion is a programming technique where a function calls itself to solve smaller instances of the same problem.
* The recursive calls continue until a base case (termination condition) is met.
* Useful for problems that can be broken down into similar subproblems, such as tree traversal, factorial, Fibonacci sequence, etc.

---

### **How Recursion Works**

* A recursive function has two main parts:

  * **Base case:** The condition under which the recursion stops.
  * **Recursive case:** The function calls itself with modified arguments to approach the base case.
* Each recursive call adds a new layer to the call stack.
* When the base case is reached, the call stack starts to unwind, returning results back up the chain.

---

### **Basic Syntax of a Recursive Function**

```python
def recursive_function(parameters):
    if base_case_condition:
        return base_case_value
    else:
        return recursive_function(modified_parameters)
```

---

### **Example: Factorial Function**

```python
def factorial(n):
    if n == 0:
        return 1  # Base case
    else:
        return n * factorial(n - 1)  # Recursive case

print(factorial(5))  # Output: 120
```

---

### **Example: Fibonacci Sequence**

```python
def fibonacci(n):
    if n <= 1:
        return n  # Base case
    else:
        return fibonacci(n-1) + fibonacci(n-2)  # Recursive case

print(fibonacci(6))  # Output: 8
```

---

### **Advantages of Recursion**

* Simplifies code for problems naturally defined by self-similarity.
* Makes code easier to write and understand for complex problems like tree/graph traversal, divide-and-conquer algorithms.

---

### **Disadvantages and Limitations**

* Recursive calls consume more memory (stack space) — risk of **stack overflow** if recursion is too deep.
* Often slower due to overhead of function calls.
* Iterative solutions may be more efficient in some cases.
* Python has a recursion depth limit (`sys.getrecursionlimit()`), usually around 1000.

---

### **Tips for Writing Recursive Functions**

* Always define a clear base case to avoid infinite recursion.
* Test with simple inputs to ensure base case triggers correctly.
* Consider memoization or dynamic programming to optimize overlapping subproblems.
* Use recursion only when it makes the problem easier to solve or understand.

---
