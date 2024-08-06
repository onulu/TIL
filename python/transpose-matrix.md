# 매트릭스(행렬) 전치하기

## List comprehension

```python
def transpose(matrix):
    return [[row[i] for row in matrix] for i in range(len(matrix[0]))]

matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
transposed = transpose(matrix)
# [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
```

## NumPy 사용

```python
import numpy as np

matrix = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
transposed = matrix.T # or np.transpose(matrix)
```

## zip() 사용

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
transposed = list(map(list, zip(*matrix)))
# [[1, 4, 7], [2, 5, 8], [3, 6, 9]]

transposed = list(zip(*matrix))
# [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
```

- 리스트 컴프리핸션은 파이썬스럽고 가독성이 좋음
- `numpy`는 큰 규모의 매트릭스에 대해 매우 효율적이고 다양한 메서드를 제공
- `map` 과 `zip`은 간결함
