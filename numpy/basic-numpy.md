Numpy는 수학계산을 위한 파이썬 라이브러리로 다차원 배열기반 연산을 지원한다. 기본 파이썬의 리스트와 가장 큰 차이는 numpy배열은 **모든 요소가 동일한 타입**이어서 메모리 사용이 효율적이고 연산 속도도 훨씬 빠르다.

## 배열 생성

## np.array

```python
# 1차원 배열
arr = np.array([1, 2, 3])
print(arr) # [1 2 3]

# 2차원 배열
arr2 = np.array([[1, 2, 3], [4, 5, 6]])
print(arr2) 
# [[1 2 3]
#  [4 5 6]]

# 모든값이 0 또는 1인 배열
arr3 = np.zeros((3, 3))
arr4 = np.ones((3, 3))
```

### np.arange, np.linspace

특정 간격의 배열생성하거나 특정 구간을 일정한 간격으로 원하는 갯수의 배열 생성한다.

`arange`는 반복문에서 인덱스 처리할때 많이 쓰고, `linspace`는 그래프나 데이터를 균일하게 나눌 때 유용

```python
# 0-9까지 1씩 증가
arr_range = np.arange(0, 10, 1)
# [0 1 2 3 4 5 6 7 8 9]

# 0-1까지 5개의 배열 생성
arr_linspace = np.linspace(0, 1, 5)
# [0.  0.25  0.5  0.75  1]
```

### np.random

랜덤하게 초기화된 배열이 필요할 때 사용. (랜덤 샘플링)
- rand - 
- randint - 정수형 랜덤 배열
- 

```python
# 0에서 1사이의 랜덤한 값으로 이루어진 3x3배열 생성
rand = np.random.rand(3, 3)

# 0에서 10사이의 정수 3x3배열
rand_int = np.random.randint(0, 10, (3, 3))
```


### np.shape, np.reshape

배열의 크기를 확인하고 배열 변형하기

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr.shape)
# (2, 3)

# arr.reshape(rows, cols)
arr1 = arr.reshape(-1) # 1차원 배열로 변형
print(arr1)
# [1 2 3 4 5 6]

arr2 = arr.reshape(-1, 2) # 2열이고 행을 자동 조절
print(arr2)
# [[1 2]
# [3 4]
# [5 6]]

arr3 = arr.reshape(2, -1) # 2행이고 열을 자동 조절
print(arr3)
#[[1 2 3]
# [4 5 6]]
```

### 배열 연산

산술 연산, 브로드캐스팅 연산

```python
arr = np.array([1, 2, 3, 4])

print(arr + 10)
# [11 12 13 14]

arr2 = np.array([5, 6, 7, 8])
print(arr1 + arr2)
# [6 8 19 12]
```

행렬 연산

```python
arr = np.array([[1, 2], [3, 4]])

# dot product 행렬곱
print(np.dot(arr, arr))
# [1 2] . [1 2]
# [3 4]   [3 4]

# [[1+6  2+8]
# [ 3+12 6+16]]


# 전치
print(arr.T)
# [[1 3]
#  [2 4]]
```

### np.astype 형 변환 

- 정수형 
	- int: 기본 정수
	- int8, int16, int32, int64
- 부호없는 정수
	- uint8: 8비트 (0 - 255)
	- uint16, uint32, uint64
- 실수형 (소수점 포함)
	- float16
	- float32: 단정밀도
	- float64: 배정밀도
- Boolean
	- bool: 0은 False, 그외 값은 True
- 그외 파이썬 타입도 사용가능


```python
arr = np.array([1.2, 2.5, 3.7])
arr_int = arr.astype(int)
# [1 2 3]

arr2 = np.array([1, 0, 3])
arr2.astype(bool)
# [True False True]
```
