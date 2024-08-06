# 여러개의 리스트에서 공통된 중복 요소 찾기

`set`와 `intersection`을 사용해 여러개의 리스트에서 공통의 요소를 찾을 수 있다. (공통의 요소 -> 합집합으로 생각할 수 있음)
`&` 연산자는 `intersection()` 메서드와 유사하지만 두개의 세트를 비교할때는 더 빠르다.

```python
array1 = [1, 2, 3, 4, 5]
array2 = [3, 4, 5, 6, 7]

print(set(array1) & set(array2))
# {3, 4, 5}
```

아래와 같이 `&=` 연산자를 사용해 `set1`에 공통요소값을 덮어씌울 수 있다.

```python
set1 &= set2
```

두개 이상의 배열에서 공통요소를 찾기위해 함수를 작성할 수 있다.

```python
def find_duplicates(*lists):
  sets = [set(lst) for lst in lists] #[{1, 2, 3}, {2, 3, 5}, {2, 3, 7}]
  return set.intersection(*sets)

list1 = [1, 2, 3]
list2 = [2, 3, 5]
list3 = [2, 3, 7]

duplicates = find_duplicates(list1, list2, list3)
print(duplicates)  # Output: {2, 3}
```
