---
sidebar_position: 2
---

# Functions and Methods

So far, we have explored different types that represent *data*, like numbers, text, and lists.

A *function* is a type of object that represents arbitrary *code*, a *process*.

Similar to functions in mathematics, they accept input variables (called *arguments*) and often (but not always) return an output value. You can think of functions as mini-scripts that run inside of your main Python script.

## Defining Functions

While functions are objects, they are not assigned to variables using the standard [assigment statement](./statements.md#assignments). Instead, the `def` keyword is used. A typical function definition looks like this:
```python
def my_function(my_param1, my_param2):
    suite
```
Here, `my_param1` and `my_param2` act as parameters, whereas `suite` is one or more statements that will be executed when the function (named `my_function`) is [called](./functions.md#calling-functions). *Calling* is the term used to describe the act of "running" a function.

:::warning
**Indentation is important.**

The way python determines whether something is part of a `suite` or not is *indentation*. The [official Python style guide](https://peps.python.org/pep-0008/) recommends 4 spaces per level of indentation, but any number of spaces counts (as long as it is consistent).

```python
def print_stuff():
    print("I'm in the suite, and therefore a part of the print_stuff function")
    print("I am also in the suite")
print("I'm outside of the suite, I have nothing to do with print_stuff.")
```
:::

Parameters can be thought of as variables that will be assigned later, when the function is *called*. They are accessible by every statement that makes up the `suite`, but are not accessible outside of that. Parameters are used to define the inputs of your function. To illustrate this point, let's define a function that raises a number to the power of three:

```python
def power_of_three(x):
    return x ** 3
```
Here, we have defined a function named `power_of_three`. 

It has one parameter, `x`. 

The `suite` of this function is `return x ** 3`. As you can see, `x` is treated as a variable inside of the `suite`. The `return` keyword is special statement used inside of functions. Whatever expression is placed after `return` is what the function will use as an output. So in this case, the output of `power_of_three` given some value `x` is `x ** 3`. 

When called, `power_of_three` will be provided a value for `x`, and that value is what will be bound to the name `x` inside of the `suite`. So if `power_of_three` is called with a value of `3` for `x`, you can imagine that before the `suite` is run, `x = 3` is run, like so:
```python
x = 3
return x ** 3
```
And once `x ** 3` is evaluated, `power_of_three` will return an output of `27`. 

A `suite` can be multiple statements. The function will end once it reaches the first `return` statement it lands on, or when it reaches the end of the `suite`.

```python
def complicated_function(x, y):
    a = x ** y
    b = x + y + 5
    c = x // y
    print("done!")
    return a * b * c # Anything after this will NOT run, because it is after the return statement.
    print("unreachable") # will never run

print("Hello!") # This WILL run, because it is not a part of complicated_function at all. 
```
This function defines extra variables `a`, `b`, and `c` to make calculations easier before returning its output. Note that much like parameters (in this case, `x` and `y`), all variables declared inside of a function can only be access inside of that function. `a`, `b`, and `c` do not exist outside of `complicated_function`.


## Calling functions

Once a function is defined, it will do nothing until it is called. A function can be called any number of times within your Python script.

Take the `power_of_three` example once more.

```python
def power_of_three(x):
    return x ** 3
```

Once this statement is run, a new `power_of_three` function variable is created and ready to be called. Note that **nothing inside of the function is run yet**.

To call `power_of_three`, simply use the name of the function follow by parentheses (`()`). Inside of the parentheses is where you pass your *arguments*, that is, the values you want to assign to function parameter.

:::info
**Arguments vs Parameters**

These two terms represent the same concept (input variables to functions), but they are used in different contexts.
When *defining* a function, the input variables (the names located inside the `()` brackets) are called *parameters*.
When *calling* a function, the input variables (the values you put inside the `()` brackets) are called *arguments*.
:::

Let's say I want to know what 4 to the power of three is. I can write:
```python
power_of_three(4)
```
This calls the `power_of_three` function, and automatically assigns the value of 4 to the `x` parameter defined in the `suite`. Then the suite is run to completion, returning the desired output.

Function calls are [expressions](./statements.md#expressions), which means they can be used as a value. For example, if I want to store the result of `power_of_three` I can write:
```python
four_cubed = power_of_three(4)
```
`power of three` can be called more than once. Each time `power_of_three` is called, it has no memory of previous parameters, only the current one:
```python
one_cubed = power_of_three(1) # => 1
two_cubed = power_of_three(2) # => 8
three_cubed = power_of_three(3) # => 27

```

### Built-in functions

Python comes with many built-in functions already defined and ready to use. You are probably already familiar this one: `print`. `print` is a function that takes any number of arguments and returns nothing. Instead, it converts all of its parameters into `string`s and prints them to the output console (usually, your terminal).

Here are some common built-in functions:

#### General functions

| function | parameters | returns |
| --- | --- | --- |
| `print(obj...)` | `obj`: any number of objects | Nothing, but prints a string representation of all `obj`s to the console |
| `input(prompt)` | `prompt`: A string prompt to print to the console before accepting input| First, this function will print `prompt` tp the console. Then, it will read all keypresses from the console until the enter key is pressed. Then, it returns all keys pressed up until that point as a `string`. |
| `type(obj)` | `obj`: any object | The type of `obj` as an object of type `type` |


#### Type functions

These are used to convert objects from one type to another
| function | parameters | returns |
| --- | --- | --- |
| `bool(obj)` | `obj`: any object | Either `True` or `False`, depending on its [truthiness value](./statements.md#truthiness) |
| `int(obj)` | `obj`: any object, usually a string or number | An integer representation of `obj` (if it's a string, the number represented by the string). Throws an error if it cannot convert `obj` to an integer |
| `float(obj)` | `obj`: any object, usually a string or number | An float representation of `obj` (if it's a string, the number represented by the string). Throws an error if it cannot convert `obj` to a float |
| `str(obj)` |  `obj`: any object | A string representation of `obj` | 
| `tuple(obj)` | `obj`: any *iterable* obj (usually a sequence type) | a tuple respresentation of the given sequence object `obj` |
| `list(obj)` | `obj`: any *iterable* obj (usually a sequence type) | a list respresentation of the given sequence object `obj` |
| `range(stop)` | `stop`: an integer representing the end of the sequence. | A `range` object, which starts at `0`, ends before `stop`, and step size of `1` |
| `range(start, stop, step)` | `start`: an integer representing the start of the sequence. <br/> `stop`: an integer representing the end of the sequence. <br/>`step`(optional): an integer representing the "step size" of the sequence | A `range` object, which starts at `start`, ends before `stop`, and step size of `step` |

#### Sequence functions

These are functions that mostly take in [sequence type](./data-types#sequence-types) objects as arguments.

| function | parameters | returns |
| --- | --- | --- |
|`len(seq)` | `seq`: a sequence-type object | The length of `seq` (i.e. how many elements `seq` has) |
| `sorted(seq)` | `seq`: a sequence-type object usually having **all** elements of the same type | A `list` with all of the elements of `seq`, sorted |
|`max(seq)` | `seq`: a sequence-type object  usually having **all** elements of the same type | The highest-value element in `seq` |
|`min(seq)` | `seq`: a sequence-type object  usually having **all** elements of the same type | The lowest-value element in `seq` |
|`sum(seq)` | `seq`: a sequence-type object  usually having **all** number-type elements | The sum of all elements in `seq` |


## Methods

Some functions are bound to a specific object type. For example, it would be useful to have a function that finds the first occurence of a character (or substring) within a string-type object. One could imagine a function like this:
```python
mystr = "hello"
index = find_in_string(mystr, "e")
print(index) # should be 1
```
This could work, but Python has a better way to go about it: *methods*. Methods are functions that are specifically associated with a type. In this case, Python has already provided us with a method to find the first occurence of a character within a string, called `find`. Every object of type `string` has a `find` method. Methods can be accessed like any other object attribute (explained later), with the `.` operator. It is important to keep in mind that **methods always take the object you called it from as their first argument**. Here is a concrete example with the exact same behaviour as the code above:
```python
mystr = "hello"
index = mystr.find("e")
print(index) # should be 1
```
As you can see, the `find` method takes one argument, `"e"`, but **it also has access to `mystr`**, which allows it to find the first occurence of "e" inside of `mystr`. You can think of it like a function that always has `mystr` as an "extra argument", because you called the function **from** `mystr`.

Most complex data types you encounter in Python (like sequence-typed objects) will have their own methods. Some methods can change the object they were called from, like the `append` method that `list`s have:
```python
mylist = [1, 2, 3]
mylist.append(4) # adds 4 to the end of mylist
print(mylist) # should be [1, 2, 3, 4]
```

### Common Methods

**TODO**
