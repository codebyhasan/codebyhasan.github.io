---
layout: post
title:  Ultimate guide to Comprehensions in Python
date: 2024-04-18 12:56
categories: [Python Tutorial]
tags: [python, tutorial]
---
### Introduction
This blog post serves as a comprehensive guide to mastering comprehension in Python. Comprehensions are a concise and powerful feature that allows you to create lists, dictionaries and sets effortlessly. Whether you're a beginner or an experienced Python developer, this guide will help you write elegant and efficient code.


![Comprehensions in Python](assets/Posts/Ultimate Guide.png)
_Comprehensions in Python_


<div align="center">
    <h1>List Comprehension</h1>
</div>


### List Comprehensions Syntax

List comprehensions provide a concise way to create lists in Python based on an expression and an iterable. The syntax for a basic list comprehension is as follows:

- [expression for item in iterables]

In this syntax:

- `expression` represents the operation or transformation to be performed on each item in the `iterables`.
- `item` is a placeholder that represents an individual element from the `iterables`.
- `iterables` is one or more iterable objects, such as lists, tuples, or strings, from which the elements are extracted.

The list comprehension iterates over each item in the `iterables`, applies the `expression` to it, and generates a new list with the results.

Here's an example to illustrate the syntax:

```text

        my_list = [1, 2, 3, 4, 5]
        squared_list = [num**2 for num in my_list]

        In this example, the list comprehension [num**2 for num in my_list] squares each number in my_list and creates a new list squared_list containing the squared values.
```

```python
nums = [1, 2, 3, 4, 5, 6]
result = [i ** 2 for i in nums]   # Here (i ** 2) is the expression 
print(*result)  # Print the result
```

    1 4 9 16 25 36
    

### List Comprehensions with Conditional Expression

List comprehensions in Python can also include conditional expressions, allowing you to conditionally modify or filter the elements in the resulting list. The syntax for a list comprehension with a conditional expression is as follows:

- [expression if condition else alternative_expression for item in iterables]

In this syntax:

- `expression` represents the operation or transformation to be performed on each item in the `iterables` that satisfies the `condition`.
- `condition` is a condition that determines whether the `expression` or `alternative_expression` is applied to the item.
- `alternative_expression` represents an alternative operation or transformation to be performed on each item that does not satisfy the `condition`.
- `item` is a placeholder that represents an individual element from the `iterables`.

The list comprehension iterates over each item in the `iterables`, evaluates the `condition`, and applies the corresponding expression or alternative expression to generate a new list.

Here's an example to illustrate the syntax:

```text

        my_list = [1, 2, 3, 4, 5]
        result_list = [num**2 if num % 2 == 0 else num for num in my_list]

        In this example, the list comprehension [num**2 if num % 2 == 0 else num for num in my_list] squares the even numbers and keeps the odd numbers as they are, resulting in a new list result_list.
```

```python
# List Comprehensions with Conditional Expression
fruits = ['apple', 'BANANA', 'Orange', 'guava']
result = [fruit.title() if fruit.islower() else fruit + ' love' for fruit in fruits]
print(*result)
```

    Apple BANANA love Orange love Guava
    


```python
# Another example
result = [i * 5 if i == 3 else i for i in nums]  # Left side of the for (if/else) block used for decision making. If we missed else python gives us an error.                              
print(*result)
```

    1 2 15 4 5 6
    


```python
# Example of List comprehensions though dictionary 
my_list_dict = [{'name': 'nafiz', 'id': 5}, {'name': 'hasib', 'id': 4}]
result = [i['id'] for i in my_list_dict]  
print(*result)
```

    5 4
    

### List Comprehensions with Filtering

List comprehensions in Python can be used to filter elements from an iterable based on a specified condition. The syntax for a list comprehension with filtering is as follows:

- [expression for item in iterables if conditional]

In this syntax:

- `expression` represents the operation or transformation to be performed on each item in the `iterables` that satisfies the `conditional`.
- `item` is a placeholder that represents an individual element from the `iterables`.
- `iterables` is one or more iterable objects, such as lists, tuples, or strings, from which the elements are extracted.
- `conditional` is a condition that determines whether an item is included in the resulting list.

The list comprehension iterates over each item in the `iterables`, evaluates the `conditional`, and includes only the items that satisfy the condition in the resulting list.

