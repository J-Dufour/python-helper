# Python Data Types

:::note

This is a lot to absorb all at once. I recommend you skim through this at first, and come back when you need it.

:::


All data in Python are either represented in the interpreter's memory as *objects* or relations between *objects*. *Objects* have three properties:
- **identity**: a unique referrent of the object. Don't worry about this
- **type**: this is what tells python what operations it can do on the data, and how the operations work.
- **value**: the actual value of the object. For example, `42`, `'John'`, or `[1, 2, 3]`

This articles focuses on the most common **types** built into Python. These can be used without importing any modules.

## Type Cheatsheet
All the most common types in one place.

| Data Type      | Use Case                                                           | Example                                                    |
| ---            | ---                                                                | ---                                                        |
| `None`         | Absence of Value                                                   | `None`                                                     |
| `bool`         | A value that is either "true" or "false"                           | `True`, `False` (Note the capitalization!)                 |
| `int`          | An integer (non-decimal) value                                     | `0`, `-123`, `100_000_000`                                 |
| `float`        | A value representing a real number                                 | `float(0)`, `0.0`, `-1.23`, `1e8`, `1.234e-50`             |
| `string`       | A value that represents text (an immutable sequence of characters) | `"John"`, `'Hello, world!'`                                |
| `tuple`        | An immutable (unchangeable) sequence of *objects*                  | `()`, `(0)`, `1, 2, 3`, `(1.2, 'Hello', False)`            |
| `list`         | A mutable (changeable) sequence of *objects*                       | `[]`, `[0]`, `[1, 2, 3]`, `[1.2, 'Hello', False]`          |
| `dict`         | For representing *key-value* relationships                         | `{"fname": "John", "lname": "Smith"}`                      |

## None

| Data Type | Use Case         | Example |
| ---       | ---              | ---     |
| `None`    | Absence of Value | `None`  |

Only one object has the `None` type, and it can be accessed with the name `None`. This type only has one value.

The `None` type signifies the absence of a value. It is comparable to a `null` value in other languages. You may encounter this type when you use Python functions that cannot guarantee a result (for example, a function that searches for a specific value within a dataset).

## Number Types

| Data Type | Use Case                                 | Example                                                    |
| ---       | ---                                      | ---                                                        |
| `bool`    | A value that is either "true" or "false" | `True`, `False` (Note the capitalization!)                 |
| `int`     | An integer (non-decimal) value           | `0`, `-123`, `100_000_000`                                 |
| `float`   | A value representing a real number       | `float(0)`, `0.0`, `-1.23`, `1e8`, `1.234e-50`             |

These are types used to represent numbers. While the boolean type (`bool`) does not necessarily represent a number, Python considers it a subtype of the integer type (`int`) and internally represents `True` and `False` as `1` and `0`, respectively.

For integer type (`int`) objects, you can use underscores (`_`) to enhance readability. For example, `100_000_000` is exactly the same as `100000000`.

For floating-point type (`float`) objects used to represent real numbers, you can use scientific notation with `e` used to signify "times `10` to the power of". For example, `1e8` means "`1` times `10` to the power of `8`". The exponent can also be a negative value. 

### Numeric Operators
Number types can use the following operators:

| Operator                 | Use                                                                     |
| ---                      | ---                                                                     |
| `x + y`, `x - y`, `x * y`, `x / y`, `x**y` | Add, subtract, multiply, divide, and exponentiate, respectively         |
| `x // y`                     | integer divide: gives the quotient, rounded down to the nearest integer |
| `x % y`                      | modulo: gives the remainder of an integer division                      |

### Boolean Operators
Some of these operators can be used with objects **beyond** the number types, but **they always result in a boolean**[^1].
[^1]: Not all boolean operators support operands of all types. When an operator is given an incompatible operand, it will cause an error. 

| Operator          | Use                                                                                                          |
| ---               | ---                                                                                                          |
| `not x`           | If `x` is `True`, results in `False`. If `x` is `False`, results in `True`                                   |
| `x and y`         | If both `x` and `y` are `True`, results in `True`. Otherwise, results in `False`                             |
| `x or y`          | If either `x` or `y` is `True` (or if both are `True`), results in `True`. Otherwise, results in `False`     |
| `x == y`          | If the value of `x` is equal to the value of `y`, results in `True`. Otherwise, results in `False`           |
| `x != y`          | If the value of `x` is **not** equal to the value of `y`, results in `True`. Otherwise, results in `False`   |
| `x > y`/`x < y`   | If `x` is (greater/lesser) than `y`, results in `True`. Otherwise, results in `False`                        |
| `x >= y`/`x <= y` | If `x` is (greater/lesser) than `y` **or is equal to `y`**, results in `True`. Otherwise, results in `False` |



## Sequence Types

