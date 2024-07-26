# Transposing a matrix

## List comprehension

```python
def transpose(matrix):
    return [[row[i] for row in matrix] for i in range(len(matrix[0]))]

matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
transposed = transpose(matrix)
# [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
```

## Using NumPy

```python
import numpy as np

matrix = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
transposed = matrix.T # or np.transpose(matrix)
```

## Using zip()

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
transposed = list(map(list, zip(*matrix)))
# [[1, 4, 7], [2, 5, 8], [3, 6, 9]]

transposed = list(zip(*matrix))
# [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
```

- List comprehension is pythonic and readable.
- NumPy is very efficient for large matrices and provides many additional matrix operations.
- Map and Zip approach is concise.
