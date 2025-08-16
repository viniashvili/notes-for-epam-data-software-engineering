# Python Core

## *Lambda Functions in Python*

* **Definition:** Anonymous (unnamed) functions defined using the `lambda` keyword.
* **Syntax:**

  ```python
  lambda arguments: expression
  ```

  * Can take **any number of arguments** but only **one expression**.
  * Always returns the value of that expression.
* **When to use:**

  * Short, throwaway functions.
  * As arguments to higher-order functions (e.g., `map()`, `filter()`, `sorted()`).
* **Example:**

  ```python
  square = lambda x: x ** 2
  print(square(5))  # 25
  ```

---

## **`map()`**

* **Definition:** Applies a function to **every item** in an iterable and returns a `map` object (iterator).
* **Syntax:**

  ```python
  map(function, iterable)
  ```
* **Example:**

  ```python
  nums = [1, 2, 3, 4]
  doubled = map(lambda x: x * 2, nums)
  print(list(doubled))  # [2, 4, 6, 8]
  ```
* **Key points:**

  * `map()` is lazy — you need to convert to `list()` or iterate to get results.
  * Good for transforming data.

---

## **`filter()`**

* **Definition:** Filters items from an iterable **based on a function** that returns `True` or `False`.
* **Syntax:**

  ```python
  filter(function, iterable)
  ```
* **Example:**

  ```python
  nums = [1, 2, 3, 4, 5]
  even = filter(lambda x: x % 2 == 0, nums)
  print(list(even))  # [2, 4]
  ```
* **Key points:**

  * Only keeps elements where the function returns `True`.
  * Function must return a boolean.

---

## *Recursion in Python*

**Definition:**
Recursion is when a function calls itself directly or indirectly to solve a problem by breaking it into smaller subproblems.
It requires **a base case** (stopping condition) and **a recursive case** (the part where the function calls itself).

**Structure:**

```python
def recursive_function(parameters):
    if base_condition:     # Base case – stop recursion
        return result
    else:                  # Recursive case – break problem down
        return recursive_function(modified_parameters)
```

---

### **Example**

Factorial calculation:

```python
def factorial(n):
    if n == 0:  # Base case
        return 1
    return n * factorial(n - 1)  # Recursive case

print(factorial(5))  # 120
```

Explanation:

* **Base case:** `n == 0` stops recursion.
* **Recursive case:** `n * factorial(n-1)` keeps breaking the problem into smaller pieces.

---

### **Advantages / Pros**

1. **Clean and readable** for problems that are naturally recursive
   (e.g., tree/graph traversal, divide-and-conquer algorithms like quicksort).
2. **Reduces code size** — complex logic can be expressed in fewer lines.
3. **Good for hierarchical data processing** (e.g., XML/JSON parsing, file system traversal).

---

### **Drawbacks / Cons**

1. **Higher memory usage** — each function call adds a new frame to the call stack.
2. **Risk of stack overflow** if recursion depth is too large.
3. **Usually slower** than iterative solutions due to function call overhead.
4. **Harder to debug** — tracing recursive calls can get confusing.

---

## *Namespaces in Python*

**Definition:**
A namespace in Python is a mapping between names (identifiers) and the objects they refer to. Namespaces prevent naming conflicts by isolating variable names.

---

### **Types of Namespaces**

1. **Built-in Namespace**

   * Contains names that are preloaded by Python.
   * Available everywhere in the code without importing.
   * Examples: `len`, `print`, `range`, `Exception`.
   * Created when the Python interpreter starts.

2. **Global Namespace**

   * Contains names defined at the top level of a module or script.
   * Created when the module is loaded.
   * Accessible from anywhere in the module but not from other modules unless imported.
   * Example:

     ```python
     x = 10  # global namespace
     ```

3. **Enclosed Namespace** (also called **Nonlocal**)

   * Exists in nested functions, in the outer function's scope.
   * Used when an inner function refers to variables from its enclosing function.
   * Example:

     ```python
     def outer():
         y = 20  # enclosed namespace
         def inner():
             print(y)
         inner()
     ```

4. **Local Namespace**

   * Contains names defined inside a function (including parameters).
   * Created when the function is called and destroyed when the function returns.
   * Example:

     ```python
     def func():
         z = 30  # local namespace
         print(z)
     ```

---

### **LEGB Rule**

Order in which Python looks for a name:

1. **Local** – Names inside the current function.
2. **Enclosed** – Names in the enclosing (outer) function scope.
3. **Global** – Names at the module level.
4. **Built-in** – Names in Python’s built-in scope.

