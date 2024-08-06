# 익명함수 람다

파이썬에서 `lambda` 키워드는 익명함수를 생성할 수 있게 해준다. 이때 익명함수의 몸체에는 표현식만 사용할 수 있으며 while, try등의 구문을 사용할 수 없다.

`람다`는 변수에 할당할 필요 없이 함수를 사용할 수 있게 해주어 익명함수라고도 불리며 다른 함수에 인수로 전달하기 위해 사용할 수 있다. 람다는 한번 사용하고 버려지는 경우 (sorted, map, filter등에 인수로 전달되는 경우)에 유용하며 그외에는 `def`를 사용하는 것이 바람직하다.

(함수를 인수로 전달 받는 함수를 고차함수라고 하며 파이썬 빌트인 함수에는 `map`, `sorted`, `filter`, `reduce` 등이 있다.)

```py
# 각가의 단어를 거꾸로 뒤집었을때의 순서대로 정렬하라.
fruits = ['strawberry', 'fig', 'apple', 'cherry', 'raspberry', 'banana']
sorted(fruits, key=lambda word: word[::-1])
# “['banana', 'apple', 'fig', 'raspberry', 'strawberry', 'cherry']”
```
