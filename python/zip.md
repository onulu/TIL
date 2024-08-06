# `zip()`

`zip`은 여러 개의 `iterable`을 하나의 튜플로 이루어진 `iterable` 로 결합하는 내장 함수이다.

- 각 `iterable`에서 요소들을 짝지어 묶는다
- 가장 짧은 `iterable`의 길이에서 멈춘다

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