**Example:**

```python
x = "global"

def outer():
    x = "enclosed"
    def inner():
        x = "local"
        print(x)
    inner()

outer()  # Output: local
```

Python resolves `x` in **Local → Enclosed → Global → Built-in** order.

---

## *Scopes in Python*

**Definition:**
A **scope** is the textual region of code where a name is visible (can be referenced without qualification). Scope controls **name lookup**—i.e., where Python searches for a name at runtime.

**Main scopes:**

* **Local (L):** Inside the current function (including parameters and comprehension inner scope).
* **Enclosing (E):** Any outer function scopes in nested functions.
* **Global (G):** The module (file) level.
* **Built-in (B):** The `builtins` module (e.g., `len`, `print`).

Python resolves names using the **LEGB** rule: Local → Enclosing → Global → Built-in.

**Notes:**

* Python has **no block scope** for `if/for/while/try` blocks—names defined there leak into the function/module scope.
* **Comprehensions** (list/dict/set/gen) have their **own inner local scope** in Python 3, so loop variables in a comprehension do **not** leak.

---

## **Namespaces vs Scopes**

| Concept       | What it is                                   | Example / Access                                    |
| ------------- | -------------------------------------------- | --------------------------------------------------- |
| **Namespace** | A **mapping** from names to objects          | `globals()`, `locals()`, `obj.__dict__`, `vars(x)`  |
| **Scope**     | A **region of code** where a name is visible | Function body (local), module (global), nested func |

* A **namespace** is *data* (a dict-like container of names → objects).
* A **scope** is *where* Python looks for names (which namespaces, and in what order).
* A **scope determines which namespaces are searched** (LEGB).

---

## **Namespace Dictionaries**

* **Module/global namespace:** `globals()` → dict of names at module level.
* **Local namespace:** `locals()` → dict of names in the current local scope.

  * At function scope, it’s a **snapshot**; writing to `locals()` **does not** reliably change locals.
  * At module scope or interactive shell, `locals()` is the same object as `globals()`.
* **Built-ins:** `import builtins; builtins.__dict__`
* **Objects/classes/modules:** `obj.__dict__` (writable for most user-defined objects); `vars(obj)` is a readable alias that calls `obj.__dict__` when available.
* **Class namespace:** Created by executing the class body; accessible via `ClassName.__dict__` (mappingproxy).

---

## **Code Examples**

### 1) LEGB resolution

```python
x = "global-x"

def outer():
    x = "enclosed-x"
    def inner():
        x = "local-x"
        print(x)  # local
    inner()
    print(x)      # enclosed

outer()
print(x)          # global
```

### 2) `global` and `nonlocal`

```python
counter = 0  # global

def bump_global():
    global counter
    counter += 1  # writes to module-level 'counter'

def make_counter():
    count = 0  # enclosed
    def inc():
        nonlocal count
        count += 1  # writes to 'count' in the enclosing scope
        return count
    return inc

bump_global()
c = make_counter()
print(counter)  # 1
print(c(), c(), c())  # 1 2 3
```

### 3) No block scope (but comprehension has its own)

```python
# No block scope
for i in range(1):
    j = 42
print(j)  # 42 (leaked into the surrounding scope)

# Comprehension has its own local scope in Python 3
i = "outer"
lst = [i for i in range(3)]
print(i)  # "outer" (not overwritten by the comprehension)
```

### 4) Inspecting and mutating namespaces

```python
# Module/global namespace
x = 10
print(globals()["x"])  # 10
globals()["y"] = 20
print(y)               # 20

# Locals: snapshot in functions (don’t rely on writes)
def demo_locals():
    a = 1
    snap = locals()
    snap["a"] = 999  # unreliable at function scope
    return a, snap["a"], "a" in snap

print(demo_locals())  # (1, 999, True)  -> 'a' remains 1

# Object/class namespaces
class C:
    cls_attr = "A"
    def __init__(self):
        self.x = 5

c = C()
print(C.__dict__["cls_attr"])  # "A"
print(vars(c))                 # {'x': 5}
vars(c)["y"] = 7               # mutate instance namespace
print(c.y)                     # 7
```

### 5) Built-ins namespace

```python
import builtins

print(builtins.len([1, 2, 3]))  # 3
# Shadowing a built-in (generally bad idea)
len = lambda x: "oops"
print(len([1,2]))               # "oops"
print(builtins.len([1,2]))      # 2  (original)
del len  # clean up shadowing
```

