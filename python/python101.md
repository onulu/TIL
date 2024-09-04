# Python 101

## 자료형

### String

```py
name = "harry potter"
name = name.title() # Harry Potter
name = name.upper() # HARRY POTTER
name = name.lower() # harry potter
```

문자열에서 변수 사용하기

```py
first_name = "harry"
last_name = "potter"

full_name = f"{first_name} {last_name}" 
# harry potter

print(f"Hello, {full_name.title()}")
#Hello, Harry Potter
```

문자열에서 좌우 공백 제거하기

```py
# 오른쪽 공백 제거
str = 'python  '
str = str.rstrip() # 'python'

# 왼쪽 공백 제거
str = '  python'
str = str.lstrip() # 'python'

# 양쪽 공백 제거
str = '  python  '
str = str.strip() # 'python'
```

### Numbers

숫자형은 소숫점이 없는 integer(정수형), 소숫점이 있는 float(실수형)으로 나뉜다.

```py
2 + 3 # 5
2.0 + 3.0 # 5.0
```

나눗셈에서는 항상 float실수형을 반환하고 정수와 실수를 섞어서 연산하게 되면 연산 결과는 실수형이다.

```py
4 / 2 # 2.0
1 + 2.0 # 3.0
2 * 3.0 # 6.0
```

### List

리스트는 순서가 있는(ordered) 변할 수 있는(mutable) 데이터 콜렉션이다.

```py
# 리스트 생성하기
names = ['harry', 'dumbledore', 'leia']

# 리스트 컴프리핸션 사용
capitalized = [name.title() for name in names] 

# `range`를 사용해 특정 범위의 숫자 배열 만들기
numbers = [n for n in range(10)]

# 리스트 컴프리핸션 + 조건식 사용
even_squares = [x**2 for x in range(9) if x % 2 == 0]
# else를 사용하려면 조건식을 먼저 작성
some_list = [x**2 if x % 2 == 0 else x + 3 for x in range(9)]
```

#### 리스트 수정하기, 요소 추가하기

```py
colors = ['pink', 'blue', 'green']

# 인덱스로 리스트 요소 수정하기
colors[0] = 'yellow'
# ['yellow', 'blue', 'green']

# append 사용해서 리스트 끌에 추가하기
colors.append('violet')
# ['yellow', 'blue', 'green', 'violet']
colors.append('red')
# ['yellow', 'blue', 'green', 'violet', 'red']

# insert 사용해서 특정 위치(index)에 추가하기
colors.insert(0, 'orange')
# ['orange', 'yellow', 'blue', 'green', 'violet', 'red']
```

#### 리스트에서 요소 삭제하기: del, pop, remove

`pop`은 삭제된 요소를 반환한다.
`remove` 메서드는 가장 첫번째로 등장하는 요소에 대해서만 삭제한다. (동일한 값이 여러개인경우 첫번째만 삭제)

```py
# 삭제할 요소의 인덱스값을 알고 있으면 del을 사용해 삭제할 수 있다.
colors = ['pink', 'blue', 'green', 'violet', 'red']

del colors[0]
# ['blue', 'green', 'violet', 'red']

# pop을 사용해 가장 뒤의 요소를 삭제할 수 있다 (stack처럼) 
# 이때 삭제된 요소의 값은 pop에서 반환된다
popped_color = colors.pop() # red

# pop에도 인덱스값을 사용할 수 있다.
popped_color = colors.pop(1) # green

# 삭제하고 싶은 요소의 값을 아는 경우에는 remove 사용
colors.remove('blue')
```

#### 배열 정렬하기: `sort`, `sorted`,`reverse`

`sort`메서드는 원본 배열을 변경하고, `sorted` 함수는 원본 배열을 변경하지 않고 새 리스트를 반환한다.

```py
cars = ['bmw', 'audi', 'tesla', 'mercedes']
cars.sort()
print(cars)
# ['audi', 'bmw', 'mercedes', 'tesla']

cars.sort(reverse=True) #역정렬
print(cars)
# ['tesla', 'mercedes', 'bmw', 'audi']
```

```py
cars = ['bmw', 'audi', 'tesla', 'mercedes']
sorted_cars = sorted(cars)
reverse_sorted_cars = sorted(cars, reverse=True)
print(sorted_cars)
# ['audi', 'bmw', 'mercedes', 'tesla']
```

```py
# 리스트의 순서를 거꾸로 뒤집는다. 
cars = ['bmw', 'audi', 'tesla', 'mercedes']
cars.reverse()
print(cars)
# ['mercedes', 'tesla', 'audi', 'bmw']
```

#### 리스트 활용하기

리스트 순회하기

