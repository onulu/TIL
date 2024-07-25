# Mutable Sequence Operations

Supported by mutable sequence types, such as lists.

## Operations

- `s[i] = x` - item i of s is replaced by x
- `s[i:j] = t` - slice of s from i to j is replaced by the contents of the iterable t
- `del s[i:j]` - same as `s[i:j] = []`
- `s[i:j:k] = t` - the elements of s[i:j:k] are replaced by those of t
- `del s[i:j:k]` - removes the elements of s[i:j:k] from the list
- `s.append(x)` - appends x to the end of the sequence
- `s.clear()` - removes all items from s
- `s.copy()` - creates a shallow copy of s
- `s.extend(t)` or `s += t` - extends s with the contents of t
- `s *= n` - updates s with its contents repeated n times
- `s.insert(i, x)` - inserts x into s at the index i
- `s.pop([i])` - removes the item at index i and returns it
- `s.remove(x)` - removes the first item from s where s[i] is equal to x
- `s.reverse()` - reverses the items of s in place

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