Here's an example to illustrate the syntax:

```text

        my_list = [1, 2, 3, 4, 5]
        filtered_list = [num for num in my_list if num % 2 == 0]

      In this example, the list comprehension [num for num in my_list if num % 2 == 0] filters the even numbers from my_list and creates a new list filtered_list containing only the even numbers.
```

```python
# Example
result = [i * 5 if i == 3 else i for i in nums if i > 1] # In this List comprehensions first we filtering which element if greater than 1, after that we complete our expression for each iterations
print(*result)
```

    2 15 4 5 6
    


```python
# We can also use multiple filtering using multiple if conditionals
result = [i * 3 if i == 3 else i for i in nums if i > 1 if i < 4]
print(*result)
```

    2 9
    

### List Comprehensions with Nested Iteration and Filtering

List comprehensions in Python can incorporate nested iteration and filtering, allowing you to create combinations of elements from multiple iterables based on specified conditions. The syntax for such list comprehensions is as follows:

- [(item_1, item_2) for item_1 in iterable_1 if (condition) for item_2 in iterable_2]

In this syntax:

- `item_1` represents an individual element from `iterable_1`.
- `item_2` represents an individual element from `iterable_2`.
- `iterable_1` and `iterable_2` are two or more iterable objects, such as lists, tuples, or strings.
- `(condition)` is a condition that determines whether a combination of `item_1` and `item_2` is included in the resulting list.

The list comprehension performs nested iteration, iterating over each element in `iterable_1` and then iterating over each element in `iterable_2`. It applies the specified condition and creates combinations of `item_1` and `item_2` that satisfy the condition in the resulting list.

Here's an example to illustrate the syntax:

```text

    numbers = [1, 2, 3]
    letters = ['a', 'b', 'c']
    combinations = [(num, letter) for num in numbers if num % 2 == 0 for letter in letters]

           In this example, the list comprehension [(num, letter) for num in numbers if num % 2 == 0 for letter in letters] creates combinations of even numbers from numbers and letters from letters where the number is divisible by 2. The resulting list combinations contains tuples with the valid combinations.
```

```python
# Example
result = [(num, fruit) for num in nums if num > 1 if num < 6 for fruit in fruits]
print(result)
```

    [(2, 'apple'), (2, 'BANANA'), (2, 'Orange'), (2, 'guava'), (3, 'apple'), (3, 'BANANA'), (3, 'Orange'), (3, 'guava'), (4, 'apple'), (4, 'BANANA'), (4, 'Orange'), (4, 'guava'), (5, 'apple'), (5, 'BANANA'), (5, 'Orange'), (5, 'guava')]
    


```python
# We can visualize the above List comprehensions in normal looping way
for num in nums:
    if 1 < num:
        if num < 6:
            for fruit in fruits:
                if fruit != 'apple':
                    print((num, fruit), end=' ')

```

    (2, 'BANANA') (2, 'Orange') (2, 'guava') (3, 'BANANA') (3, 'Orange') (3, 'guava') (4, 'BANANA') (4, 'Orange') (4, 'guava') (5, 'BANANA') (5, 'Orange') (5, 'guava') 


```python
# we can add more feature in this List comprehensions
result = [(num, fruit) for num in nums if num > 1 if num < 6 for fruit in fruits if fruit != 'apple' and fruit != 'guava']
print(result)
```

    [(2, 'BANANA'), (2, 'Orange'), (3, 'BANANA'), (3, 'Orange'), (4, 'BANANA'), (4, 'Orange'), (5, 'BANANA'), (5, 'Orange')]
    

### Python - List comprehension vs map function

In Python, you have two options for applying a function to each element of an iterable: using list comprehensions or the `map` function. Let's compare the two approaches:

- **List Comprehensions**:
    - List comprehensions provide a concise way to create lists by applying an expression to each element of an iterable.
    - The syntax for a list comprehension that applies a function to an iterable is `[f(x) for x in iterable]`.
    - You can use a lambda function if you don't have a specific function to apply.
    - List comprehensions are more readable and Pythonic compared to the `map` function.
    - Example: `[x**2 for x in nums]`


The `map()` function in Python is a built-in function that takes two arguments: a function and an iterable. It applies the specified function to each element of the iterable and returns a map object, which is an iterator containing the results.

