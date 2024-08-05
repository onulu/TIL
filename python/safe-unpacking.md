# 리스트의 요소 안전하게 언패킹하기

웹 데이터를 스크래핑할 때, 마크업에서 일부 요소가 누락되는등의 일관성이 없는 경우를 만날 수 있다.
예를 들어, 구인 공고를 스크래핑할 때 일부 게시물에는 다른 게시물에 있는 '지역' 같은 필드가 누락될 수 있다. 이러한 불일치는 데이터를 변수로 언패킹할 때 오류를 일으킬 수 있다.

1. 기본값을 사용한 리스트 슬라이싱

```python
company, position, *rest = job.find_all('span', class_='company')
region = rest[0] if rest else ''
```

2. 헬퍼 함수를 사용하기

```python
def safe_unpack(iterable, num, default = ''):
    return list(iterable) + [default] * (num - len(iterable))

company, position, region = safe_unpack(job.find_all('span', class_='company'), 3)
```

`safe_unpack` 함수를 사용하면 값이 없는 경우 기본값으로 채워주어 항상 예상된 수의 항목을 얻을 수 있고 에러를 방지할 수 있다.