```py
foods = ['taco', 'burger', 'salad']
for food in foods:
    print(food)
```

리스트 슬라이싱

```py
foods = ['taco', 'burger', 'salad', 'pizza', 'noodle']
print(foods[1:3])
# ['burger', 'salad']

print(foods[:4])
# ['taco', 'burger']

print(foods[-2:])
# 뒤에서 2개 아이템 가져오기
# ['pizza', 'noodle']

print(foods[:-2])
# 뒤에서 2개를 제외하고
# ['taco', 'burger', 'salad']

my_foods[:]
# 리스트 카피
```

리스트 패킹 & 언패킹

```py
# 2. 기본적인 리스트 언패킹
a, b, c = packed_list
print(a, b, c)  # 출력: 1 2 3

# 3. *를 사용한 리스트 언패킹
x, *y = [1, 2, 3, 4, 5]
print(x, y)  # 출력: 1 [2, 3, 4, 5]

*x, y = [1, 2, 3, 4, 5]
print(x, y)  # 출력: [1, 2, 3, 4] 5

# 4. 리스트의 부분 언패킹
first, *middle, last = [1, 2, 3, 4, 5]
print(first, middle, last)  # 출력: 1 [2, 3, 4] 5
```

### Tuple

튜플의 특징

- 불면성: 한 번 생성되면 내용을 변경할 수 없다.
- 순서: 요소들은 특정 순서를 가지며, 인덱스로 접근할 수 있다. (순서가 보장)
- 다양한 데이터 타입 저장 가능: 정수, 문자열, 리스트 등 여러 데이터 타입을 저장할 수 있다.
- `()` 소괄호와 쉼표로 구분된다.
- 패킹과 언패킹: 여러 값을 하나의 튜플로 묶거나, 튜플의 요소들을 개별 변수에 할당할 수 있다.

튜플은 주로 관련된 데이터를 그룹화하거나, 함수에서 여러 값을 반환할때, 또는 데이터의 무결성을 보장해야 할 때 사용된다.

```py
# 튜플 생성
my_tuple = (1, "Hello", 3.14)
one_tuple = (100, ) # 한개의 요소인 튜플을 만들때는 쉼표가 반드시 필요하다.

# 인덱싱
print(my_tuple[1])  # 출력: Hello

# 패킹
packed_tuple = 1, 2, 3  # 괄호는 선택사항입니다
print(packed_tuple)  # 출력: (1, 2, 3)

# 언패킹
a, b, c = packed_tuple
print(a, b, c)  # 출력: 1 2 3

# 언패킹 시 *를 사용하여 나머지 요소 모두 가져오기
x, *y = (1, 2, 3, 4, 5)
print(x, y)  # 출력: 1 [2, 3, 4, 5]

*x, y = (1, 2, 3, 4, 5)
print(x, y)  # 출력: [1, 2, 3, 4] 5

# 튜플은 불변이므로 아래 코드는 오류를 발생시킴
my_tuple[0] = 2  # TypeError: 'tuple' object does not support item assignment
```

### Dictionary

딕셔너리는 키(Key)와 값(Value)의 쌍으로 이루어진 데이터의 모음이다. 딕셔너리는 수정이 가능하며 특히 파이썬 3.7이후부터는 삽입 순서가 유지된다.

```py
# 딕셔너리 생성
person = {'name': 'Harry', 'age': 16, 'city': 'London'}

# 딕셔너리 컴프리핸션
names = ['harry', 'alice', 'bob']
ages = [16, 25, 39]
name_age = {name: age for name, age in zip(names, ages)}
# {'harry': 16, 'alice': 25, 'bob': 39}

# 딕셔너리 컴프리핸션2
ranking = [(1, 'harry'), (2, 'alice'), (3, 'bob')]
student_ranking = {name: rank for name, rank in ranking}
# {'harry': 1, 'alice': 2, 'bob': 3}
```

딕셔너리 활용하기

```python
# 키-값 쌍 삭제하기
del person['city']

# 키 존재 여부 확인
if 'name' in person:
    print(person['name'])

# 키-값 쌍 순회하기
for key, value in person.items():
    print(f"{key}: {value}")

# 키 가져오기
keys = person.keys()
print(keys) # dict_keys(['name', 'age'])

# 값 가져오기
values = person.values()
print(values) # dict_values(['Harry', 16])

# get() 으로 안전하게 값 가져오기
print(person.get('job', 'no job')) # 키가 없는 경우 두번째 인자로 넘겨준 정보 출력

# 딕셔너리 병합하기
details = {'job': 'student', 'major': 'magic'}
person.update(details)

# | 사용해서 병합하기 (3.9버전 부터 가능)
d1 = {'a': 1, 'b': 3}
d2 = {'a': 3, 'c': 4}

print(d1 | d2)
# {'a': 1, 'b': 3, 'c': 4}
d1 |= d2 # d1에 d2를 병합시킨다
print(d1)
# {'a': 1, 'b': 3, 'c': 4}
```

