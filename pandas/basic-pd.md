# Pandas 기본 문법

## Pandas가져오기

```py
import pandas as pd
```

## DataFrame 과 Series

Pandas에는 *DataFrame*과 *Series* 라는 두개의 메인 객체가 있다.

1. Series
   - 1차원의 라벨을 가진 리스트
   - 모든 데이터 타입을 담을 수 있다
   - 스프레드시트의 **컬럼 한개**와 유사하다.
   - 인덱스가 있다. (시리즈내의 각각의 요소에 대한 라벨 - row의 이름과도 같아)

2. DataFrame
   - 2차원의 라벨을 가진 데이터 구조
   - 스프레드시트나 SQL테이블과 유사
   - 같은 인덱스를 가진 **여러개의 시리즈**로 구성된다
   - 각각의 컬럼은 다양한 데이터 타입을 가질 수 있다.
   - row와 column라벨을 가진다.

## DataFrame

![df layout](/asset/df.webp)
DataFrame은 여러개의 Series가 합쳐진 테이블이다. 행과 열 그리고 인덱스로 구성되어 있다.
인덱스는 주소와 같아서 행과 열을 모두 찾는 데 사용할 수 있다. (숫자를 사용할 수도 있고 문자열을 사용할수도 있다.)

```python
pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]})

#     Yes | No
# 0    50 | 131
# 1    21 |  2
```

### 파일 읽기

`index_col`은 인덱스로 사용할 컬럼을 지정할 수 있다. 한글의 경우 `encoding`을 지정해야 하는 경우도 있다.

```python
df = pd.read_csv('/example.csv', index_col=0)
```

### 데이터 살펴보기

```Python
df.head()   # 첫 5개 열을 가져온다
df.tail()   # 끝 5개 열을 가져온다

df.info()   # 데이터 프레임의 columns에 대한 정보
df.shape()  # 데이터 프레임의 형태 row, column 갯수
df.describe()  # 숫자 컬럼에 대한 확률적 설명 (mean, median, min, max)
```

```python
df.nunique()   # 고유한 요소의 수
df.isnull()    # 빠진 값에 대한 결과로 값이 Null이면 True를 반환한다.
```

### 컬럼 선택하기

한개의 컬럼 선택하기

```python
# 한개 컬럼 선택
df['Revenue']

# 한개의 컬럼을 선택한뒤 메서드 적용
df['Revenue'].max()

# 평균을 구한뒤 정수로 변환
round(df['Revenue'].mean())
```

#### 여러개의 컬럼 선택하기

여러개의 컬럼을 중괄호를 사용해 선택할때는 그 안에 리스트의 형태로 컬럼명을 작성해야한다.(더블 중괄호)

```python
df[['Revenue', 'Employees', 'Country']]
```

### `loc` 컬럼 인덱스로 선택하기

`loc`는 라벨이나 위치로 데이터프레임의 행과 열을 선택할 수 있다.
`loc[row_label, column_label]` 와 같이 row, column순으로 입력한다.

```python
df.loc['Apple', 'Revenue'] # Apple row의 Revenue 컬럼값
```

row_label이나  column_label 대신 `:`를 입력하면 해당 컬럼에 대한 모든 값을 가져온다.

```python
df.loc[:, 'Revenue'] # Revenue 컬럼에 대한 모든 row 값
df.loc['Apple', :] # Apple row에 대한 모든 컬럼 값
```

슬라이싱으로 일부분만 선택할 수 있다. 추가적으로 스탭을 줄 수도 있다.
`df.loc[row_label, column_name_start : column_name_stop]`

```python
# 컬럼의 일부를 선택하기 -> Apple의 Revenue부터 Sector컬럼(포함)까지 
df.loc['Apple', 'Revenue':'Sector']

# row의 일부 선택하기 -> Apple부터 Microsoft까지 row 선택하기
df.loc['Apple':'Microsoft', :]
```

스탭 적용하기

df.loc[`row_label`, `column_name_start`:`column_name_stop`:n]
df.loc[`row_name_start`:`row_name_stop`:n , `column_label`]
df.loc[:`, `column_name_start`:`column_name_stop`:n]
df.loc[`row_name_start`:`row_name_stop`:n , :]

### `iloc` 위치로 선택하기

`iloc[row_position, column_position]`

```python
# 1번째 row, 0번째 column
df.iloc[1, 0]

# 1번째 row, 컬럼 전체
df.iloc[1, :]

# 전체 row, 0번째 컬럼
df.iloc[:, 0]
```

## DataFrame Mutation

### 컬럼 만들기

```python
df["Revenue per Employee"] = df["Revenue"] / df["Employees"]

# 단일값 적용
df['Is Tech?'] = "Yes"

# 리스트 값 적용
stock_prices = [143.28, 49.87, 88.26, 1.83, 253.75, 0,
                43.4, 167.32, 89.1, 52.6, 25.58, 137.35, 48.23, 8.81]
df['Stock Price'] = stock_prices
```

### Row 삭제하기

`drop(index)`을 사용해 row를 삭제할 수 있다. immutable 메서드이기 때문에 재할당을 통해 적용할 수 있다.

```python
new_df = df.drop(["Microsoft", "Tencent", "Samsung", "Alphabet", "Meta", "Hitachi", "Apple"])
```

특정 조건에 따라 row 삭제하려면 조건문의 결과에 `.index`를 붙여 해당 조건을 만족하는 row의 인덱스를 가져와서  `drop`메서드의 인자로 넘겨줄 수 있다.

```python
df.drop(df.loc[df["Revenue"] < 80_000].index)
```

### Column 삭제하기

`axis=0` -> row level, `axis=1` -> column level

```python
df.drop(['Revenue', 'Employees'], axis=1)
```

## DataFrame  필터링과 정렬

`sort_index()`  & `sort_values()`

```python
# Employees 컬럼 정렬 (기본 ascending=True)
df.sort_values('Employees')
df.sort_values('Employees', ascending=False)

# 여러개의 컬럼에 대한 정렬
# Country는 descending으로 Employees는  ascending으로 정렬
df.sort_values(by=['Country', 'Employees'], ascending=[False, True])
```

```python
# index 정렬하기
df.sort_index(ascending=False)
```

### `loc`와 `query`로 필터링 선택

```python
df_software = df.loc[df["Country"] == "USA"]
```

```python
df.query("Country == 'USA'")

# USA가 아니고 Consumer Electronics가 아닌 회사
df.query("Country != 'USA' and Sector == 'Consumer Electronics'")

# 여백이 있는 값 사용하기
df.query("`Founding Date` == '04-02-2004'")
```