The general syntax for using the `map()` function is as follows:

                map_object = map(function, iterable)


In this syntax:

- `function` is the function to be applied to each element of the `iterable`.
- `iterable` is a sequence, such as a list, tuple, or string, that will be iterated over.

The `map()` function applies the `function` to each element of the `iterable` in a lazy and efficient manner. This means that the function is applied only when requested, and the results are generated on the fly.

##### Example: Using the `map()` Function with a Lambda Function

Here's an example that demonstrates the usage of the `map()` function with a lambda function:


                nums = [1, 2, 3, 4, 5]
                squared_nums = list(map(lambda x: x**2, nums))
                print(squared_nums)  # Output: [1, 4, 9, 16, 25]
                

In this example, the `map()` function is used to apply the lambda function `lambda x: x**2` to each element of the `nums` list. The result is a map object that contains the squared values of the numbers. By casting the map object to a list using the `list()` function, we obtain the final result `[1, 4, 9, 16, 25]`.

##### Alternative: Unpacking Values without Casting to List

Alternatively, you can use the unpacking operator `*` to obtain the values from the map object without explicitly casting it to a list. Here's an example:


                nums = [1, 2, 3, 4, 5]
                squared_nums = [*map(lambda x: x**2, nums)]
                print(squared_nums)  # Output: [1, 4, 9, 16, 25]


In this case, the `map()` function is used with the lambda function, and the resulting map object is unpacked using the `*` operator within a list context. This creates a list containing the squared values of the numbers.

It's recommended to use list comprehensions instead of the `map` function because they are more readable and aligned with Python's idiomatic style.


```python
# Examples
result = list(map(lambda i: i ** 2, nums))
print(result)
```

    [1, 4, 9, 16, 25, 36]
    


```python
# Example for passing fn in List comprehensions
def square(num):
    return num ** 2

result = [square(num) for num in nums]
print(result)
```

    [1, 4, 9, 16, 25, 36]
    


```python
numbers1 = [1, 2, 3]
numbers2 = [10, 20, 30]

result = [*map(lambda x, y: x + y, numbers1, numbers2)]
print(result)  # Output: [11, 22, 33]

#In this case, the lambda function adds corresponding elements from `numbers1` and `numbers2` to create a new list.
```

    [11, 22, 33]
    

### Taking Single Line Input and Applying Function using List Comprehension

To take a single line input and apply a function to each element using list comprehension in Python, you can follow these steps:

1. Prompt the user for input using the `input()` function.
2. Split the input line into individual elements based on a delimiter.
3. Convert the elements to the desired data type (e.g., integers or strings).
4. Apply the function `f(x)` to each element using list comprehension.
5. Optionally, store the resulting list in a variable for further use or display it.

Here's an example:

```text
1.Taking a single line input and applying a function using list comprehension

2.Prompt the user for input
    input_line = input("Enter a list of numbers separated by spaces: ")

3.Split the input line into individual elements
    elements = input_line.split()

4.Convert the elements to the desired data type
    numbers = [int(x) for x in elements]

5.Apply the function to each number using list comprehension
    result = [f(x) for x in numbers]

6.Display the resulting list
    print(result)
```

```python
user_input = [int(user) for user in input().split()]  # Here input.split() is an iterable because when we 
print(user_input[0])                                  # split it, it became a str of list so we can iterate over the input()
                                                      # Then we pass our iteration value to int() fn and make it single line input generator
```

    1 2 3
    1
    

### Taking Matrix Input using List Comprehension

To take a matrix input from the user in Python using list comprehension, you can follow these steps:

1. Use a nested list comprehension to prompt the user for the elements of each row and create the matrix.
2. Split the input line into individual elements based on a delimiter.
3. Convert the elements to the desired data type (e.g., integers) using list comprehension.
4. Create the matrix using the nested list comprehension.
5. Optionally, store the resulting matrix in a variable for further use or display it.

Here's an example:

```text

1.Create the matrix using nested list comprehension
        user_matrix = [[int(col) for col in input().split()] for row in range(3)]

2.Display the matrix
        for row in user_matrix:
           print(*row)
```

```python
user_matrix = [[int(col) for col in input().split()] for row in range(3)]
for row in user_matrix:
    print(*row)
```

    1 2 3
    4 5 6
    7 8 9
    1 2 3
    4 5 6
    7 8 9
    

