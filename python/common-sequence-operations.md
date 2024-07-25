# Common Sequence Operations

supported by most sequence types, both mutable and immutable.
for example strings, lists, and tuples.

## Operations

`x in s` - True if an item of s is equal to x, else False
`x not in s` - False if an item of s is equal to x, else True
`s + t` - the concatenation of s and t
`s * n` or `n * s` - equivalent to adding s to itself n times
`s[i]` - ith item of s, origin 0
`s[i:j]` - slice of s from i to j
`s[i:j:k]` - slice of s from i to j with step k
`len(s)` - length of s
`min(s)` - smallest item of s
`max(s)` - largest item of s
`s.index(x[, i[, j]])` - index of the first occurrence of x in s (at or after index i and before index j)
`s.count(x)` - total number of occurrences of x in s

---

## Indexing

```python
my_list = [1, 2, 3, 4, 5]
print(my_list[0]) # 1
print(my_list[-1]) # 5
```

## Slicing

```python
my_list = [1, 2, 3, 4, 5]
print(my_list[1:3]) # [2, 3]
print(my_list[1:]) # [2, 3, 4, 5]
print(my_list[:3]) # [1, 2, 3]
print(my_list[:]) # [1, 2, 3, 4, 5]
print(my_list[::2]) # [1, 3, 5]
print(my_list[::-1]) # [5, 4, 3, 2, 1]
```

## Concatenation

```python
my_list = [1, 2, 3]
other_list = [4, 5, 6]
print(my_list + other_list) # [1, 2, 3, 4, 5, 6]
```

## Finding Index

```python
my_list = [1, 2, 3, 4, 5]
print(my_list.index(3)) # 2

# ValueError: 6 is not in list
print(my_list.index(6))

# search from index 2 to 4
print(my_list.index(3, 2, 4)) # 2
```
