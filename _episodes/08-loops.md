---
title: "Optimizing Loops"
teaching: 10
exercises: 5
questions:
- "What are the main factors affecting the speed of Python loops?"
objectives:
- "Learn why loops are so important to performance."
- "Discover ways to improve the performance of loops."
- "See what options are available to replace loops."
keypoints:
- "Anything in a loop is going to be executed many times."
- "Even small factors can add up if they are in a loop."
- "There are a variety of ways to do things in Python without using loops."
---
It is important to realize that everything you put in a loop gets executed for every loop iteration. 
They key to optimising loops is to minimize what they do. Even operations that appear to be very fast
will take a long time if the a repeated many times. Executing an operation that takes 1 microsecond a 
million times will take 1 second to complete. Even something as innocuous as using the '.' notation can 
add extra overhead. Lets look at the '.' notation in a bit more detail.

The following code creates a list of the same words in lowerlist but first converts them to uppercase.

~~~
import random
lowerlist = ['abcdefghijklmnopqrstuvwxyz'[:random.randint(0,25)] for x in range(1000)]
upperlist = []
​
def to_upper_1():
    for word in lowerlist:
        upperlist.append(str.upper(word))
        
to_upper_1()
~~~
{: .python}

Notice that the loop is calling two methods `upperlist.append` and `str.upper`. Since these methods are called many
times, any tiny overhead eventually adds up. What does '.' do anyway? The '.' operator is how an instance attribute is
referenced. Although you would think this would be fast, Python must support dynamic attributes as well as multiple
namespaces.  This means that the dot operator does a lot more than you might think.

We can demonstrate this by first saving the actual methods referred to by `str.upper` and `upperlist.append` into 
separate variables and replace the calls to these functions with the variable names. In this way,
we avoid the overhead of searching:

~~~
upper = str.upper
append = upperlist.append

def to_upper_2():
    for word in lowerlist:
        append(upper(word))
        
to_upper_2()
~~~
{: .python}

In this example, the `upperlist`, `upper` and `append` variables are global. Another optimization for the 
loop version is to use local variables rather than global variables as these can be accessed much 
more efficiently in Python.

~~~
def to_upper_3():
	upperlist = []
	upper = str.upper
	append = upperlist.append
    for word in lowerlist:
        append(upper(word))
    return upperlist
        
upperlist = to_upper_3()
~~~
{: .python}

The problem now is that this code is much more difficult to understand! Optimizing code may result in 
performance improvements, but it often comes at a cost.

Another way to speed up loops is to remove the looping stucture altogether. If the body of the 
loop is simple, the interpreter overhead of the `for` loop itself can be a substantial amount of 
the overhead. This is where the `map` function is handy. You can think of `map` as a `for` loop moved 
into C code. The only restriction is that the "loop body" of `map` must be a function call. 

~~~
upperlist = map(str.upper, lowerlist)
~~~
{: .python}

The same loop can also be written with a list comprehension. You can use list comprehension to replace 
many `for` and `while` blocks. List comprehension is  faster because it is optimized for the Python 
interpreter to spot a predictable pattern during looping. Besides  the syntactic benefit of list comprehensions, 
they are often as fast or faster than equivalent use of `map`.

~~~
lowerlist = ['abcdefghijklmnopqrstuvwxyz'[:random.randint(0,25)] for x in range(1000)]
upperlist = [str.upper(x) for x in lowerlist]
~~~
{: .python}

> ## Check Timings
>
> Try timing the `to_upper_1()`, `to_upper_2()`, and `to_upper_3()` functions and see the difference. Which
> function is the fastest?
{: .challenge}

> ## Using The `map` Function
>
> Rewrite the loop using the `map` function and time how long it takes to execute. Is this faster than
> the function versions?
{: .challenge}


> ## Using A List Comphrehension
>
> Rewrite the loop using a list comprehension and time how long it takes to execute. Is this faster than
> the function and `map` versions?
{: .challenge}