## List Comprehension vs Filter in Python

### Using List Comprehension for Filtering

List comprehension provides a concise and expressive way to filter elements from an iterable based on certain conditions. The syntax for list comprehension is as follows:

- [expression for item in iterable if condition]

In this syntax, the `if` conditional part, which comes after the `for` loop, is used for filtering the elements based on the specified condition. Additionally, you can also pass a function to the `if` conditional part to perform more complex filtering operations. The updated syntax would be:

- [expression for item in iterable if fn()]

### Using the `filter()` Function

Python's `filter()` function is another way to filter elements from an iterable based on a given function. Here's an example <br>usage of the `filter()` function:

```text

- filter(fn, iterable)

         list(filter(lambda i: i > 1, map(int, [1, 2, 3])))
    
This is equivalent to the following list comprehension:
    
        [int(i) for i in [1, 2, 3] if i > 1]

Both approaches allow you to filter elements from an iterable using a specified condition or function.
```


```python
# With list comprehension
result = [i for i in nums if i > 2]
print(*result)
```

    3 4 5 6
    


```python
# With filter function
result = list(filter(lambda i: i > 2, nums))
print(*result)
```

    3 4 5 6
    


```python
# pass fn to filter list
def greater_than_two(num):
    return num > 2

result = [num for num in nums if greater_than_two(num)]
print(*result)
```

    3 4 5 6
    


```python
# pass fn to filter function
result = list(filter(greater_than_two, nums))
print(result)
```

    [3, 4, 5, 6]
    

### Filtering with `None` Data Type

When filtering through values in Python, we can also filter through `None` values. In Python, `None` represents the absence of a value.

Here are some points to keep in mind when filtering through `None` values:

- Boolean values: In Python, `True` is equivalent to `1` and `False` is equivalent to `0`.
- Empty containers: Empty lists, tuples, strings, and dictionaries are considered as `False` values in Python.

To filter through `None` values and return true values, you can use the `filter()` function or list comprehension.

Here's an example using `filter()`:

```text

        result = filter(None, [True, False, '', {}, [], 'hi'])
        filtered_values = list(result)
        print(filtered_values)

Alternatively, you can achieve the same result using list comprehension:
    
        iterable = [True, False, '', {}, [], 'hi']
        filtered_values = [i for i in iterable if bool(i) is not None]
        print(filtered_values)
```


```python
# with filter fn
result = list(filter(None, [1, 2, True, False, '', {}, []]))
print(result)
```

    [1, 2, True]
    


```python
# With List comprehension
result = [i for i in [1, 2, True, False, '', {}, []] if bool(i) != bool(None)]
print(result)
```

    [1, 2, True]
    

### List comprehension vs reduce in Python

The reduce function is part of Python's functools module and provides a way to perform a cumulative computation on a   sequence of elements. It applies a specified function to the elements of an iterable, reducing them to a single value. The syntax for using reduce is as follows:
        
            from functools import reduce
            result = reduce(function, iterable, initializer)
                                |
                                 --> This fn needs to take two arguments, because we are comparing 
                                 (x, y) or two things all the time
            
- The reduce function is particularly useful when you need to perform operations such as summation, multiplication, or <br>aggregation on a sequence.
- It requires an explicit import from the functools module.
- The specified function should take two arguments and return a single value.
- The initializer argument is optional and represents the initial value from which the reduction starts.
- The resulting value is the accumulation of applying the function to the elements of the iterable.
            
            For sum of a list if we use list comprehension
                Ex: sum([i for i in iterable])
            If we use reduce fn-->
                Ex: reduce(lamda x, y: x + y, iterable)


```python
# Using list comprehension
result = sum([num for num in nums])  # for summing all the iterable values 
print(result)
```

    21
    


```python
# Using reduce
from functools import reduce
result = reduce(lambda x, y: x + y, nums)
print(result)
```

    21
    


```python
# Flattening a nested list using List Comprehension
nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened_list = [item for sublist in nested_list for item in sublist]
print(flattened_list)  # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9]
    


```python
# Flattening a nested list using reduce fn
flattened_list = reduce(lambda x, y: x + y, nested_list)   # Because it adds two list and continue it's process
print(flattened_list)
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9]
    


