---
title: "Membership Testing"
teaching: 5
exercises: 5
questions:
- "What is the best datatype to use when searching for elements?"
objectives:
- "Learn how dicts, sets, lists, and tuples are stored."
- "See the best way to find elements in a datatype."
keypoints:
- "Dicts and sets are fast when looking up elements."
- "Be mindful of the datastructures you use as it can have a big impact on performance."
---

Python provides the `in` operator to check if an element exists in a collection (`not in` to test
the opposite). The `in` operator is very fast at checking if an element exists in a dict or a set,
because both dict and set are implemented using a hash table. Although this seems an 
obvious choice of data structure for a dict, it is not so obvious that a set would 
also use a hash table. 

Checking for membership in a list or tuple is not as effecient, as each element must be checked
in turn. Therefore, if you need to check membership very often, use dict 
or set as your container rather than searching a list.

> ## Membership Of A List
>
> ~~~
> letters = [x for x in 'abcdefghijklmnopqrstuvwxyz'*1000+'%']
> ~~~
> {: .python}
>
> Time how long it takes to find 'a' in `letters`. Next, time how long it takes to find '%' in `letters`. 
> Are they the same? Why?
{: .challenge}

> ## Membership Of A Set
>
> ~~~
> letters = set('abcdefghijklmnopqrstuvwxyz'*1000+'%')
> ~~~
> {: .python}
>
> Time how long it takes to find 'a' in `letters`. Time how long it takes to find '%' in `letters`. What 
> do you notice?
{: .challenge}
