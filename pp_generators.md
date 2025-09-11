1.
- Create a generator expression that generates the reciprocals of the numbers from 1 to 10.
A reciprocal of a number n is 1 / n.
Use a `for` loop to print each value.
```python
reciprocals = (1 / x for x in range(1, 11))

for value in reciprocals:
    print(value)
```

2.
- Create a generator function that generates the reciprocals of the numbers from 1 to n,
where n is an argument to the function.
Use a for loop to print each value.
```python
def recipe_gen_func(n):
    count = 1
    while count <= n:
        yield count
        count += 1

test = recipe_gen_func(3)
for num in test:
    print(1 / num)
# 1.0
# 0.5
# 0.33333333
```

3.
Use a generator expression to capitalize every string in a list of strings.
Use a single print invocation to print all the capitalized strings as a tuple.
```python
str_list = ['first', 'second', 'third']

gen_obj = (el.capitalize() for el in str_list)
print(tuple(gen_obj))
# ('First', 'Second', 'Third')
```

4.
Create a generator function that generates the capitalized version of every string in a list of strings. Use a single print invocation to print all the capitalized strings as a tuple.
```python
def cap(collection, list=[]):
    for string in collection:
        yield string.capitalize()

print(tuple(cap(['first', 'second', 'third'])))
```

5.
Use a generator expression to capitalize the strings in a list of strings whose length is at least 5. Use a single print invocation to print all the capitalized strings as a set.
```python
my_list = ['tester123', 'alphagenetic', 'one', 'two', 'fasho']

cap_generator = (el.capitalize() for el in my_list
                 if len(el) >= 5)

print(set(cap_generator))
# {'Alphagenetic', 'Tester123', 'Fasho'}
```

6.
Create a generator function that generates the capitalized version of every string in a list of strings whose length is less than 5. Use a single print invocation to print all the capitalized strings as a set.
```python
my_list = ['tester123', 'alphagenetic', 'one', 'two', 'fasho']

def cap_strings(collection):
    for string in collection:
        if len(string) >= 5:
            yield string.capitalize()

print(set(cap_strings(my_list)))
# {'Fasho', 'Alphagenetic', 'Tester123'}
```

7.



Notes:
- When you pass a generator object into a built-in iterable function like `list()`, the function consumes the generator, iterating through all its yielded values to create a list containing those values.
- The generator is exhausted in the process, so it cannot be iterated over again without creating a new generator object.

- An expression function, also known as a generator expression, creates a generator object that produces values one at a time as you iterate over it. When you pass this generator object into a built-in iterable function like list(), the function iterates through the generator expression, collecting all the generated values into a list. This consumes the generator expression, exhausting it just like a generator function.

- A generator function is not the same as a generator expression, but both produce generator objects.
    - A generator function is defined using def and the yield keyword to produce values, while a generator expression is a concise syntax using parentheses to create a generator object in a single expression.
    - Both behave similarly when iterated over, producing values lazily one at a time.
