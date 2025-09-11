1.
Write a select function that mimics the built-in `filter` function.
Your `select` function should take two arguments:
a callback function and an iterable object.
It should return a list of all the elements of the iterable
for which the callback function returns a truthy value.
It should not include any elements for which the callback returns a falsy value.
```python

def select(callback, collection):
    selection = []

    for element in collection:
        if callback(element):
            selection.append(element)

    return selection

numbers = [1, 2, 3, 4, 5]
colors = {'red', 'orange', 'yellow', 'green',
          'blue', 'indigo', 'violet'}

odd_numbers = select(lambda number: number % 2 != 0, numbers)
print(odd_numbers)            # [1, 3, 5]

large_numbers = select(lambda number: number >= 10, numbers)
print(large_numbers)          # []

small_numbers = select(lambda number: number < 10, numbers)
print(small_numbers)          # [1, 2, 3, 4, 5]

short_color_names = select(lambda color: len(color) <= 5, colors)
print(short_color_names)      # ['blue', 'red', 'green']
# # The order of the colors may vary, but should include the
# # indicated colors.
```

- Using list comprehension:
```python

def select(callback, collection):
    return [el for el in collection if callback(el)]

numbers = [1, 2, 3, 4, 5]
colors = {'red', 'orange', 'yellow', 'green',
          'blue', 'indigo', 'violet'}

odd_numbers = select(lambda number: number % 2 != 0, numbers)
print(odd_numbers)            # [1, 3, 5]

large_numbers = select(lambda number: number >= 10, numbers)
print(large_numbers)          # []

small_numbers = select(lambda number: number < 10, numbers)
print(small_numbers)          # [1, 2, 3, 4, 5]

short_color_names = select(lambda color: len(color) <= 5, colors)
print(short_color_names)      # ['blue', 'red', 'green']
# # The order of the colors may vary, but should include the
# # indicated colors.
```

2.
Write a `reject` function that mimics the `select` function you just wrote,
but that rejects rather than selects elements from the iterable object.
That is, it should return a list of all the elements of the iterable for which the callback function doesn't return a truthy value.
It should only include any elements for which the callback returns a falsy value.
```python
def reject(callback, collection):
    selection = []

    for item in collection:
        if not callback(item):
            selection.append(item)

    return selection

numbers = [1, 2, 3, 4, 5]
colors = {'red', 'orange', 'yellow', 'green',
          'blue', 'indigo', 'violet'}

even_numbers = reject(lambda number: number % 2 != 0, numbers)
print(even_numbers)            # [2, 4]

small_numbers = reject(lambda number: number >= 10, numbers)
print(small_numbers)          # [1, 2, 3, 4, 5]

large_numbers = reject(lambda number: number < 10, numbers)
print(large_numbers)          # []

long_color_names = reject(lambda color: len(color) <= 5, colors)
print(long_color_names)
# ['yellow', 'violet', 'orange', 'indigo']
# The order of the colors may vary, but should include the
# indicated colors.
```

    - Using list comprehension:
```python
def reject(callback, collection):
    return [item for item in collection if not callback(item)]

numbers = [1, 2, 3, 4, 5]
colors = {'red', 'orange', 'yellow', 'green',
          'blue', 'indigo', 'violet'}

even_numbers = reject(lambda number: number % 2 != 0, numbers)
print(even_numbers)            # [2, 4]

small_numbers = reject(lambda number: number >= 10, numbers)
print(small_numbers)          # [1, 2, 3, 4, 5]

large_numbers = reject(lambda number: number < 10, numbers)
print(large_numbers)          # []

long_color_names = reject(lambda color: len(color) <= 5, colors)
print(long_color_names)
# ['yellow', 'violet', 'orange', 'indigo']
# The order of the colors may vary, but should include the
# indicated colors.
```

3.
- A function that often appears in languages that have `map` and `filter` functions is called the `reduce` function,
or, sometimes, `inject`.
Python has one tucked away in the `functools` module, but we won't be using it in this challenge.

- The `reduce` function reduces the elements in an iterable object to a single value.
    - For instance, `reduce` can return the sum of all numbers in a list or concatenate the strings in a tuple to form a single long string.
    - It's a bit like `map`, but instead of returning a new collection,
it just returns a single value.

- `reduce` functions typically take 3 arguments:
    - a callback that takes two arguments.
        - The first argument is the current element of the iterable argument and the second is the current reduction value, commonly called the "accumulator" and named `accum`.
    - an iterable.
    - a starting value.
        - The starting value is the initial value for the current argument in the callback.

- For instance, consider the following reduce invocation:
```python
numbers = [10, 3, 5]
product = lambda number, accum: accum * number
print(reduce(product, numbers, 2))     # 300
# 10 * 2 * 3 * 5
```

- On the first invocation of the product `lambda`, `number` will be 10 while `accum` will be 2, the starting value given by the third argument to reduce. The callback will return 20.

- On the second invocation of product, number will be 3 while `accum` will be 20, the return value from the previous invocation. The return value will be 60.

- On the final invocation, number will be 5, `accum` will be 60, and the return value will be 300.

- `reduce` always uses the callback like this. The first invocation gets passed the first element of the iterable and the starting value given by `reduce`'s third argument. It then passes the callback the second element of the iterable and the return value of the first invocation. This continues until all elements have been processed by the callback, and the final return value of reduce is the return value of the last callback invocation.

- Your job in this problem is to implement `reduce`. Beware: this may be a challenging problem. We recommend not using comprehensions.
```python
numbers = (1, 2, 4, 8, 16)
total = lambda number, accum: accum + number
print(reduce(total, numbers, 0))        # 31

numbers = [10, 3, 5]
product = lambda number, accum: accum * number
print(reduce(product, numbers, 2))      # 300

colors = ['red', 'orange', 'yellow', 'green',
          'blue', 'indigo', 'violet']
rainbow = lambda color, accum: accum + color[0].upper()
print(reduce(rainbow, colors, ''))      # ROYGBIV
```

- Solution:
```python
def reduce(callback, collection, start):
    accum = start

    for item in collection:
        accum = callback(item, accum)

    return accum

numbers = (1, 2, 4, 8, 16)
total = lambda number, accum: accum + number
print(reduce(total, numbers, 0))        # 31

numbers = [10, 3, 5]
product = lambda number, accum: accum * number
print(reduce(product, numbers, 2))      # 300

colors = ['red', 'orange', 'yellow', 'green',
          'blue', 'indigo', 'violet']
rainbow = lambda color, accum: accum + color[0].upper()
print(reduce(rainbow, colors, ''))      # ROYGBIV
```

4.
Use the reduce function shown in the answer to the previous question to compute the sum of the squares in a list of numbers.
```python
def reduce(callback, collection, start):
    accum = start

    for item in collection:
        accum = callback(item, accum)

    return accum

numbers = (1, 2, 4, 8, 16)

squares = reduce(lambda number, accum: number ** 2, numbers, 1)
print(squares) # 256
```
