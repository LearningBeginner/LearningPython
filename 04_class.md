# Decorator
## What really is a decorator
```py
def wrapper_gen(wrapped_func):
    def wrapper_func(wrapped_func_params):
        # pre-action
        print(1)
        wrapped_func(wrapped_func_params)
        # post-action
        print(2)
    return wrapper_func
def my_func1(arg):
    print(arg)

my_func1 = wrapper_gen(my_func1)
my_func1('this is a test [1]')

# or 

@wrapper_gen
def my_func2(arg):
    print(arg)

my_func2('this is a test [2]')
```
## Adding Flexibility
```py
import functools
def wrapper_gen(wrapped_func):
    @functools.wraps(wrapped_func) ###############
    def wrapper_func(*args, **kwargs):
        # pre action
        wrapped_func(*args, **kwargs)
        # post action
    return wrapper_func
@wrapper_gen
def my_func1(arg):
    print(arg)
@wrapper_gen
def my_func2(arg1, arg2):
    print(arg1, arg2)

my_func1('here1')
my_func2('here2', 'here3')
```
## Decorator with Parameters
```py
def out_wrapper_gen(init_val):
    call_count = init_val
    def in_wrapper_gen(wrapped_func):
        wrapped_func_name = wrapped_func.__name__
        def wrapper_func(wrapped_func_params):
            nonlocal call_count
            print(f">> '{wrapped_func_name}()' has been called {call_count} times.")
            wrapped_func(wrapped_func_params)
            call_count += 1
        return wrapper_func
    return in_wrapper_gen
@out_wrapper_gen(10)
def my_func(arg):
    print(arg)

my_func("what")
```
## Class Decorators of Function
```py
class Power(object):
    def __init__(self, func):
        self._func = func
    def __call__(self, *args, **kwargs):
        ret_val = self._func(*args, **kwargs)
        return ret_val
    def mod(self, *args, **kwargs):
        ret_val = args[0] % args[1]
        return ret_val

@Power
def divide(a, b):
    return a / b

print(divide(16, 5))  # 3.2
print(divide.mod(16, 5))  # 1
```
# @Property, @Setter
```py
class Q:
    def __init__(self, x):
        self.__x = x
    @property
    def x(self):
        return self.__x
    def x(self, x):
        self.__x = x
q1 = Q(100)
print(q1.x)  # 100
q1.x = 200
print(q1.x)  # 200
```
```py
class R:
    def __init__(self, val):
        self.__x = val
        self.__z = None
    @property
    def b(self):
        return self.__x
    @b.setter  ##################
    def a(self, val):
        self.__x = val
        self.__z = val

r1 = R(-100)  # -100, None
print(r1.b)  # -100, None
r1.a = 200  # 200, 200
```