# `zip()`

`zip` is a built-in function that combines multiple iterables into a single iterable of **tuples**.

- It pairs elements from each iterable together.
- It stops at the length of the *shortest* iterable.
- The result is an iterator.

## Creating dictionaries

```python

keys = ['name', 'breed', 'age']
values = ['Hippy', 'Boston Terrier', 7]
dog = dict(zip(keys, values))

# {'name': 'Hippy', 'breed': 'Boston Terrier', 'age': 7}
```

## Pairing items from lists

```python
name = ['Hippy', 'Louie', 'Haru']
ages = [7, 6, 3]
likes = ['Sweet Potato', 'Tuna', 'Banana' ]

for name, age, like in zip(names, ages, cities):
    print(f"{name} is {age} years old and lives the {like}")
```

## Matrix transposition with `*args`

Turning columns into rows.

```python
matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
]

transposed = list(zip(*matrix))
print(transposed)
# [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
```
