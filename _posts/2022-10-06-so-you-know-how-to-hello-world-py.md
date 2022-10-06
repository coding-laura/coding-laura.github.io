---
layout: post
title: So you know how to `hello-world.py`
description: What comes after you learn how to print some output to the console.
image: /post-images/code_screen.png
comments: True
tags: python learning
---

Many times since I first ecountered coding I've seen the good ol' `Hello World` demo. You may have seen it for Java, C, C++, Python, Ruby - everyone does it. And it's a wonderful way to get introduced to a programming language. But what happens next? How much of a Hello-World demo can evolve into a fully functioning script or program? Let me tell you what I've done.

Countless times I've been overwhelmed by the complexity of code when compared to the simplicity of a `hello-world.py` script. With a bit of practice the script below is not difficult to understand but to a Python novice, it can certainly be a "what did I get myself into" kinda moment.

![netmiko-screenshot](/post-images/netmiko_screenshot.png){: .center-image width="65%" }
*from the ktbyers/netmiko repo `netmiko/arista/arista.py`*

So here I am sharing some of the learning milestones I set for myself when learning Python. I don't aim to teach these concepts but to provide you with a learning map to guide your learning.

These milestones have been useful to further my automation journey. They have allowed me to implement repeatable configurations changes, but equally as important, they've allowed me to understand the code that *others* write - *given that their naming conventions, documentation, etc. make sense slol*. 

My hope is these can be applied by anyone looking to get a bit more experienced with Object-oriented Programming (OOP) languages. 

## The Basics

The basics of Python for me include basic [data types](https://www.w3schools.com/python/python_datatypes.asp){:target="_blank"}, conditionals ([if, else, elif](https://www.w3schools.com/python/python_conditions.asp){:target="_blank"}), and flow control statements ([while loop](https://www.w3schools.com/python/python_while_loops.asp){:target="_blank"}, [for loop](https://www.w3schools.com/python/python_for_loops.asp){:target="_blank"}).

Once I understand these topics I can move on to more complex concepts such as functions, methods, and classes.

## Functions

[A function](https://www.freecodecamp.org/news/python-functions-define-and-call-a-function/){:target="_blank"} is a block of code within a script that completes some action. It can alter the content of some variables, it can use exisiting data to build something new, or in some cases it can just do nothing. A function is a good way to segment and organize your code in a way that the block has a specific purpose and can be reused.

There are multiple ways to write a function, here's one of them: 

```python
# this is a function called add that accepts two parameters
def add (a, b):
    return a+b
# end of function

# calling the function
sum = add (5,4)
print (sum)

# Output: 9
```

## Data Structures

Data structures are just ways to store data. I consider them a bit more complex than the standard data types - such as Strings and Integers, etc.. No need to learn them all but I recommend learning about [Lists](https://www.geeksforgeeks.org/python-lists/){:target="_blank"} and [Dictionaries](https://www.geeksforgeeks.org/python-dictionary/){:target="_blank"}, both Python constructs.

Here's an example of a Dictionary: 

```python

# create a dictionary of interfaces (key) and their respective descriptions (value)
interface_descriptions = { "Ethernet1": "Host1 NIC1", "Ethernet2": "Host2 NIC1" }

# print the whole dict
print (interface_descriptions)

# print the value of the key that matches Ethernet1
print (interface_descriptions["Ethernet1"])

# Output: {'Ethernet1': 'Host1 NIC1', 'Ethernet2': 'Host2 NIC1'}
# Output: Host1 NIC1

```

These are useful to store data I may want to send to a device or build a report off of. Dictionaries are a very similar to JSON if you think about it, may come in handy for API calls.

Other data structures can be Sets and Tuples.

## Objects

By now I know variables, for loops, if statements and I'm ready to start understanding why engineers build scripts with keywords such as `class`. 

To understand objects you may need to understand classes. A Class is an OOP construct which is a fancy term for a blueprint. A class has methods (the class word for functions) and attributes (the class word for variables). An object is an instance of a class. Objects are the manifestation of [OOP](https://www.programiz.com/python-programming/object-oriented-programming){:target="_blank"}.

```python

# This is a blueprint for arithmetic operations such as addition and multiplication 
class Maths():
    def add (self, a, b):
        return a+b
    def multiply (self, c, d):
        return c*d

# notebook is an object, an instance of the class Maths
notebook = Maths()

# notebook then gains access to all the functions defined on the class Maths 
# but with the option to pass its own data
print("The sum is", notebook.add( 7, 9 ) )
print("The product is", notebook.multiply( 7, 9 ) )

# Output: The sum is 16
# Output: The product is 63
```

**Note:** `self` is a standard naming convention for the first argument in a method. It should always be added to all methods in a class. It's a Python thing that I don't believe it worth of further exploration, trust me. You just add it as a hardcoded thing.

## Modules

Modules are a way to not have to re-invent the wheel. If someone has written a program that handles mathematical functions, then you can import it and use the functions defined on those files rather than having to write those processes on your own. The example below uses a module that implements regex functionalities, such as identifying regex patterns.

```python
# re is the module for Regex
import re

# escape is a re function that allows you to identify special characters
# and it adds the escape (backslash) character to each occurence
print(re.escape( '(config)#' ))

# Output: \(config\)\#

```

Python is full of modules, either built-in with your copy of Python (e.g. [re](https://docs.python.org/3/py-modindex.html){:target="_blank"}) or downloadable (e.g. [netmiko](https://pypi.org/project/netmiko/){:target="_blank"}). I had a friend once try to manually format a dictionary into JSON or something along those lines. He ended up finding a module that did it for him - hours saved and headaches prevented.

## Projects

Lastly, build something. Come up with a small idea to script out. Maybe save a device's config on a text file and parse it while looking for a specific pattern. Improve on it by using SSH and getting the data directly from a device.

There is this concept of `pseudo-code` which basically means: write out in plain speech what you want the actual code to do. This helps to write the code later on.

```
First open the file containing the config output
Then parse it.
Match content of the line to pattern "ntp"
If found print a message saying NTP is configured
If not found print a message saying NTP is missing from the config
Done
```

You will find that working on a project will inspire you to think about the problem and the solution. Google is my friend for projects like this. 

## Resources

FreeCodeCamp #python Articles - [here](https://www.freecodecamp.org/news/tag/python/){:target="_blank"}

RealPython Tutorials - [here](https://realpython.com/){:target="_blank"}

Codecademy Python for Programmers course - [here](https://www.codecademy.com/learn/python-for-programmers){:target="_blank"}

($) Udemy Learn to Code with Python - [here \$](https://www.udemy.com/course/learn-to-code-with-python/){:target="_blank"} (*wait for it to go on sale*)

W3Schools Python Tutorial - [here](https://www.w3schools.com/python/default.asp){:target="_blank"}


## Conclusion

These milestones will not teach everything there is to know about Python. But they do provide the building blocks to start putting together purposeful scripts.

In the future I hope to share examples of code that I find in the wild and how I go about understanding what it does - which consequently allows me to use it on my own code going forward. The secret is Google.

Feel free to share with me your own processes and techniques for learning a programming language.