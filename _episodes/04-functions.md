---
title: "Function Call Overhead"
teaching: 5
exercises: 5
questions:
- "Do functions affect my program's performance?"
objectives:
- "See the impact of functions on program performance."
- "Learn ways of improving performance by eliminating function call overhead."
keypoints:
- "Functions have a lot of overhead in Python."
- "It is possible to reduce this overhead without sacrificing readability."
---

Function call overhead in Python is relatively high, especially compared with the execution speed of builtin functions. 
The overhead in Python is mainly due to the dynamic type checking of function arguments that must be performed before 
and after the function call. This strongly suggests that, where appropriate, functions should handle data aggregation 
rather than being called on a per element basis.

In the following example, the function `inner` is called for each element in the list. The overhead of the function call 
and the argument checking is multiplied 100000 times.

~~~
x = 0
def inner(i):
    global x
    x = x + i
    
def outer_1():
    for i in range(100000): 
        inner(i)
~~~
{: .python}

In the next example, the loop is moved inside the `aggregate` function so that the function is only called once 
instead of 100000 times.

~~~
x = 0
def aggregate(list):
    global x
    for i in list:
        x = x + i

def outer_2():
    aggregate(range(10000))
~~~
{: .python}

> ## Check Results
>
> Does moving the function call result in faster execution? Time how long it takes to run the `outer_1` and
> `outer_2` functions. Is there any difference?
>
> In the second example, there is still function call overhead every time `outer_2` is called. Modify the 
> function to eliminate this overhead, then time the resulting execution. Is it improved? What effect does this
> have on the program's readability?
{: .challenge}
