---
title: "Decorator Caching"
teaching: 5
exercises: 5
questions:
- "How can I use a decorator to improve the performance of a function?"
objectives:
- "Introduce the notion of a decorator in Python."
- "Show how a decorator can be used to cache intermediate results."
keypoints:
- "Decorators are an important part of Python."
- "Decorators can be used for a variety of different purposes."
- "Caching is one way to improve performance."
---

The symbol `@` is Python decorator syntax. Python decorators are normally used for tracing, locking, or logging. 
However, you can also decorate a Python function so that it remembers the results needed later. See the [`functools` 
documentation](https://docs.python.org/2/library/functools.html#functools.wraps) for more information on creating 
and using decorators.

The following function computes the `i`th fibonacci number for a given value of `i`. 

~~~
def fib(i):
    if i < 2: return 1
    return fib(i-1) + fib(i-2)
~~~
{: .python}

Using the following code, we can create a decorator that saves each intermediate value in memory rather than 
calculating it every time.

~~~
from functools import wraps
def cache(f):
    cache = { }
    @wraps(f)
    def wrap(*arg):
        if arg not in cache: cache[arg] = f(*arg)
        return cache[arg]
    return wrap
~~~
{: .python}

> ## Using A Decorator For Caching
>     
> Time how long it takes to find `fib(20)`. Now time how long the same `fib` function takes if it is decorated with @cache.
> Can you explain what is happening?
{: .challenge}