#### 패턴 매칭 - `match/case`

파이썬 3.10버전 부터는 다른 언어의 `switch`와 유사한 `match/case`를 사용할 수 있다.

```python
def match_case(argument):
    match argument:
        case 1:
            return "One"
        case 2:
            return "Two"
        case 3:
            return "Three"
        case _:
            return "Invalid!" # 디폴트

print(match_case(1))
```

시퀀스 매칭

```python
def coordinate_point(point):
    match point:
        case (0, 0):
            return "Origin"
        case (0, y):
            return f"Y-axis, y={y}"
        case (x, 0):
            return f"X-axis, x={x}"
        case (x, y):
            return f"Point ({x}, {y})"
        case _:
            return "Not a point"

coordinate_point((3, 0))    # 'X-axis, x=3'
coordinate_point((1, 2))    # 'Point (1, 2)'
```

조건문을 활용한 매칭

```python
def categorize_age(age):
    match age:
        case n if n < 4:
            return "Toddler"
        case n if 4 <= n < 13:
            return "Kid"
        case n if n >= 13:
            return "Human"

print(categorize_age(3))    # 'Toddler'
print(categorize_age(30))    # 'Human'
```

### Set

set은 고유한 객체의 콜렉션이다. 주로 중복된 요소를 제거하는데 사용되며 요소들은 특정 순서를 갖지 않는다. (순서가 보장되지 않는다)

```python
# set 만들기
s = {1}
s1 = set()  # 빈 셋을 만들때는 {}가 아닌 set()을 사용해야한다.

f = ['apple', 'banana', 'blueberry', 'banana', 'apple']
f_set=list(set(f))
print(f)  # ['apple', 'banana', 'blueberry', 'banana', 'apple']
print(f_set)  # ['banana', 'apple', 'blueberry']
```

셋은 집합의 개념으로 사용될 수 있으며 합집합, 교집합, 차집합 등의 집합 연산이 가능하다.

```python
A = {1, 2, 3}
B = {3, 4, 5}

print(A | B)  # 합집합: {1, 2, 3, 4, 5}
print(A & B)  # 교집합: {3}
print(A - B)  # 차집합: {1, 2}
```

### 함수

```python
def greet(name, age):
    """Greet user"""
    print(f"Hi! {name}, you are {age} years old.")
  
greet('harry', 16)

# Keyword Argument 사용하면 인수의 순서와 상관없이 전달할 수 있다. 두개는 동일하게 호출된다.
greet(name='sam', age=20)
greet(age=20, name='sam')
```

파라미터에 디폴드 값 설정하기

```python
def greet(name, age=1):
    """Greet user"""
    print(f"Hi! {name}, you are {age} years old.")

greet(name='hippy') 
# age에 디폴트 값이 1로 설정되어 있기 때문에 인수로 값을 전달하지 않으면 1을 사용한다.
```

옵셔널 파라미터 설정하기

```python
def gree(name, age=''):
    """Greet user"""
    if age:
        print(f"Hi! {name}, you are {age} years old.")
    else:
        print(f"Hi! {name}.")

greet(name='lulu')
# age는 옵셔널이므로 전달하지 않으면 사용되지 않는다.
```

#### 가변인자 사용하기 - `*args` & `**kwargs`

`*`를 사용해 특정한 인ㅈ자가 아닌 여러개의 임의의 인자를 받을 수 있다.

```python
def make_pizza(*toppings):
    """Print the list of toppings"""
    for topping in toppings:
        print(f"- {toppings}")

make_pizza('pepperoni')
make_pizza('pepperoni', 'cheese', 'pineapple')
```

지정된 인자와 그외의 가변인자를 받도록 작성 할 수도 있다. (넘겨주는 순서에 유의해야함)

```python
def make_pizza(size, *toppings):
    """Print the size and the list of toppings"""
    print(f"Making a {size} pizza with the toppings:")
    for topping in toppings:
        print(f"- {toppings}")

make_pizza('small', 'pepperoni')
make_pizza('large', 'pepperoni', 'cheese', 'pineapple')
# 첫번째 인수는 size가 되고 나머지는 toppings로 전달된다.
```

`**`을 사용하면 키워드 가변인자를 받도록 할 수 있다.

```python
def build_profile(first, last, **user_info):
    user_info['first_name'] = first
    user_info['last_name'] = last
    return user_info

profile = build_profile('harry', 'potter', city='london', major='magic')
print(profile)

# {
#   'city': 'london',
#   'major': 'magic',
#   'first_name': 'harry',
#   'last_name': 'potter'
# }
```

