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
> letters = 'abcdefghijklmnopqrstuvwxyz'
> letters_list = [x+y+z for x in letters for y in letters for z in letters]
> ~~~
> {: .python}
>
> Time how long it takes to find 'aaa' in `letters_list`. Next, time how long it takes to find 'zzz' in `letters_list`. 
> Are they the same? Explain your findings?
{: .challenge}

> ## Membership Of A Dict
>
> ~~~
> letters_dict = dict([(x,x) for x in letter_list])
> ~~~
> {: .python}
>
> Time how long it takes to find 'aaa' in `letters_dict`. Time how long it takes to find 'zzz' in `letters_list`. What 
> do you notice? Does it take longer to find 'aaa' in `letters_dict` or `letters_list`? What about 'zzz'? Explain your 
> findings.
{: .challenge}
