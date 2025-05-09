---
layout: post
title:  Mastering Python Generators - A Comprehensive Guide with Examples
date: 2024-04-26 10:00
categories: [Python Tutorial]
tags: [python, tutorial]
---


Generators are a powerful feature in Python that allow you to create iterators in a simple and memory-efficient way. In this comprehensive tutorial, we'll dive deep into the world of generators, exploring their inner workings, use cases, and best practices with numerous examples and step-by-step code explanations.

GitHub Repo : **[Python Generators](https://github.com/ahammadnafiz/Python-UIU/blob/main/Generators_in_Python/generator.py)**


![Mastering Python Generators](assets/Posts/Mastering Generators in Python.png)
_Mastering Python Generators_


## What is a Generator?

A generator is a special type of function that returns an iterator. Unlike regular functions that use the `return` statement to return a value and terminate, generators use the `yield` keyword to produce a sequence of values, one at a time, and maintain their state between successive calls.

Here's a simple example to illustrate the concept:

```python
def gen_demo():
    yield "first statement"
    yield "second statement"
    yield "third statement"

gen = gen_demo()

print(next(gen))  # Output: first statement
print(next(gen))  # Output: second statement
print(next(gen))  # Output: third statement
```

In the above example, `gen_demo` is a generator function that yields three strings. When we call `gen_demo()`, it returns a generator object `gen`. We can then use the `next()` function to retrieve the next value yielded by the generator.

**Step-by-Step Explanation:**

1. **Function Definition**: We define the `gen_demo()` function using the `def` keyword. This function is a generator, which means it will produce a sequence of values one at a time.

2. **Using `yield`**: Inside `gen_demo()`, instead of using `return` to send back a single result, we use the `yield` keyword. `yield` allows the function to return a value while saving its state so that it can resume from where it left off when called again.

3. **Creating the Generator**: We call `gen_demo()` and assign the resulting generator object to the variable `gen`. This does not immediately execute the function; it just prepares it for later use.

4. **Retrieving Values with `next()`**: We use the `next(gen)` function to retrieve the next value yielded by the generator `gen`.

5. **First `next()` Call**: When `next(gen)` is first called, it starts executing `gen_demo()`. The function runs until it reaches the first `yield` statement and returns "first statement".

6. **Subsequent `next()` Calls**: Each subsequent call to `next(gen)` causes the function to resume execution from where it was paused by the last `yield` statement. It continues until it encounters the next `yield` statement, returning the next value in the sequence.

7. **Sequence of Execution**: 
   - First call: Executes until the first `yield`, returning "first statement".
   - Second call: Resumes from where it left off, executes until the next `yield`, returning "second statement".
   - Third call: Again resumes from where it paused, executes until the next `yield`, returning "third statement".


## The Need for Generators

Before diving into the intricacies of generators, let's understand why we need them in the first place. Consider the following example:

```python
L = [x for x in range(100000)]

import sys
print(sys.getsizeof(L))  # Output: 824456

x = range(10000000)
print(sys.getsizeof(x))  # Output: 48
```

In the first case, we create a list `L` with 100,000 elements. This operation allocates memory for the entire list, resulting in a sizeable memory footprint of 824,456 bytes. In contrast, the `range` object in the second case doesn't actually store all the values in memory; instead, it generates them on-the-fly as needed, occupying only 48 bytes.

This example highlights the memory efficiency of generators, which becomes increasingly important when dealing with large datasets or infinite streams of data.

## Generator Functions vs Regular Functions

While regular functions use the `return` statement to return a value and terminate, generator functions use the `yield` keyword to produce a sequence of values, one at a time, and maintain their state between successive calls.

To better understand the difference between `yield` and `return`, let's use the Python Tutor visualization tool:

```python
def regular_function():
    result = []
    for i in range(3):
        result.append(i)
    return result

def generator_function():
    for i in range(3):
        yield i
```

In the regular function, the entire list `[0, 1, 2]` is created and returned, while in the generator function, values are yielded one by one, preserving the state of the function between iterations.

**Step-by-Step Explanation:**


1. **Definition of `regular_function()`**:
   - The `regular_function()` is defined using the `def` keyword.
   - Inside the function, an empty list named `result` is created.

2. **Appending Values to `result`**:
   - A `for` loop is used to iterate from 0 to 2 (inclusive).
   - During each iteration, the current value (0, 1, or 2) is appended to the `result` list.

3. **Return the Resulting List**:
   - Once the loop finishes, the function returns the `result` list containing `[0, 1, 2]`.

4. **Definition of `generator_function()`**:
   - The `generator_function()` is also defined using the `def` keyword.

5. **Yielding Values**:
   - Inside this function, a `for` loop is used to iterate from 0 to 2 (inclusive).
   - Instead of appending values to a list, each value (0, 1, 2) is yielded using the `yield` keyword during each iteration.

6. **State Maintenance with `yield`**:
   - The `yield` keyword allows the function's state to be preserved between successive iterations of the loop.
   - After yielding a value, the function is paused until the next iteration, retaining its current state (e.g., the loop variable's value and other local variables).

In summary:
- `regular_function()` creates a list and populates it with values using a loop, then returns the complete list.
- `generator_function()` yields values one by one during each iteration of a loop, maintaining its execution state between each `yield` statement. This function can be used as a generator to produce values lazily without generating the entire sequence upfront.

## Creating Generators

There are several ways to create generators in Python:

1. **Generator Functions**: As shown earlier, you can define a generator function using the `yield` keyword.

    ```python
    def square(num):
        for i in range(1, num+1):
            yield i**2
    ```

    In this example, the `square` function is a generator function that yields the squares of numbers from 1 to `num`.

**Step-by-Step Explanation:**


1. **Definition of `square(num)` Function**:
   - The `square(num)` function is defined using the `def` keyword, with `num` as a parameter representing the maximum value for iteration.

2. **Iterating with a `for` Loop**:
   - Inside the function, a `for` loop is used to iterate from 1 to `num` (inclusive). This loop will run for each integer value from 1 up to and including `num`.

3. **Using `yield` to Produce Squares**:
   - During each iteration of the loop, the `yield` keyword is used to produce the square of the current value (`i`).
   - For example, if the loop is currently at `i`, `yield i * i` will produce the square of `i`.

4. **State Maintenance with `yield`**:
   - The `yield` keyword allows the function's state to be preserved between successive iterations of the loop.
   - After yielding a value (in this case, the square of `i`), the function is paused until the next iteration, retaining its current state (such as the loop variable's value and other local variables).

In summary, the `square(num)` function generates and yields the square of each integer from 1 up to `num` lazily, one value at a time. This makes `square(num)` a generator function, allowing you to iterate over the squares of numbers without having to compute and store all of them in memory at once. You can use this function in a loop or with other generator functions to process the yielded values as needed.

To use this generator function, you can create a generator object and iterate over it:

```python
gen = square(10)
for i in gen:
    print(i)
```

This will print the squares of numbers from 1 to 10:

```
    1
    4
    9
    16
    25
    36
    49
    64
    81
    100
```


2. **Generator Expressions**: Similar to list comprehensions, generator expressions provide a concise way to create generators. Here's an example:

    ```python
    gen = (i**2 for i in range(1, 101))
    for i in gen:
        print(i)
    ```

    This will print the squares of numbers from 1 to 100.

    **Step-by-Step Explanation:**


1. **Generator Expression Creation**:
   - The generator expression `(i**2 for i in range(1, 101))` is used to create a generator object named `gen`.
   - This expression defines a sequence where each value is the square of `i` for `i` in the range `1` to `100` (inclusive).

2. **Evaluation of `i**2` for Each `i`**:
   - As the generator is iterated over, the expression `i**2` is evaluated for each value of `i` in the range `1` to `100`.
   - This means that `i**2` computes the square of each number in the specified range.

3. **On-the-Fly Value Production**:
   - Unlike list comprehensions that eagerly create a list of all values, the generator expression produces values on-the-fly as they are needed.
   - This lazy evaluation is a key feature of generator expressions. It conserves memory by generating values only when requested, rather than storing them all at once in memory.

4. **Iteration with a `for` Loop**:
   - A `for` loop is used to iterate over the generator object `gen`.
   - During each iteration, the loop retrieves the next value (the square of the current number) from the generator and prints it.
   - The loop continues until all values in the generator have been exhausted.

In summary, the generator expression `(i**2 for i in range(1, 101))` efficiently computes and yields the square of each number from 1 to 100, producing values as needed without precomputing and storing them in memory. This approach is suitable for scenarios where memory conservation and lazy evaluation are important considerations.

3. **Iterating over Generators**: You can create a generator by iterating over another generator or an iterable object. For example:

    ```python
    import os
    import cv2

    def image_data_reader(folder_path):
        for file in os.listdir(folder_path):
            f_array = cv2.imread(os.path.join(folder_path, file))
            yield f_array
    ```

    This generator function reads image files from a specified folder path and yields their numpy arrays one by one, allowing you to process large datasets without loading them entirely into memory.

    **Step-by-Step Explanation:**

    1. The `image_data_reader(folder_path)` function is defined with the `def` keyword, taking a `folder_path` parameter.
    2. Inside the function, a `for` loop iterates over the list of files in the `folder_path` directory, obtained using `os.listdir(folder_path)`.
    3. For each file, the `cv2.imread()` function from the OpenCV library is used to read the image file and store its numpy array representation in the `f_array` variable.
    4. The `yield` keyword is used to produce the `f_array` value, allowing the function to generate image arrays one by one, without loading all of them into memory at once.

To use the `image_data_reader` generator function, you can iterate over the generator object it returns. Here's an example of how you can do this:

```python
import os
import cv2

def image_data_reader(folder_path):
    for file in os.listdir(folder_path):
        f_array = cv2.imread(os.path.join(folder_path, file))
        yield f_array

# Specify the folder path containing the image files
folder_path = "path/to/image/folder"

# Create a generator object
image_generator = image_data_reader(folder_path)

# Iterate over the generator to process each image array
for image_array in image_generator:
    # Perform operations on the image array
    # For example, display the image
    cv2.imshow("Image", image_array)
    cv2.waitKey(0)
    cv2.destroyAllWindows()
```

Here's a step-by-step explanation of how to use the generator:

1. You call the `image_data_reader` function with the `folder_path` argument, which creates a generator object.
2. The generator object is assigned to the `image_generator` variable.
3. You can then iterate over the `image_generator` using a `for` loop.
4. Inside the loop, each iteration yields the next image array (`image_array`) from the generator.
5. Within the loop, you can perform operations on the `image_array`, such as displaying the image using OpenCV's `cv2.imshow()` function.

By using a generator, you can process large datasets of image files without loading all of them into memory at once, which can be more memory-efficient, especially when dealing with large datasets or limited system resources.

Note: Make sure to replace `"path/to/image/folder"` with the actual path to the folder containing your image files.


## Benefits of Using Generators

Using generators in Python offers several benefits:

1. **Memory Efficiency**: As demonstrated earlier, generators don't store the entire sequence in memory, making them more memory-efficient, especially when dealing with large datasets or infinite streams of data.

2. **Representing Infinite Streams**: Generators can represent infinite streams of data, as they produce values on-the-fly. For example:

    ```python
    def all_even():
        n = 0
        while True:
            yield n
            n += 2
    ```

    This generator function produces an infinite stream of even numbers.

    **Step-by-Step Explanation:**

    1. The `all_even()` function is defined with the `def` keyword.
    2. Inside the function, the variable `n` is initialized to 0.
    3. An infinite `while True` loop is used to generate even numbers indefinitely.
    4. Inside the loop, the current value of `n` is yielded using the `yield` keyword.
    5. The value of `n` is incremented by 2 to generate the next even number.
    6. The loop continues indefinitely, generating and yielding even numbers on-the-fly.

    To use this generator function, you can create a generator object and iterate over it (with care, as it will produce an infinite stream of values):

    ```python
    gen = all_even()
    print(next(gen))  # Output: 0
    print(next(gen))  # Output: 2
    print(next(gen))  # Output: 4
    # ... and so on
    ```

3. **Chaining Generators**: Generators can be chained together, allowing you to create complex data pipelines. For example:

    ```python
    def fibonacci_numbers(nums):
        x, y = 0, 1
        for _ in range(nums):
            x, y = y, x+y
            yield x

    def square(nums):
        for num in nums:
            yield num**2

    print(sum(square(fibonacci_numbers(10))))  # Output: 4895
    ```

    In this example, the `fibonacci_numbers` generator produces the first 10 Fibonacci numbers, which are then squared by the `square` generator, and finally summed up.

    **Step-by-Step Explanation:**

    1. The `fibonacci_numbers(nums)` function is defined to generate the first `nums` Fibonacci numbers.
    2. Inside the function, `x` and `y` are initialized to 0 and 1, respectively, representing the first two Fibonacci numbers.
    3. A `for` loop iterates `nums` times, generating the next Fibonacci number by swapping the values of `x` and `y` and adding them (`x, y = y, x+y`).
    4. The current Fibonacci number (`x`) is yielded using the `yield` keyword.
    5. The `square(nums)` function is defined to take an iterable `nums` and yield the square of each number.
    6. Inside the `square` function, a `for` loop iterates over the elements in `nums`.
    7. For each element `num`, the square `num**2` is yielded using the `yield` keyword.
    8. The `sum(square(fibonacci_numbers(10)))` expression creates a generator `fibonacci_numbers(10)` that generates the first 10 Fibonacci numbers.
    9. The `square` generator takes the `fibonacci_numbers(10)` generator as input and squares each Fibonacci number.
    10. The `sum` function consumes the squared Fibonacci numbers from the `square` generator and calculates their sum, which is printed as the output (4895).

4. **Ease of Implementation**: Generators are relatively easy to implement compared to creating custom iterator classes.

5. **Representing Ranges and Sequences**: Generators can be used to represent ranges and sequences in a memory-efficient way. For example:

    ```python
    def mera_range(start, end):
        for i in range(start, end):
            yield i
    ```

    This generator function behaves like the built-in `range` function but uses a generator to produce values on-the-fly.

    **Step-by-Step Explanation:**

    1. The `mera_range(start, end)` function is defined with the `def` keyword, taking `start` and `end` parameters.
    2. Inside the function, a `for` loop iterates from `start` to `end-1` using the built-in `range` function.
    3. For each iteration, the current value `i` is yielded using the `yield` keyword.

    To use this generator function, you can create a generator object and iterate over it:

    ```python
    for i in mera_range(15, 26):
        print(i)
    ```

    This will print the numbers from 15 to 25 (inclusive):

    ```
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    ```

## Advanced Topics

While the basics of generators are relatively straightforward, there are some advanced topics worth exploring:

1. **Generator Delegation**: Generators can delegate part of their operation to a different generator, allowing for more modular and reusable code.

    ```python
    def gen_range(start, end):
        while start < end:
            yield start
            start += 1

    def gen_delegated(start, end, step):
        for i in gen_range(start, end):
            if i % step == 0:
                yield i
    ```

    In this example, the `gen_delegated` generator delegates the task of generating numbers to the `gen_range` generator and filters out values that are not divisible by the `step` value.

2. **Generator Pipelines**: By chaining multiple generators together, you can create powerful data processing pipelines, enabling efficient data transformations and filtering.

    ```python
    def integers():
        i = 0
        while True:
            yield i
            i += 1

    def squares(nums):
        for n in nums:
            yield n ** 2

    def odds(nums):
        for n in nums:
            if n % 2 != 0:
                yield n

    # Pipeline: Integers -> Squares -> Odds
    pipeline = odds(squares(integers()))

    for i in pipeline:
        if i > 100:
            break
        print(i)
    ```

    In this example, we create a pipeline that generates integers, squares them, and filters out the even numbers. The pipeline is constructed by chaining the `odds`, `squares`, and `integers` generators together.

3. **Coroutines and Async Generators**: Python's coroutines and async generators provide a way to write concurrent code using generators, making it easier to manage and reason about asynchronous operations.

4. **Generator-based Algorithms**: Many algorithms, such as graph traversal algorithms (e.g., breadth-first search, depth-first search), can be elegantly implemented using generators.

    ```python
    def bfs(graph, start):
        visited, queue = set(), [start]
        while queue:
            vertex = queue.pop(0)
            if vertex not in visited:
                visited.add(vertex)
                yield vertex
                queue.extend(graph[vertex] - visited)
    ```

    This generator function implements the breadth-first search (BFS) algorithm for traversing a graph, yielding each visited vertex one by one.

## Conclusion

Python generators are a powerful and versatile tool that offer memory efficiency, ease of implementation, and the ability to represent infinite streams of data. By understanding and leveraging generators, you can write more efficient and elegant code, especially when dealing with large datasets or infinite data streams.

Throughout this tutorial, we've covered the fundamental concepts of generators, their creation methods, benefits, and advanced topics with numerous examples and step-by-step code explanations. With the knowledge gained from this tutorial, you should now be well-equipped to incorporate generators into your Python projects and unlock their full potential.
