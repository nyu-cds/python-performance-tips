---
title: "Introduction"
teaching: 5
exercises: 0
questions:
- "Why is Python slower than compiled languages like C and C++?"
objectives:
- "Explain the key differences between Python and compiled languages."
- "Explain what a dynamic language is."
keypoints:
- "Python is a dynamic interpreted language."
- "The flexibility of dynamic languages comes at a cost in terms of performance."
- "There are ways to improve the performance of Python, but it will never be as fast as compiled languages."
---
Python is a dynamic interpreted language. The "dynamic" part means that the types of variables, 
functions arguments, etc. are not known until the program runs. An interpreted language is one 
that is directly executed, or compiled to bytecode for an abstract machine, rather than being 
compiled to the native object code and executed on a computer system. Python takes the second 
approach, and compiles the source to bytecode (*.pyc files) which is then interpreted by the 
Python interpreter (CPython).

While dynamic interpreted languages have great flexibility, they also suffer from significant 
performance limitations when compared to languages that compile directly to native object code. 
There are two primary reasons for this. The first is due to the dynamic nature of the language. 
Because the types of Python objects (variables, function arguments, etc.) are not known until 
the program is run, it is very difficult to optimize the interpreter, since it is not possible 
to know what the bytecode is going to do before it is executed. The second issue is that the 
bytecode generated from compiling Python is targeted at a Python Virtual Machine (PVM), not 
at the hardware that the program is running on. The Python interpreter must convert the PVM 
instructions into hardware instructions in order to execute the bytecode. This coversion is 
always going to carry some overhead, and is why languages such as Java are always somewhat 
slower than native languages such as C or C++.

A good analysis of the Python interpreter is available [here](http://akaptur.com/blog/2013/11/15/introduction-to-the-python-interpreter).

Although Python is a relatively slow language, that doesn't stop it from being useful for high
performance computing or for Data Science applications. There are a variety of techniques that 
can be used to improve performance, and we will be covering some of these here. A good reference
for these and other performance tips is the [PythonSpeed PerformanceTips wiki](https://wiki.python.org/moin/PythonSpeed/PerformanceTips).