위의 함수에서 `**user_info`는 넘겨받은 키-밸류 쌍을 `user_info`라는 딕셔너리로 만들어 준다.

### Class

파이썬에서 OOP(객체 지향 프로그래밍)은 프로그래밍 구조를 더 모듈화하고 재사용 가능하며 유지 관리하기 쉽게 만드는 중요한 역할을 한다.

- 객체 Object: 데이터와 메소드를 포함하는 독립적인 단위. (객체는 클래스의 인스턴스)
- 클래스 Class: 객체를 정의하는 템플릿. 클래스는 객체의 속성과 메소드로 아루어진다.
- 메소드 Method: 객체가 수행할 수 있는 동작이나 행동을 정의하는 함수.
- 캡슐화 Encapsulation: 데이터와 메소드를 하나의 단위로 묶어 외부로부터 숨기고 제한한다.
- 상속 Inheritance: 하나의 클래스가 다른 클래스의 속성과 메소드를 물려받아 재사용하고 확장하는 방법
- 다형성 Polymorphism: 동일한 인터페이스나 메소드가 다른 클래스에서 다양하게 구현되어 사용될 수 있는 능력
- 추상화 Abstraction: 복잡한 시스템을 단순화하여, 중요한 부분만을 노출

```python
class Animal:
    def __init__(self, name):
        self.name = name

class Dog(Animal):
    def speak(self):
        return f"{self.name}은 멍멍!"

dog = Dog('Hippy')
print(dog.speak()) # Hippy는 멍멍!
```

`__init__`메서드는 특별한 생성자 메서드로 클래스 인스턴스를 생성할때 자동으로 호출된다. 객체의 초기 상태를 설정하는 데 사용되며, 초기화 작업을 수행한다.
(__ 언더스코어가 붙은 메서드는 던더메서드 혹은 매직 메서드라고도 함)

```python
class Person:
    def __init__(self, name, age):
        self.name = name  # 인스턴스 변수 초기화
        self.age = age    # 인스턴스 변수 초기화
```

그외의 매직 메서드

```python
class Person:
    def __init__(self, name, age):
        self.name = name  # 인스턴스 변수 초기화
        self.age = age    # 인스턴스 변수 초기화

    def __str(self):
        return f"{self.name}, {self.age}"
    
    def __repr__(self):
        return f"Person(name={self.name!r}, age={self.age!r})"

    def __eq__(self, other):
        return self.name == other.name and self.age == other.age
```

자식클래스에서 속성와 메서드 정의하기

```python
class Car:
    def __init__(self, make, model, year):
        self.make = make
        self.model = model
        self.year = year

class ElectricCar(Car):
    def __init__(self, make, model, year)
        super().__init__(make, model, year) # 부모 클래스로부터 상속받은 속성들의 초기설정
        self.battery_size = 40  # ElectricCar에서만 사용하는 속성

    def describe_battery(self):
        print(f"This car has a {self.battery_size}-kWh battery.")
```

클래스 컴포지션 - 한개의 클래스에 여러가지 속성이 생기고 메서드가 많아지면 여러개의 클래스로 쪼개서 관리할 수 있다.

```python
class Car:
    --snip--

class Battery:
    def __init__(self, battery_size=40):
        self.battery_size = battery_size

    def describe_battery(self):
        print(f"This car has a {self.battery_size}-kWh battery.")
 
class ElectricCar(Car):
    def __init__(self, make, model, year)
        super().__init__(make, model, year) 
        self.battery = Battery()    # battery속성에는 Battery클래스 인스턴스를 할당한다

my_car = ElectricCar('tesla', 'model x', 2024)
my_car.battery.describe_battery()   # Battery클래스의 describe_battery매서드가 호출된다.
```

Protected Attribute

파이썬에서는 다른 언어(예, 자바)와는 달리 공개되지 않는 프라이빗한 변수를 만드는 방법이 없다. 파이썬에서의 private한 속성은 그저 실수로 덮어쓰는것을 방지하기 위한 예방차원의 조취에 가깝다.

`_변수명`은 파이썬 인터프리터에게는 아무런 의미가 없지만, 컨벤션으로써 암묵적으로 보호받는(외부에서 접근하지 말아야하는) 멤버변수를 의미한다.

```python
class Dog:
    def __init__(self, protected_code):
        self._protected_code =  protected_code

    def get_protected_value(self):  # 직접 접근 대신 메서드로 값을 가져오게 하므로써 값의 수정이나 덮어쓰는것을 방지한다.
        return self._protected_value
```
