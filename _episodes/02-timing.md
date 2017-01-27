---
title: "Timing Python Code"
teaching: 5
exercises: 5
questions:
- "How can I tell how long my python code takes to run?"
objectives:
- "Explain how to time Python programs and snippets of Python code."
keypoints:
- "There are a variety of ways to time Python code."
- "The best way depends on what environment you are using."
---
In order to evaluate the usefulness of these performance improvement techniques, 
we are going to be timing how long it takes run snippits of code. While this does 
not provide an accurate measure of the performance, it does give an idea of the 
relative improvement (or decrease) in performance.

Python provides the [timeit module](https://docs.python.org/2/library/timeit.html)
for measuring the execution time of small code snippits. This can be called from 
the command line, or by importing it into an exisiting program.

~~~
import timeit
def my_function():
    y = 3.1415
    for x in range(100):
        y = y ** 0.7
    return y

print timeit.timeit(my_function, number=100000)
~~~
{: .python}

The `timeit` function will run the code a set number of times (in this case 100000) 
and then report how long it took to run (in seconds). So to find out how long it 
took to run once, divide the result by 100000. The repeat function can be used to 
perform multiple runs if desired (default 3) and report the result for each run.

If you are using IPtyhon, an even easier method is to use the `%timeit` or `%%timeit`
magic functions. These do essentially the same thing as the timeit module. The 
`%timeit` magic function is documented [here](http://ipython.readthedocs.org/en/stable/interactive/magics.html?highlight=timeit#magic-timeit).

> ## Be Careful When Mixing Both Techniques
>
> Note that the `timeit` function requires you to pass only the name of the function 
> (in this case `my_function`) while the `%timeit` magic command requires the function 
> call `my_function()` itself. Using only the function name for `%timeit` will result 
> in incorrect timing results.
{: .callout}

> ## Try It Out
>
> Run the above example, then use the `%timeit` magic function to time the function using the same 
> number of loops. Why do you think there is a difference in the results (hint: read the documentation.)
>
> > ## Solution
> > ~~~
> > import timeit
> > def my_function():
> >     y = 3.1415
> >     for x in range(100):
> >         y = y ** 0.7
> >     return y
> > 
> > print(timeit.timeit(my_function, number=100000) / 100000)
> > ~~~
> > {: .python}
> > ~~~
> > 6.944025074999445e-06
> > ~~~
> > {: .output}
> > ~~~
> > %timeit -n 100000 my_function()
> > ~~~
> > {: .python}
> > ~~~
> > 100000 loops, best of 3: 7.01 µs per loop
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}