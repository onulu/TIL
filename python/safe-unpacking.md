# How to unpacking items safely

When scraping web data, it's common to encounter inconsistencies in the structure of the information you're collecting. For example, when scraping job listings, some posts might omit fields like 'region' that are present in others. This inconsistency can cause errors when unpacking data into variables.

1. Using list slicing with a defaul value

```python
company, position, *rest = job.find_all('span', class_='company')
region = rest[0] if rest else ''
```

2. Using a helper function

```python
def safe_unpack(iterable, num, default = ''):
    return list(iterable) + [default] * (num - len(iterable))

company, position, region = safe_unpack(job.find_all('span', class_='company'), 3)
```

The `safe_unpack` function ensures you always get the expected number of items, filling in with the default value when necessary.
