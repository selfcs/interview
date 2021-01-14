## 1. 谈一谈装饰器（decorator）

装饰器的本质也是一个函数。它可以让其它函数在不作任何变动的情况下增加额外功能，装饰器的返回值也是一个函数对象。它可以让其它函数在不作任何变动的情况下增加额外功能，装饰器的返回值也是一个函数对象。

```python
def use_logging(func):

    def wrapper():
        logging.warning("%s is running" % func.__name__)
        return func()   # 把 foo 当做参数传递进来时，执行func()就相当于执行foo()
    return wrapper

def foo():
    print('i am foo')

foo = use_logging(foo)  # 因为装饰器 use_logging(foo) 返回的时函数对象 wrapper，这条语句相当于  foo = wrapper
foo()                   # 执行foo()就相当于执行 wrapper()

# WARNING:root:foo is running
# i am foo
```

```python
import logging


def use_logging(func):
    def wrapper():
        logging.warning("%s is running" % func.__name__)
        return func()

    return wrapper

@use_logging
def foo():
    print("i am foo")

foo()

# WARNING:root:foo is running
# i am foo
```