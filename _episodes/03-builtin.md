---
title: "Built-in Functions"
teaching: 10
exercises: 10
questions:
- "How can I speed up my function?"
objectives:
- "Explain how built-in functions can be used to speed up your code."
- "Learn how intrinsic operators can be used to replace user defined functions."
keypoints:
- "Using built-in functions and intrinsic operators is much more efficient."
---
One of the easiest ways to improve Python performance is not to execute any 
Python code at all! Python provides a large number of built-in functions 
that perform a wide variety of operations. These built-in functions are written in C, 
and so are generally very fast. See the Python documentation for a list of the available 
functions.

In the code below, the function called `my_min` takes a list of integers as an argument 
and finds the minimum value.

~~~
def my_min(values):
    min_value = values[0]
    for v in values:
        if v < min_value:
            min_value = v
    return min_value

import random
random_numbers = [random.randint(0,1000) for p in range(0,1000)]
my_min(random_numbers)
~~~
{: .python}

However, Python already provides a `min` function that can be used instead. So, the above code
could have been written as:

~~~
import random
random_numbers = [random.randint(0,1000) for p in range(0,1000)]
min(random_numbers)
~~~
{: .python}

Another performance improvement is to use _intrinsic operators_ (+, -, *, etc.)
instead of a user defined function. The operator module exports a set of 
efficient functions corresponding to the intrinsic operators of Python. For example, 
`operator.add(x, y)` is equivalent to the expression `x+y`. See the 
[Python documentation](https://docs.python.org/2/library/operator.html#module-operator)
for a list of standard operators.

Suppose we need to calculate the sum of 1000000 pairs of random numbers. We might consider
using the `map` function as follows:

~~~
random_numbers = [random.randint(0,1000) for p in range(0,1000000)]
random_numbers2 = [random.randint(0,1000) for p in range(0,1000000)]

res=list(map(lambda x,y: x+y, random_numbers, random_numbers2))
~~~
{: .python}

On the surface, this looks fine. However `map` is calling our function for every pair of numbers. Since
our function is simple, we could just replace it with the appropriate intrinsic operator as follows:

~~~
import operator
res=list(map(operator.add, random_numbers, random_numbers2))
~~~
{: .python}

> ## Why Use List?
>
> Why do we convert the map to a list in the above code? In Python 3.5, the map function returns an iterator
> that does not evaluate the arguments until it needs to. By converting the iterator to a list, we
> are forcing map to compute every value.
{: .callout}

> ## Check Results
>
> 
> Check how long the `my_min` function takes compared to the built-in `min` function. Which performs the best?
>
> Check how long it takes for each of the `map` statements to run. Which performs the best?
{: .challenge}