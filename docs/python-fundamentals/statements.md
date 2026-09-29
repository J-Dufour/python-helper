# Python Statements

In short, a *statement* is any valid Python instruction. Some statements (e.g. `if` statements, `for` statements, etc.) may contain other statements.
```python
# The following are all statements:
5 

3 + 7 * 8

"Hello"

x = "hello"

print(x)

# Note: the following two lines are all one (1) if statement.
if True == False: # True == False is a statement on its own!
    print("The world is ending!") # this line is also a statement on its own, and so is the string "The world is ending!"!
```

## Expressions

Many statements can be *evaluated* to a value. For example:
```python
1 + 2 * 3 ** 4
```
Will *evaluate* to the number that results from these mathematical [operations](./data-types#numerical-operators). In this case, `163`.

Statements that *evaluate* to a certain value are called *expressions*. Many statements in Python require expressions to be in certain places. For example:

## Assignments

One very common statement is an *assignment*. This is what lets you give names to certain expressions. Note that an assignment is not an expression; it does not have a value. An *assignment* follows this general syntax:
```python
my_var = my_expr
```
Where `my_var` is the name you want to give to an expression, and `my_expr` is that very expression. `my_expr` **must** be an expression, or else an error will occur.
Once this assignment statement is run, `my_var` becomes a *name* that refers to an *object* in memory. This object will have the value and type of `my_expr`. Another effect of this assignment is that `my_var`, as a name, *becomes* an expression. In fact, it becomes an expression that evaluates to the same value as `my_expr`. You can now use `my_var` in any place that requires an expression, like another assignment statement.

## Control Flow

In very simple Python scripts, every line gets executed by the interpreter. For example:
```python
# Age Calculator

current_year = 2026
birth_year_string = input("Enter your birth year: ")
birth_year = int(birth_year_string)

age = current_year - birth_year
print(f'Your age is {age}!')
```
This script will always run line 1, then 2, then 3, etc. until it either gets to the end of the file or an error occurs. This is too rigid for most use cases. For example, what if the user does not give a valid number as a birth year? Surely we would want to run *different* lines of code depending on the circumstances.

"Control Flow" refers to the ability to control the "flow" of code in just this fashion. Sometimes we don't want every line of code to be run, and sometimes we want different lines of code to be run, and sometimes we even want the same lines of code to be run *more than once*. To accomplish this, we can use `if`, `while`, and `for` statements. 

### `if` Statements

`if` statements allow you to only run some lines of code when a given expression is true. It looks like this:
```python
if condition:
    suite
```
Here, `condition` can be any valid python expression. The type of the expression should usually be a `bool`, and this is what we will focus on for now.
`suite` represents one or more statements that will **only** run when `condition` evaluates to `True`. These statements are given line by line as normal, and must be indented.

Indentation is how Python knows whether knows whether a statement following an `if` statement is a part of the `suite`, or if it is simply a statement *after* the `if` statement. This is also true of `while` and `for` statements below.

```python
if condition:
    print("I'm in the if statement, I only run if condition is True.")
print("I'm outside of the if statement, I always run.")
```

#### `condition`s

It is important to restate that the `condition` of an `if` statement can be **any expression**, but for most use cases we limit it to **any expression that evaluates to a `bool`**. This is where [Boolean Operators](./data-types.md#boolean-operators) can really shine, because they naturally result in `bool`s!

Here are some possible 



<span id="truthiness"></span>
:::info
 **"Truthy" and "Falsy" values** 

If an `if` statement can accept any expression as a `condition`, how does it handle values that are not `True` or `False`? The answer is that every expression, no matter the type, has a "truthiness value", which is either "Truthy" or "Falsy". When an `if` statement receives a non-`bool` expression, it will use the truthiness value of the expression to choose whether or not to run its `suite`. In general, all values are "Truthy" except for the following, which are "Falsy":
- `None`
- `False`
- Any number-typed value with a value of `0` (including `0.0`)
- Any empty sequence-type value (`""`, `()`, `[]`)
::: 

#### `else` and `elif`



### `while` Statements

*AKA: while loops*

### `for` Statements

*AKA: for loops*
## Imports