```python
# finding max num using reduce fn
my_list = [1, 8, 10, 0, 9, 58, 3]
result = reduce(lambda x, y: x if x > y else y, my_list)
print(result)
```

    58
    


```python
# Finding max num using max fn
result = max([i for i in my_list])
print(result)
```

    58
    

### List Comprehensions with Multiple For Loops (Nested For Loops)

List comprehensions in Python can have multiple for loops, also known as nested for loops or double iteration. This allows you to generate a list by iterating over multiple iterables simultaneously. The general syntax for list comprehensions with multiple for loops is as follows:
            
     new_list = [(expression) for (variable1) in (iterable1) for (variable2) in (iterable2) ... for (variablen) in (iterablen)]
                                        |                                                              |
                                        |                                                              |
                                        |                                           And the rightmost for loop will be 
                                        |                                                 the (inner loop)
                                        |
                                        |
                                         ---> In this the leftmost for loop will be the (outer loop)
                                         
                                         
In this syntax:

- `new_list` is the name of the new list that will be created.
- `(expression)` represents an expression or a computation that determines the value of each element in the new list.
- This `(expression)` can be any iterable like Dictionary {}, tuple (), list []
- `(variable1)`, `(variable2)`, ..., `(variablen)` are the loop variables used to iterate over the corresponding `(iterable1)`, `(iterable2)`, ..., `(iterablen)`.
- `(iterable1)`, `(iterable2)`, ..., `(iterablen)` are sequences, such as lists or tuples, that contain the elements used for iteration.
          
#### we can also visualize it though normal way
            
            for i in iterables:
                for j in iterables:
                    .
                    .
                    .
                        for n in iterables :
                            print(i, j, ... n)


```python
# A list of Tuples
numbers = [1, 2, 3]
letters = ['a', 'b', 'c']
combined_list = [(num, letter) for num in numbers for letter in letters]
print(combined_list)
```

    [(1, 'a'), (1, 'b'), (1, 'c'), (2, 'a'), (2, 'b'), (2, 'c'), (3, 'a'), (3, 'b'), (3, 'c')]
    


```python
# A list of Dictionarys
numbers = [1, 2, 3]
letters = ['a', 'b', 'c']
combined_list = [{num, letter} for num in numbers for letter in letters]
print(combined_list)
```

    [{1, 'a'}, {1, 'b'}, {1, 'c'}, {2, 'a'}, {'b', 2}, {2, 'c'}, {3, 'a'}, {'b', 3}, {3, 'c'}]
    


```python
# A list of Lists
numbers = [1, 2, 3]
letters = ['a', 'b', 'c']
combined_list = [[num, letter] for num in numbers for letter in letters]
print(combined_list)
```

    [[1, 'a'], [1, 'b'], [1, 'c'], [2, 'a'], [2, 'b'], [2, 'c'], [3, 'a'], [3, 'b'], [3, 'c']]
    


```python
# Flattening a nested list using List Comprehension
nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened_list = [item for sublist in nested_list for item in sublist]
print(flattened_list)  # Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

    [1, 2, 3, 4, 5, 6, 7, 8, 9]
    

### 3 Ways to Print in List comprehensions (Printing List Comps for Debugging)


In Python, when using list comprehensions, the expressions inside the comprehension are evaluated and added to the resulting list. However, when using a function that only performs printing without returning a value, it will evaluate to `None` by default. This behavior can be observed when using list comprehensions with the `print()` function.

Let's consider the following example:

```text

            [print(i) for i in range(3)]

When executed in a Jupyter Notebook, this code will print the values 0, 1, and 2 to the notebook cell output. However, since the print() function does not have a return value, the resulting list will contain None for each iteration. This is because the list comprehension evaluates the expressions but does not capture any return values.

The output will be as follows:
        
             0
             1
             2
             [None, None, None]
             
To capture the values returned by a function in a list comprehension, the function should explicitly return the desired value. Let's consider an example using a custom function printreturn() that returns the input value:

1st way: 
           def printreturn(i):
                return i

            [printreturn(i) for i in range(3)]
            
The output will be as follows:
        
             0
             1
             2
             [0, 1, 2]

2nd way: 
    
             print([i for i in range(3)])

3rd way: 
                    
             [print(i) or i for i in range(3)]
