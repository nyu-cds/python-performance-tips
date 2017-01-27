---
title: "Import Overhead"
teaching: 5
exercises: 5
questions:
- "What impact does the import statement have on program performance?"
objectives:
- "Show the different ways import can be used."
- "Explain how import can affect program performance."
keypoints:
- "The location of the import statment can impact performance."
- "Avoiding using import is a good strategy."
---
Import statements can be executed just about anywhere. It's often useful to place them inside functions to 
restrict their visibility and/or reduce initial startup time. Although Python's interpreter is optimized 
to not import the same module multiple times, repeatedly executing an import statement can seriously affect 
performance in some circumstances.

The following two functions do the same thing, the only difference is the location of the import statement.

~~~
def func1():
    import string
    string.lower('Python')

import string
def func2():
    string.lower('Python')
~~~
{: .python}

Note that using string methods avoids the need to import at all, and runs even faster.

~~~
def func3():
    'Python'.lower()
~~~
{: .python}

> ## Different Import Location
>
> Compare the execution of the `func1` and `func2` by timing how long it takes to run each 10000 times.
{: .challenge}

> ## Avoid Import
>
> Try executing the `func3` function 10000 times and see how long it takes.
{: .challenge}