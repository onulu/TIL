# 클로져와 데코레이터

클로저는 자신을 둘러싼 상태(렉시컬 환경)에 대한 참조를 기억하는 함수이다. 파이썬에서 클로저는 중첩함수에서 외부 함수의 실행이 끝난 후에도 외부 범위의 변수를 기억하고 접근할 수 있는 특별한 기능이다.

클로저는 마치 작은 '데이터 저장소' 혹은 '특별한 가방'을 가진 함수라고 생각할 수 있다. 나중에 함수가 실행될 때 이 정보를 사용할 수 있다.


```python
def outer(x):
    def inner(y):
        return x
    return inner

closure = outer(10)
print(closure(20))  # 10
```

클로저가 유영한 경우

- 데이터의 은닉, 보호
- 콜백 함수의 활용
- 데코레이터
- 메모아이제이션

> 렉시컬 환경이란 코드가 실행된 환경이 아닌 코드가 작성된 환경을 의미한다.
> 이는 소스 코드에서의 위치를 기준으로 중첩된 함수에서 변수가 어떻게 해결되는지를 의미한다.

## Decorators

데코레이터는 다른 함수를 인수로 받아 그 함수이 동작을 확장하는 함수이다. 데코레이터는 원래 함수의 코드를 수정하지 않고도 그 동작을 변경하거나 확장할 수 있게 해준다.

  ```python
  import time

  def elapsed(func):
      def wrapper(*args, **kwargs):
          start = time.time()
          result = func(*args, **kwargs) # pass the arguments to the function
          end = time.time()
          print(f"Elapsed time: {end - start}")
          return result
      return wrapper


  @elapsed
  def func():
    print("Running myfunc")
  
  func()
  # @elapsed => func함수는 elapsed함수에 의해 감싸져서 실행된다.
  # elapsed(func)() 와 동일한 문법적 설탕임.
  ```

```python
# Memoization and decorator

def memoize(func):
    cache = {}
    def wrapper(n):
        if n not in cache:
            cache[n] = func(n)
        return cache[n]
    return wrapper

@memoize
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)

print(fib(100))
```
