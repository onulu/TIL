# Finding duplicate items across multiple lists

To find duplicate items across multiple lists in Python, you can use sets and their intersection.

You can use `&` operator to perform an intersection operation. It's equivalent to the `intersection()` method but faster for two sets.

```python
array1 = [1, 2, 3, 4, 5]
array2 = [3, 4, 5, 6, 7]

print(set(array1) & set(array2))
# {3, 4, 5}
```

You can also use it with the augmented assignment operator.
This modifies `set1` in-place, keeping only elements also present in `set2`

```python
set1 &= set2
```

For multiple lists, you can define function to find duplicates.

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

This returns a set of duplicate items. If you need a list instead, you can convert the result using `list(duplicates)`
