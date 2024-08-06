# 리스트에서 중복요소 제어하기

## Set() 사용

```python
def remove_dups(lst):
    return list(set(lst))
```

파이썬에서 `set`는 요소의 중복을 허용하지 않기 때문에 set로 생성하면 자동으로 중복요소가 제거 된다. 배열로 사용하기 위해서는 다시 배열로 변환해 반환한다.

## 리스트 컴프리핸션 사용하기

```python
def remove_dups(lst):
    return [n for i, n in enumerate(lst) if n not in lst[:i]]
```

`enumerate` 함수는 리스트의 `index`와 `value`를 반환한다.
리스트 컴프리핸션에서는 현재 인덱스 이전까지의 리스트와 현재값을 비교해 중복된 요소의 추가를 막을 수 있다.

lst = [1,1,1,3]
i = 0, n = 1 -> 1 not in list[:0] -> [] -> True
i = 1, n = 1 -> 1 not in list[:1] -> [1] -> False
i = 2, n = 1 -> 1 not in list[:2] -> [1,1] -> False

## for문 사용하기

```python
def remove_dups(lst):
    new_lst = []
    for i in lst:
        if i not in new_lst:
            new_lst.append(i)
    return new_lst
```
