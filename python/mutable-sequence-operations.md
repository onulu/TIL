# Mutable Sequence Operations

리스트와 같은 가변의 시퀀스 타입 연산자

## Operations

- `s[i] = x` - s의 i번째 항목을 x로 대체
- `s[i:j] = t` - s의 i부터 j까지의 슬라이스를 반복 가능한 t의 내용으로 대체
- `del s[i:j]` - `s[i:j] = []`와 동일
- `s[i:j:k] = t` - s[i:j:k]의 요소들을 t의 요소들로 대체
- `del s[i:j:k]` - s[i:j:k]의 요소들을 리스트에서 제거
- `s.append(x)` - x를 시퀀스의 끝에 추가
- `s.clear()` -  s의 모든 항목을 제거
- `s.copy()` - s의 얕은 복사본을 생성
- `s.extend(t)` 혹은 `s += t` - s를 t로 확장
- `s *= n` - s의 내용을 n번 반복하여 s를 업데이트
- `s.insert(i, x)` - x를 s의 인덱스 i 위치에 삽입
- `s.pop([i])` - 인덱스 i의 항목을 제거하고 반환
- `s.remove(x)` - s[i]가 x와 같은 첫 번째 항목을 s에서 제거
- `s.reverse()` - s의 항목들을 제자리에서 뒤집음

---

## Replacing an Item

```python
my_list = [1, 2, 3, 4, 5]
my_list[0] = 10
print(my_list) # [10, 2, 3, 4, 5]
```

## Replacing a Slice

```python
my_list = [1, 2, 3, 4, 5]
my_list[1:3] = [20, 30]
print(my_list) # [1, 20, 30, 4, 5]
```

## Deleting a Slice

```python
my_list = [1, 2, 3, 4, 5]
del my_list[1:3]
print(my_list) # [1, 4, 5]
```

## Replacing a Slice with a Step

```python
my_list = [1, 2, 3, 4, 5]
my_list[::2] = [10, 30, 50]
print(my_list) # [10, 2, 30, 4, 50]
```

## Deleting a Slice with a Step

```python
my_list = [1, 2, 3, 4, 5]
del my_list[::2]
print(my_list) # [2, 4]
```

## Appending an Item

```python
my_list = [1, 2, 3, 4, 5]
my_list.append(6)
print(my_list) # [1, 2, 3, 4, 5, 6]
```

## Clearing a List

```python
my_list = [1, 2, 3, 4, 5]
my_list.clear()
print(my_list) # []
```

## Copying a List

```python
my_list = [1, 2, 3, 4, 5]
new_list = my_list.copy()
print(new_list) # [1, 2, 3, 4, 5]
```

## Extending a List

```python
my_list = [1, 2, 3]
other_list = [4, 5, 6]
my_list.extend(other_list)
print(my_list) # [1, 2, 3, 4, 5, 6]
```

## Inserting an Item

```python
my_list = [1, 2, 3, 4, 5]
my_list.insert(2, 300) # insert 30 at index 2
print(my_list) # [1, 2, 300, 3, 4, 5]
```

## Popping an Item

```python
my_list = [1, 2, 3, 4, 5]
item = my_list.pop()
print(item) # 5
print(my_list) # [1, 2, 3, 4]
```

## Popping an Item at Index

```python
my_list = [1, 2, 3, 4, 5]
item = my_list.pop(2)
print(item) # 3
print(my_list) # [1, 2, 4, 5]
```

## Removing an Item

```python
my_list = [1, 2, 3, 4, 5]
my_list.remove(3)
print(my_list) # [1, 2, 4, 5]
```

## Reversing a List

```python
my_list = [1, 2, 3, 4, 5]
my_list.reverse()
print(my_list) # [5, 4, 3, 2, 1]
```