```


```python
def printreturn(i):
    return i
[printreturn(i) for i in range(3)]
```




    [0, 1, 2]




```python
print([i for i in range(3)])
```

    [0, 1, 2]
    


```python
[print(i) or i for i in range(3)]
```

    0
    1
    2
    




    [0, 1, 2]



<div align="center">
    <h1>Dictionary Comprehension</h1>
</div>

#### Dictionary Comprehension Syntax

The syntax for dictionary comprehension in Python is as follows:

        my_dict = {key: expression for (key, value) in iterable}
        
In this syntax:

- `my_dict` is the name of the dictionary that will be created.
- `key` represents the key of each key-value pair in the resulting dictionary.
- `expression` is an expression that will be evaluated to determine the value of each key-value pair.
- `(key, value)` is the unpacking pattern that extracts the key and value from each element of the `iterable`.
- `iterable` is a sequence, such as a list or a tuple, that contains the elements used to create the dictionary.

The resulting dictionary `my_dict` will contain key-value pairs, where the key is extracted from the `iterable` and the value is determined by the `expression` for each element in the `iterable`.


```python
# Example for simple Dictionary Comprehension
tempreture = {"dhaka": 24, "sylet": 26, "barisal": 27, "cumilla": 25}
c_to_f = {key: (value * 9/5) + 32 for (key, value) in tempreture.items()}
print(c_to_f)
```

    {'dhaka': 75.2, 'sylet': 78.8, 'barisal': 80.6, 'cumilla': 77.0}
    

### Dictionary Comprehension with Filtering

Dictionary comprehensions in Python can include filtering to selectively include key-value pairs based on certain conditions. The syntax for dictionary comprehension with filtering is as follows:
             
             new_dict = {key: expression for (key, value) in iterable if condition}
             
In this syntax:

- `new_dict` is the name of the new dictionary that will be created.
- `key` represents the key of each key-value pair in the resulting dictionary.
- `expression` is an expression that will be evaluated to determine the value of each key-value pair.
- `(key, value)` is the unpacking pattern that extracts the key and value from each element of the `iterable`.
- `iterable` is a sequence, such as a list or a tuple, that contains the elements used to create the new dictionary.
- `condition` is an optional condition that filters the elements based on a specific criterion. Only the elements that satisfy the condition will be included in the new dictionary.

#### Example

Here's an example to illustrate dictionary comprehension with filtering:

            my_dict = {'apple': 3, 'banana': 5, 'orange': 2, 'kiwi': 1}
            filtered_dict = {key: value for (key, value) in my_dict.items() if value > 2}
            print(filtered_dict)  # Output: {'apple': 3, 'banana': 5}
      
       In this example, a dictionary comprehension is used to filter out the key-value pairs from
       `my_dict` where the value is greater than 2. 
       The resulting `filtered_dict` will only contain the key-value pairs that satisfy the condition.
    


```python
# Dictionary Comprehension with Filtering
c_to_f = {key: (value * 9/5) + 32 for (key, value) in tempreture.items() if value > 25}
print(c_to_f)
```

    {'sylet': 78.8, 'barisal': 80.6}
    

### Dictionary Comprehension with Conditional Expression

Dictionary comprehensions in Python can include conditional expressions to selectively assign values to key-value pairs based on certain conditions. The syntax for dictionary comprehension with conditional expression is as follows:

       new_dict = {key: (value_if_true) if (condition) else (value_if_false) for (key, value) in iterable}
       new_dict = {(key_if_true) if (condition) else (key_if_false): value for (key, value) in iterable}
            
In this syntax:

- `new_dict` is the name of the new dictionary that will be created.
- `key` represents the key of each key-value pair in the resulting dictionary.
- `value_if_true` is the value assigned to the key if the condition is true.
- `value_if_false` is the value assigned to the key if the condition is false.
- `(key, value)` is the unpacking pattern that extracts the key and value from each element of the `iterable`.
- `iterable` is a sequence, such as a list or a tuple, that contains the elements used to create the new dictionary.
- `condition` is the condition that determines which value to assign to the key.

##### Example

Here's an example to illustrate dictionary comprehension with conditional expression:

```text

        my_dict = {'apple': 3, 'banana': 5, 'orange': 2, 'kiwi': 1}
        discounted_dict = {key: value * 0.8 if value >= 3 else value for (key, value) in my_dict.items()}
        print(discounted_dict)  # Output: {'apple': 2.4, 'banana': 4.0, 'orange': 2, 'kiwi': 1}
