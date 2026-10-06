---
sidebar_position: 4
---

# Classes

All the types introduced so far have been *built-in*, which means that Python defined them for us ahead of time. Python also allows you to make your own types. The easiest way to do this is by creating a *class*. You can think of a class like a custom type that you create. Most Python libraries that we will use, like Numpy and Pandas, have their own classes that use to represent data (for example, a dataset table).

## Class definition

To define a class, you use the `class` keyword. It will typically look like this:
```python
class MyClass:
    suite
```
Where `MyClass` is the name of the class (custom type) that you create, and `suite` is the Python code used to describe the class. Before diving deeper into class definitions, let's look at what we get by default, with the simplest suite possible:

```python
class MyClass:
    pass
```

This creates a new type called MyClass. 

:::tip
**The `pass` keyword**

Many statements, like class definitions and [function definitions](./functions.md#defining-functions), *require* a suite that contains at least one statement. 

```python
# This is not valid python code
def myFunction():
    # The function NEEDS something here
print("After the function def")
```

On rare occasions, you may not want any statements in the suite. The `pass` keyword is a statement that does *nothing*, which you can use in these scenarios:

```python
# This is valid python code
def myFunction():
    pass # literally does NOTHING
print("After the function def")
```
:::

To create an object of type MyClass (also called an *instance* of MyClass), you call the *constructor* of MyClass. A *constructor* is a function used to create an *instance* of a class. For any class `ExampleClass`, the constructor is simply the name of the class, i.e. `ExampleClass()`. Therefore, to create an instance of `MyClass`, we use `MyClass()`:

```python
class MyClass:
    pass

instance_of_MyClass = MyClass()
print(type(instance_of_MyClass)) # should be MyClass
```
What can we do with class instances? By default, these instances can be assigned *attributes*. You can think of attributes as "internal variables", they are named objects that exist inside of the instance. Each instance holds their own set of attributes.

To define and access attributes, use `.` notation, in the form `instance.attribute`:
```python
class MyClass:
    pass

my_instance = MyClass()

my_instance.myattr1 = "Hello!" # define a new attribute named "myattr1", and set its value to "Hello!"

my_instance.mynum = 3.14 # define a new attribute named "mynum", and set its value to 3.14

# You can access attributes later in the same way:
print(my_instance.mynum + 5) # prints 8.14
print(my_instance.myattr1[0:5]) # prints "Hello"

another_instance = MyClass() # creates another instance
print(another_instance.mynum) # will throw an error because another_instance's attributes are independent of my_instance, it does not have mynum defined.
```

## Defining Methods

Most of the time, you will want *every* instance of your class to have certain attributes by default. For example, let's say you want to create a type that represents a fraction. Fractions can be split into two components: a numerator and a denominator. These can be easily represented by attributes:

```python
class Fraction:
    pass

one_half = Fraction()
one_half.numerator = 1
one_half.denominator = 2
```
As you can expect, writing all of this every time would be very tedious. One way to fix this could be to write a function that does all this setup for us:

```python
def initialize_fraction(fraction, numerator, denominator):
    fraction.numerator = numerator
    fraction.denominator = denominator
```

Now, if we want to create a new Fraction:

```python
one_half = Fraction()
initialize_fraction(one_half, 1, 2)
print(one_half.denominator)
```

This function seems pretty tightly bound to our Fraction class, though. It would be a perfect candidate for a [method](./functions.md#methods)! Let's make an `initialize` method for our class. To do this, we simply include a function definition within the class's suite, like so:
```python
class Fraction:
    def initialize(self, numerator, denominator):
        self.numerator = numerator
        self.denominator = denominator
```

The **first** parameter in a method definition will always be the object from which the method was called. The rest of the parameters will need to be passed as arguments when called. Take our new and improved `initialize`:
```python
class Fraction:
    def initialize(self, numerator, denominator):
        self.numerator = numerator
        self.denominator = denominator

one_half = Fraction()
one_half.initialize(1,2)
print(one_half.denominator) # should still be 2
```
Even though our `initialize` method is defined with **3** parameters, it only takes **2** arguments when you call it. This is because the first parameter, which we called `self`, is automatically going to be the object from which the method was called (in this case, `one_half`). So in the method definition, we have the parameters `(self, numerator, denominator)`. When `one_half.initialize(1,2)` is called, Python automatically sets `self` to the object `one_half`, and then assigns the arguments to the rest of the parameters (so `numerator` is set to `1` and `denominator` is set to `2`).

This still seems a little clunky, though. We'll still need to call `initialize` on *every instance of `Fraction` we make*. We know for a fact that every Fraction object will need a `numerator` and `denominator`, so how can we give *every* Fraction a `numerator` and `denominator` from the get-go?

### Magic Methods (A.K.A Special Methods A.K.A Dunder Methods)

Remember how every instance of `Fraction` has to be created by calling the `Fraction()` contructor? Turns out, Python gives you the power to change what `Fraction()` does! The way this happens is through *magic methods*. A magic method is a method with a special name that Python specifically looks out for. These methods may be called by Python automatically in certain circumstances. To avoid programmers accidentally giving their regular method the name of a magic method, **magic methods always begin and end with two underscores (`__`)**. This is why they are sometimes called "Dunder methods" (short for "**D**ouble **under**score methods"). Do note that not all methods with double underscores are magic; only the converse is true: all magic methods have double underscores.

#### __init__

To change our constructor, we need to define the ``__init__()`` magic method. Python automatically calls this method right after it creates an instance of a class. It can even take parameters like any other methods, which it will take from the constructor call. All we have to do in our case is to change the name of `initialize` in our `Fraction` class to `__init__`, like so:
```python
class Fraction:
    def __init__(self, numerator, denominator):
        self.numerator = numerator
        self.denominator = denominator
```
:::note
Because `__init__` is still a **method**, its first parameter, `self`, refers to the class instance it is "bound" to. Usually this refers to the object from which a method is called, but in this case it refers to the new object that is created when `Fraction()` is called. The order of events when `Fraction()` is called be thought of as follows:
1. create a new `Fraction` object, (let's call it `frac`)
2. call `frac.__init__()`, with all the arguments (if any) given to `Fraction()` passed along to `__init__()`

Remember, Python does this *automatically*, only because it knows in advance to look for a method called `__init__` in the `Fraction` class.
:::

Now, **because our `Fraction` class now has a method called "`__init__`"**, Python will run `__init__` automatically when the class constructor, `Fraction()`, is called. In fact, since our `__init__` definition has more than the `self` parameter, Python requires that you pass in the other arguments when you call `Fraction()`. So 
```python
class Fraction:
    def __init__(self, numerator, denominator):
        self.numerator = numerator
        self.denominator = denominator
one_half = Fraction()
```
Will fail, because `__init__` was defined with the parameters `numerator` and `denominator`, which were not given in the `Fraction()` call. On the other hand,
```python
class Fraction:
    def __init__(self, numerator, denominator):
        self.numerator = numerator
        self.denominator = denominator
one_half = Fraction(1, 2) # Pass in 1 and 2 as arguments
print(one_half.denominator) # should still be 2
```
Will succeed, passing on `1` and `2` to the `__init__` method as `numerator` and `denominator` respectively (remember, the first parameter in a method is automatically assigned by Python).

And now we finally have a way to automatically give our `Fraction` objects attributes upon creation.

`__init__` is not the only magic method, of course. Just about any behaviour you'd want in an object can be programmed through magic methods.

To learn more about megic methods, check out the [Python docs](https://docs.python.org/3/reference/datamodel.html#special-method-names).