| Data Type      | Use Case                                                           | Example                                                                      |
| ---            | ---                                                                | ---                                                                          |
| `string`       | A value that represents text (an immutable sequence of characters) | `"John"`, `'Hello, world!'`                                                  |
| `tuple`        | An immutable (unchangeable) sequence of *objects*                  | `()`, `(0)`, `1, 2, 3`, `(1.2, 'Hello', False)`                              |
| `list`         | A mutable (changeable) sequence of *objects*                       | `[]`, `[0]`, `[1, 2, 3]`, `[1.2, 'Hello', False]`                            |

Sequence types are useful to represent sequences of values.

*Immutable* sequence types cannot be changed (i.e. elements cannot be added or removed from them) after they are created. In contrast, *mutable* sequence types can be altered: it is possible to add elements to and remove elements from them after they are created.

### Sequence operators
Most sequence types can use the following operators. Note the overlap between these and some [Numeric Operators](./data-types.md#numeric-operators). **The type determines what the operator does.**

For the purposes of this table, assume that `lst` and `lst2` are `list`s, and `n`, `i`, and `j` are `int`s. 

| Operator      | Use                                                                                                                          | Example                                                                                  |
| ---           | ---                                                                                                                          | ---                                                                                      |
| `lst[i]`      | Accesses the `i`th element of `lst`, assuming that the first element is at `i` = `0`.                                        | `[1, 2, 3][2]` => `3`                                                                    |
| `lst[i:j]`    | Returns a *slice* of `lst`, i.e., a `list` consisting of the `i`th element to the `j`th, **excluding the `j`th element**[^2] | `[1, 2, 3][1:3]` => `[2,3]`                                                              |
| `lst + lst2` | Concatenates two sequences                                                                                                   | `[1, 2, 3] + [4, 5, 6]` => `[1, 2, 3, 4, 5, 6]`                                          |
| `lst * n`     | Concatenates lst to itself `n` times                                                                                         | `['hello' , 'world' ] * 3` => `['hello' , 'world', 'hello', 'world', 'hello' , 'world']` |

[^2]: This is true of the built-in sequence types. This **may not** be true for types offered by other libraries, such as `pandas`.

:::tip
The `[i]` and `[i:j]` operators can actually accept *negative* values. Normally, `i` counts upwards from the first element (element `0`). **When `i` is negative, it counts downwards from the last element**. So:
```python
lst = [1, 2, 3]

lst[-1] # => 3

lst[0:-1] # => [1,2]
```
the *slice* operator (`[i:j]`) will also work when `i` or `j` are omitted. When `i` is omitted, the slice starts at the beginning of the sequence, and when `j` is omitted, the slice ends at the last element of the sequence (including the last element).
:::

#### Boolean Sequence Operators
Certain boolean operators basically only work on sequences, so I found it more fitting to introduce them here. Remember, **these operators result in `bool` values**[^1]

| Operator       | Use                                                                                         | Example                                         |
| ---            | ---                                                                                         | ---                                             |
| `x in lst`     | Results in `True` if an element equal to `x` is in `lst`. Otherwise, results in `False`     | `'hello' in [2, True, 'hello']` => `True`       |
| `x not in lst` | Results in `True` if **no** element equal to `x` is in `lst`. Otherwise, results in `False` | `'hello' not in [2, True, 'hello']` => `False`  |

## Mapping Types

| Data Type | Use Case         | Example |
| ---       | ---              | ---     |
| `dict`    | For representing *key-value* relationships | `{"fname": "John", "lname": "Smith"}`  |

Mapping types are useful for representing relationships between *keys* and *values*. The only built-in mapping type is currently the `dict` type, which is short for dictionary.

To demonstrate the use of a `dict`, imagine a contacts list:

| Name    | Phone    |
| ---     | ---      |
| Alice   | 555-0123 |
| Bob     | 555-0124 |
| Charlie | 555-0125 |

In this case, a `dict` would make it easy to relate people's names to their phone numbers. Names would be *keys* and phone numbers would be *values*. When given a *key*, a `dict` can quickly retrieve the *key*'s' associated *value*:

```python
contacts_list = {"Alice": "555-0123", "Bob": "555-0124", "Charlie": "555-0125"}

# I need Bob's number, so I retrieve it from contacts_list by giving it the right key (in this case, "Bob")
bobs_number = contacts_list["Bob"] # Access is similar to sequences, but keys are allowed to be strings
print(bobs_number) # Should be "555-0124"
```

### Mapping Operators

| Operator       | Use                                                       | Example                                                   |
| ---            | ---                                                       | ---                                                       |
| `vals[k]`      | Access the *value* related to the *key* `k` within `vals` | `{"fname": "John", "lname": "Smith"}["fname"]` => `'John'`|


:::note
`dict` keys and values are not always `string`s. `dict` values can be any *object*. `dict` keys have some extra complicated constraints, but in practice they are almost always `string`s or a number type.
:::