```


```python
# Dictionary Comprehension with Conditional Expression(value)
c_to_f = {key: (value * 9/5) + 32 if value > 25 else value for (key, value) in tempreture.items()}
print(c_to_f)
```

    {'dhaka': 24, 'sylet': 78.8, 'barisal': 80.6, 'cumilla': 25}
    


```python
# Dictionary Comprehension with Conditional Expression(key)
c_to_f = {(key.upper() if value > 25 else key): (value * 9/5) + 32 for (key, value) in tempreture.items()}
print(c_to_f)
```

    {'dhaka': 75.2, 'SYLET': 78.8, 'BARISAL': 80.6, 'cumilla': 77.0}
    


```python
# Another condition
c_to_f = {(key if key == 'dhaka' else 'UIU'): (value * 9/5) + 32 for (key, value) in tempreture.items()}
print(c_to_f)    # In the result if key not equal to dhaka it will return the last value of the dict and assign it to the else condition
```

    {'dhaka': 75.2, 'UIU': 77.0}
    


```python
# Combined all of this 
c_to_f = {(key if key == 'dhaka' else 'UIU'): (value * 9/5) + 32 if value > 26 else value for (key, value) in tempreture.items() if value > 25}
print(c_to_f)
```

    {'UIU': 80.6}
    

### Dictionary Comprehension with Function

Dictionary comprehensions in Python can include applying a function to the values while creating a new dictionary. The syntax for dictionary comprehension with a function is as follows:

            new_dict = {key: fn(value) for (key, value) in iterable}
            
In this syntax:

- `new_dict` is the name of the new dictionary that will be created.
- `key` represents the key of each key-value pair in the resulting dictionary.
- `fn` is the function applied to the corresponding value.
- `value` is the value extracted from each element of the `iterable`.
- `(key, value)` is the unpacking pattern that extracts the key and value from each element of the `iterable`.
- `iterable` is a sequence, such as a list or a tuple, that contains the elements used to create the new dictionary.

#### Example

Here's an example to illustrate dictionary comprehension with a function applied to the values:

```text

          def square_root(value):
               return value ** 0.5

          numbers = {'a': 9, 'b': 16, 'c': 25, 'd': 36}
          root_dict = {key: square_root(value) for key, value in numbers.items() if value > 10}
          print(root_dict)  # Output: {'b': 4.0, 'c': 5.0, 'd': 6.0}
```


```python
def square_root(value):
    return value ** 0.5

numbers = {'a': 9, 'b': 16, 'c': 25, 'd': 36}
root_dict = {key: square_root(value) for key, value in numbers.items() if value > 10}
print(root_dict)  # Output: {'b': 4.0, 'c': 5.0, 'd': 6.0}
```

    {'b': 4.0, 'c': 5.0, 'd': 6.0}
    


```python
d = {key: value for (key, value) in enumerate(['nafiz', 'taha', 'sunan'])}
my_dict = {key: value.upper() if key == 1 else value for (key, value) in d.items()}
print(my_dict)
```

    {0: 'nafiz', 1: 'TAHA', 2: 'sunan'}
    


```python
my_list = [1, 2, '', [], [], 6]
new_list = list(filter(lambda x:x != [], my_list))
print(new_list)
```

    [1, 2, '', 6]
    


### Conclusion

Comprehensions offer several benefits in terms of readability and efficiency. By using comprehensions, you can often achieve the same results as traditional iterative approaches with significantly fewer lines of code. Comprehensions also tend to be more readable and expressive, as they succinctly capture the intent of the data structure creation.

Furthermore, comprehensions have a performance advantage over traditional loops in many cases. They leverage the underlying optimizations of the Python interpreter, resulting in faster execution times. This can be especially beneficial when dealing with large datasets or performance-critical code.

In summary, comprehensions in Python provide a concise and efficient way to create lists, dictionaries, and sets. By leveraging comprehensions, you can write more expressive and readable code while maintaining performance. Whether you're working with lists, dictionaries, or sets, comprehensions are a valuable tool in your Python programming arsenal.