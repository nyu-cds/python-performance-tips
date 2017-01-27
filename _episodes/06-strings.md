---
title: "String Concatenation"
teaching: 5
exercises: 5
questions:
- "How is it possible to improve the performance of strings in Python?"
objectives:
- "Learn the implications of immutable objects."
- "See other ways to perform string operations."
keypoints:
- "The immutability of strings can be a performance penalty."
- "There are alternatives to common string operators like '+'"
---

Strings in Python are immutable, which has some advantages and disadvantages. This attrbute means that 
strings can be used as keys in dictionaries and individual copies can be shared among multiple 
variable bindings. (Python automatically shares one- and two-character strings.) However the 
disadvantage is that you can't say something like, "change all the 'a's to 'b's" in any given 
string. Instead, you have to create a new string with the desired properties. This continual 
copying can lead to significant inefficiencies in Python programs because it means using the 
'+' or '+=' operators may build new strings for each intermediate step.

~~~
def make_string(a_list):
    mystring = ''
    for x in a_list:
        mystring += x
    return mystring

mylist = [x for x in 'abcdefghijklmnopqrstuvwxyz']
~~~
{: .python}

Strings have their own inbuilt operators. Clever usage of these operators can sometimes help avoid
the overhead of continual copying. For example, strings have a `join` operator that allows statements
such as `'this string '.join(['a string', 'b string'])`. Since `join` takes an iterable as an argument
it is effectively doing the same thing as the loop above. We can replace this code with the following:

~~~
''.join(mylist)
~~~
{: .python}

> ## String Performance
>
> Time how long it takes to call `make_string` with `mylist`. Now time how long it takes to 
> create the same string using `join`. Explain how the `join` operation works.
{: .challenge}