---

## **Class Scope Special Case**

Names defined in a **class body** live in the **class namespace**, but methods **don’t** see those names via LEGB as “enclosed”. Inside methods, you must qualify with `ClassName.name` or use `self` for instance attributes.

```python
x = "global"

class D:
    x = "class-attr"
    def show(self):
        # 'x' here resolves to global unless qualified
        return x, D.x, self.__dict__

d = D()
print(d.show())  # ('global', 'class-attr', {})
```

---

## *Closures in Python*

**Definition:**
A **closure** is a function that **remembers the variables from its enclosing scope**, even after the outer function has finished executing.
It allows the inner function to access and use variables that are not in its local scope, without using `global`.

---

### **Requirements for a Closure**

1. A **nested function** (function inside another function).
2. The **inner function must reference variables** from the outer function.
3. The outer function must **return the inner function** (or pass it somewhere), so it can be used later.

---

### **Example**

```python
def outer(msg):
    def inner():
        print(msg)  # 'msg' is from outer scope
    return inner

greet = outer("Hello")
greet()  # Hello
```

* `outer` finishes execution, but `inner` still **remembers** `msg` from the `outer` scope.

---

### **Practical Example: Counter**

```python
def make_counter():
    count = 0
    def increment():
        nonlocal count  # modify enclosing variable
        count += 1
        return count
    return increment

counter1 = make_counter()
print(counter1())  # 1
print(counter1())  # 2
print(counter1())  # 3
```

* Each call to `make_counter()` creates a new closure with its **own** `count`.

---

### **Advantages**

1. Data **encapsulation** – variables are hidden from the outside.
2. Avoids using global variables.
3. Maintains state between function calls without using classes.

---

### **Drawbacks**

1. Can make debugging harder because variables are “hidden” in function scopes.
2. May cause **memory retention** if large objects are kept in the closure unintentionally.

---

## *Object-Oriented Programming (OOP) Principles in Python*

Python supports OOP, which organizes code into **objects** that bundle **data** (attributes) and **behavior** (methods).
The four main principles are **Encapsulation, Abstraction, Inheritance, and Polymorphism**.

---

### **1. Encapsulation**

* **Definition:** Bundling data and methods into a single unit (class) and restricting direct access to some of the object’s components.
* **Purpose:** Protects internal object state and ensures controlled access.
* **Implementation in Python:**

  * Public members: `self.name`
  * Protected members (by convention): `_name`
  * Private members (name mangling): `__name`
* **Example:**

```python
class Person:
    def __init__(self, name):
        self.__name = name  # private

    def get_name(self):
        return self.__name

p = Person("Alice")
print(p.get_name())  # Alice
```

---

### **2. Abstraction**

* **Definition:** Hiding internal implementation details and showing only the necessary features.
* **Purpose:** Simplifies complexity by exposing only relevant operations.
* **Implementation in Python:**

  * Use abstract base classes (`abc` module).
  * Define abstract methods with `@abstractmethod`.
* **Example:**

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, r):
        self.r = r
    def area(self):
        return 3.14 * self.r ** 2
```

---

### **3. Inheritance**

* **Definition:** Creating new classes from existing ones to reuse and extend functionality.
* **Purpose:** Promotes code reuse and establishes relationships between classes.
* **Types in Python:**

  * Single Inheritance
  * Multiple Inheritance
  * Multilevel Inheritance
  * Hierarchical Inheritance
* **Example:**

```python
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def speak(self):
        print("Bark")

d = Dog()
d.speak()  # Bark
```

---

### **4. Polymorphism**

* **Definition:** The ability to use the same method name for different types (different implementations).
* **Purpose:** Increases flexibility and code reusability.
* **Example:**

```python
class Cat:
    def speak(self):
        return "Meow"

class Dog:
    def speak(self):
        return "Bark"

def make_it_speak(animal):
    print(animal.speak())

make_it_speak(Cat())  # Meow
make_it_speak(Dog())  # Bark
```

---

### **Summary Table**

| Principle     | Purpose                            | Python Implementation                    |
| ------------- | ---------------------------------- | ---------------------------------------- |
| Encapsulation | Protect internal state             | Private/protected attrs, getters/setters |
| Abstraction   | Hide complexity, expose essentials | Abstract base classes, interfaces        |
| Inheritance   | Reuse and extend behavior          | Class inheritance                        |
| Polymorphism  | Same interface, different behavior | Method overriding, duck typing           |

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
