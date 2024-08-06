# Common Sequence Operations

문자열, 배열, 튜플등 대부분의 시퀀스 타입에서 사용할 수 있는 연산자들

## Operations

`x in s` - x가 s에 포함되어 있으면 참, 반대는 x not in s
`s + t` - s와 t를 결합
`s * n` 또는 `n * s` - s를 n번 반복
`s[i]` - 인덱싱
`s[i:j]` - 슬라이싱
`s[i:j:k]` - 슬라이싱 + 간격(k)
`len(s)` - s의 길이
`min(s)` - s의 요소 중 가장 작은 것
`max(s)` - s의 요소 중 가장 큰 것
`s.index(x[, i[, j]])` - s에서 x의 위치를 찾음 (선택적으로 i부터 j까지 범위 지정)
`s.count(x)` - s 안에 x가 몇 개 있는지 세기`

---

## 인덱싱

```python
my_list = [1, 2, 3, 4, 5]
print(my_list[-1]) # 5

my_str = 'hello'
print(my_str[0]) # h

```

## 슬라이싱

```python
my_list = [1, 2, 3, 4, 5]
print(my_list[1:3]) # [2, 3]
print(my_list[1:]) # [2, 3, 4, 5]
print(my_list[:3]) # [1, 2, 3]
print(my_list[:]) # [1, 2, 3, 4, 5]
print(my_list[::2]) # [1, 3, 5]
print(my_list[::-1]) # [5, 4, 3, 2, 1]
```

## 결합하기

```python
my_list = [1, 2, 3]
other_list = [4, 5, 6]
print(my_list + other_list) # [1, 2, 3, 4, 5, 6]
```

## 인덱스 구하기

```python
my_list = [1, 2, 3, 4, 5]
print(my_list.index(3)) # 2

# ValueError: 6 is not in list
print(my_list.index(6))

# search from index 2 to 4
print(my_list.index(3, 2, 4)) # 2
```
