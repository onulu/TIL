# 클로져와 데코레이터

A closure is a function bundled together with references to its surrounding state (lexical environment). A closure in Python is a function that remembers and can access variables from its outer(enclosing) scope even after the outer function has finished executing.

```python
def outer(x):
    def inner(y):
        return x
    return inner

closure = outer(10)
print(closure(20))  # 10
```

Closures are useful

- for data privacy
- for callback functions
- for decorators
- for memoization

> Lexical environment is the environment in which the code is written.
> It refers to how variable names are resolved in nested functions based on their location in the source code.

## Decorators

Decorator is a function that takes another function and extends its behavior **without explicitly modifying it**.

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
  # func will be wrapped by elapsed function by the @elapsed syntax
  # it's same as calling elapsed(func)()
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
