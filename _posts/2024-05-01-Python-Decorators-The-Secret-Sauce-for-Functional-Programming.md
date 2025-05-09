---
layout: post
title:  Python Decorators - The Secret Sauce for Functional Programming
date: 2024-05-01 10:00
categories: [Python Tutorial]
tags: [python, tutorial]
---


## What are Names in Python?

In Python, names serve as identifiers referencing various objects such as variables, functions, classes, modules, or other entities within the codebase. They function as labels facilitating the referencing and manipulation of data or code elements, thereby enhancing the readability and manageability of programs.


GitHub Repo : **[Python Decorators](https://github.com/ahammadnafiz/Python-UIU/tree/main/Decorators%20In%20Python)**


![Python Decorators](assets/Posts/Mastering Decorators in Python.png)
_Python Decorators_

### Assigning Names

```python
# Assigning a Name to a Variable
x = 10

# Assigning a Name to a Function
def greet(name):
   print("Hello, " + name + "!")
```

Here, `x` is a name assigned to an integer object (`10`), and `greet` is a name assigned to a function object.

Python associates each name with a unique object, and you can check the identity (memory address) of an object using the `id()` function:

```python
# Demonstrating Identity
print(id(x))  # Identity of x
print(id(10)) # Identity of integer 10
```

## What are Namespaces in Python?

Namespaces in Python constitute a systematic framework for organizing and governing identifiers such as variable names, function names, class names, etc. They play a pivotal role in mitigating naming conflicts and furnishing a structured means of accessing distinct elements within the codebase.

Python has four types of namespaces:

1. **Built-in Namespace**: This namespace encompasses all predefined functions, exceptions, and constants furnished by Python. These entities can be directly utilized without necessitating any import statements.

    ```python
    print(len("Hello"))  # Demonstrating the usage of the built-in function 'len'
    print(ValueError)    # Demonstrating the usage of the built-in exception 'ValueError'
    print(True)          # Demonstrating the usage of the built-in constant 'True'
    ```

2. **Module-Level/Global Namespace**: The global namespace pertains to the outermost scope of a program, housing all built-in objects, functions, and variables pre-defined in Python. It also encompasses any variables or functions defined at the top level of a script or module. Objects within the global namespace are accessible throughout the entirety of the program.

    ```python
    # Global Variable
    x = 10

    def my_func():
       print(x)  # Accessing the global variable x

    my_func()  # Output: 10
    print(x)   # Output: 10
    ```

3. **Local Namespace**: A local namespace denotes the scope confined within a function or a class. It encompasses the names of variables and objects specifically defined within the confines of that particular function or class. These names are exclusively accessible from within the local scope and remain concealed from external visibility.

    ```python
    a = 10

    def func_1():
       a = 20
       print(dir())  # Printing the directory of the local namespace, displaying only 'a'

    def func_2():
       a = 30

    print(dir())  # Printing the directory of the global namespace/module level, encompassing built-in modules, variable a, and functions func_1, func_2
    func_1()
    ```

4. **Enclosed Namespace**: The enclosed namespace denotes the scope situated between the local and global namespaces. It comes into existence when a nested function is defined within another function. The nested function possesses access to variables from the enclosing function's scope, alongside its own local namespace and the global namespace.

    ```python
    # Global Variable
    x = 'global'

    def outer_func():
       # Enclosed Variable
       y = 'enclosed'

       def inner_func():
           # Local Variable
           z = 'local'
           print(x)  # Accessing the global variable
           print(y)  # Accessing the enclosed variable
           print(z)  # Accessing the local variable

       inner_func()

    outer_func()
    ```

Python follows the **LEGB** rule to resolve names:

- **L**ocal: Python first checks if the name is defined in the current part of the code you're working on.
- **E**nclosed: If Python doesn't find the name locally, it looks in the functions that contain the current part of the code.
- **G**lobal: If it's still not found, Python looks at the entire file to see if the name is defined outside of any functions.
- **B**uilt-in: If Python can't find the name anywhere in your code, it checks if it's a built-in name that's always available.

```python
# Global scope
x = 10  # global variable

def outer_func():
    # Enclosing scope
    x = 20  # nonlocal/Enclosed variable
    
    def inner_func():
        # Local scope
        x = 30  # local variable
        print(x)
    
    inner_func()
    print(x)

outer_func()
print(x)
```

In this example, the output will be:

```
30
20
10
```


## Understanding Closures in Python

In Python, functions are first-class objects, which means they can be assigned to variables, passed as arguments to other functions, and even returned from functions. This ability to treat functions as objects opens up a world of possibilities, including the creation of closures.

### Functions as Objects

Before diving into closures, let's understand how functions can be treated as objects in Python:

```python
def outer():
    print('Hello')

print(outer)  # <function outer at 0x7f9b7c6a4dc0>
print(type(outer))  # <class 'function'>
```

In the above example, we define a function `outer()` and then print the function itself using `print(outer)`. The output shows the memory address of the function object. We can also check the type of the function using `type(outer)`, which confirms that it is indeed a `function` object.

### Nested Functions

Python allows you to define functions inside other functions, which are called nested functions:

```python
def outer():
    print('Outer')
    def inner():
        print('Inner')
    inner()

outer()
```

In this example, we define an `inner()` function inside the `outer()` function. When we call `outer()`, it prints 'Outer' and then calls the `inner()` function, which prints 'Inner'.

### Aliasing Functions

Just like variables, you can create aliases (or references) for functions:

```python
def outer():
    print('Hello')

new = outer  # Aliasing outer function
new()  # Hello
outer()  # Hello
```

Here, we create an alias `new` for the `outer` function. Calling `new()` or `outer()` will both execute the same function and print 'Hello'.

### Closures in Python

A closure is a nested function that has access to variables in the outer (enclosing) function's scope, even after the outer function has finished executing. The nested function "closes over" the variables from the outer function, allowing it to remember and use those variables even after the outer function has completed.

```python
def outer():
    def inner():
        x = 100
        return x
    return inner()

print(outer())  # 100
```

In this example, the `inner()` function is a nested function inside `outer()`. When we call `outer()`, it returns the result of `inner()`, which is `100`. However, this is not a closure because the `x` variable is local to the `inner()` function and doesn't reference any variables from the outer function's scope.

To create a closure, we need to have a nested function that references variables from the outer function's scope:

```python
def outer():
    x = 100
    def inner():
        return x
    return inner  # returning inner function object

inner = outer()  # The outer function returns the inner function object, and we assign it to inner
print(inner())  # 100
```

In this example, the `inner()` function references the `x` variable from the `outer()` function's scope. When we call `outer()`, it returns the `inner()` function object itself, which we then assign to the `inner` variable. When we call `inner()`, it has access to the `x` variable from the `outer()` function's scope, even though `outer()` has already finished executing.

The key points to remember about closures are:

1. A closure is a nested function that has access to variables in the outer (enclosing) function's scope, even after the outer function has finished executing.
2. The nested function "closes over" the variables from the outer function, allowing it to remember and use those variables even after the outer function has completed.
3. Closures are created when a nested function references variables from the outer function's scope.
4. Closures can be used to create private variables and encapsulate data.

Closures are a powerful concept in Python and have many practical applications, such as implementing decorators, creating private variables, and implementing functional programming patterns like currying.


## Understanding Python Decorators: A Detailed Explanation

Python decorators are sophisticated constructs that allow for dynamic alteration of function behavior without altering the original function implementation. They provide a means to wrap or augment a function with additional features.

Let's delve into decorators step by step, elucidating through examples and detailed explanations.

### What is a Decorator?

In Python, a decorator is a function that accepts another function as input, augments it with additional behavior, and then returns the modified function. This capability empowers developers to enhance or modify the functionality of functions or methods.

Consider this fundamental example of a decorator:

```python
def decorator(func):
    def inner():
        func()  # Execute original function
        print('Ahammad Nafiz')  # Additional functionality
    return inner

@decorator
def welcome():
    print('Hello')

welcome()  # Output: Hello\nAhammad Nafiz
```

Here's a breakdown:
- `decorator` is a function that takes `func` as an argument.
- Within `decorator`, `inner` is defined to wrap around `func`, adding extra functionality (like printing 'Ahammad Nafiz' after calling `func`).
- The `@decorator` syntax above `welcome` is a shorthand to apply the decorator to the `welcome` function.

### How Decorators Work

Visualize the process of applying a decorator to a function:

```text
def func():
    ---> func()

@decorator
def func():
    ---> func(func())
                |
                ---> original func
```

The `@decorator` syntax effectively replaces `func` with the result of calling `decorator(func)`. This implies that `func` now points to its decorated version.

### Example: Adding New Functionality

Let's explore a scenario where a decorator calculates the duration of a function's execution:

```python
import time

def duration_decorator(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"Duration: {end-start} seconds")
        return result
    return wrapper

@duration_decorator
def my_function(n):
    L = [i for i in range(n)]

my_function(100000)
```

In this case:
- `duration_decorator` measures a function's execution time.
- `@duration_decorator` is utilized to apply this decorator to `my_function`.
- Upon calling `my_function(100000)`, the `duration_decorator` wraps around `my_function`, gauges its execution time, and displays the duration.

### Chaining Decorators

Multiple decorators can be chained together:

```python
def double_decorator(func):
    def wrapper(*args, **kwargs):
        func(*args, **kwargs)
        func(*args, **kwargs)
    return wrapper

@double_decorator
@duration_decorator
def another_function(n):
    L = [i for i in range(n)]

another_function(100000)
```

Here, `@double_decorator` encapsulates the outcome of `@duration_decorator(another_function)`, effectively invoking `another_function` twice and gauging its duration.

### Employing Decorators with Classes

Decorators can operate within classes, exemplified by the `@property` decorator:

```python
class MyClass:
    def __init__(self):
        self._x = 0
    
    @property
    def x(self):
        return self._x
    
    @x.setter
    def x(self, value):
        self._x = value

obj = MyClass()
obj.x = 5
print(obj.x)  # Output: 5
```

In this instance, `@property` facilitates defining `x` as a property of `MyClass`, supporting getter, setter, and deleter methods.

## Exploring Decorators with Comprehensive Examples

Decorators are potent features in Python, fostering augmentation or extension of function or method behavior. They offer a succinct and elegant approach for integrating functionality sans altering the original function's code. Let's explore decorators further through extensive examples.

### Example: Timing Execution with a Decorator

Design a decorator to measure a function's execution time:

```python
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"Execution time: {end_time - start_time} seconds")
        return result
    return wrapper

@timer
def heavy_computation(n):
    result = sum(i for i in range(n))
    return result

print(heavy_computation(1000000))
```

Output:
```
Execution time: 0.05608105659484863 seconds
499999500000
```

In this example:
- `timer` measures a function's execution time.
- `@timer` is employed to implement this decorator with the `heavy_computation` function.
- On invoking `heavy_computation(1000000)`, the `timer` decorator encapsulates it, gauges its execution time, and shows the duration.

### Example: Memoization with a Decorator

Memoization, a technique to cache outcomes of resource-intensive function calls for subsequent reuse, can be implemented using a decorator:

```python
def memoize(func):
    cache = {}

    def wrapper(*args):
        if args not in cache:
            cache[args] = func(*args)
        return cache[args]

    return wrapper

@memoize
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))  # Output: 55
```

In this example:
- `memoize` caches `fibonacci` function results using a dictionary (`cache`).
- `@memoize` is applied as a decorator to the `fibonacci` function.
- On invoking `fibonacci(10)`, the decorator examines if the result for `n=10` is in the cache; if absent, it recursively computes the result and stores it in the cache.

### Example: Logging with a Decorator

Decorators can log details concerning function calls:

```python
def log(func):
    def wrapper(*args, **kwargs):
        print(f"Calling function: {func.__name__} with args: {args}, kwargs: {kwargs}")
        result = func(*args, **kwargs)
        print(f"Function {func.__name__} returned: {result}")
        return result
    return wrapper

@log
def add(x, y):
    return x + y

print(add(3, 5))  # Output:
```

Output:
```
Calling function: add with args: (3, 5), kwargs: {}
Function add returned: 8
8
```

In this example:
- `log` logs function call specifics.
- `@log` applies this decorator to the `add` function.
- On calling `add(3, 5)`, the `log` decorator records details pre and post `add` invocation, encompassing arguments and return value.

### Example: Debugging with a Decorator

Let's explore a debugging scenario using a decorator that logs details about function calls:

```python
def debug(func):
    def wrapper(*args, **kwargs):
        args_value = ', '.join(str(arg) for arg in args)
        kwargs_value = ', '.join(f"{k} = {v}" for k, v in kwargs.items())
        print(f"Calling: {func.__name__} with args: {args_value} and kwargs: {kwargs_value}")
        return func(*args, **kwargs)
    return wrapper

@debug
def greet(name, greeting='Hello'):
    return f"{greeting}, {name}"

greet('Nafiz', greeting='How are you?')
```

Output:
```
Calling: greet with args: Nafiz and kwargs: greeting = How are you?
```

In this example:
- `debug` is a decorator that logs information about function calls.
- `@debug` is used to apply this decorator to the `greet` function.
- Upon calling `greet('Nafiz', greeting='How are you?')`, the `debug` decorator intercepts the call, constructs a formatted string displaying the function name, arguments (`args`), and keyword arguments (`kwargs`), and then invokes the original `greet` function.


### Conclusion

Decorators are a versatile Python tool for broadening function or method behavior. They're adept at tasks like timing, caching, logging, authentication, and more. Comprehending decorators is paramount for crafting modular, reusable, and

 maintainable code.

Experiment with decorators to realize their full potential and leverage their prowess in Python projects!