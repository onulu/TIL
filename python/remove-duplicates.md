# Multiple Ways to Remove Duplicates from a List

## Using Set()

```python
def remove_dups(lst):
    return list(set(lst))
```

Since set does not allow duplicates, it will remove all duplicates from the list.
We need to return the list back, as set returns a set object.

## Using List Comprehension

```python
def remove_dups(lst):
    return [n for i, n in enumerate(lst) if n not in lst[:i]]
```

The enumerate function returns the `index` and the `value` of the list.
The list comprehension iterates over the list and checks if the value is not in the list before the current index.

lst = [1,1,1,3]
i = 0, n = 1 -> 1 not in list[:0] -> [] -> True
i = 1, n = 1 -> 1 not in list[:1] -> [1] -> False
i = 2, n = 1 -> 1 not in list[:2] -> [1,1] -> False

## Using a Loop

```python
def remove_dups(lst):
    new_lst = []
    for i in lst:
        if i not in new_lst:
            new_lst.append(i)
    return new_lst
```

## Using a While Loop

```python
def remove_dups(lst):
    new_lst = []
    while lst:
        item = lst.pop()
        if item not in new_lst:
            new_lst.append(item)
    return new_lst[::-1]
```

The pop method removes the last element from the list.

## Using a Set and List Comprehension

```python
def remove_dups(lst):
    return list({n for n in lst})
```

The set comprehension returns a set of unique elements, which is then converted back to a list.
