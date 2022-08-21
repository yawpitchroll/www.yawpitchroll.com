+++
title = "The 42 Python Operators"
date = "2019-08-11"
tags = ["python", "learning"]
categories = ["articles"]
series = ["The Etymology of Python"]
draft = true
+++

## Python's Meaningful Punctuation

In the previous post you learned about [Python's 35 keywords][last-post], which form the backbone of Python's grammar. You can think of those as the most basic _nouns_ of the language; in this post we'll take a few steps further and introduce the most basic _verbs_, in the form of Python's 42[^1] operators.

  [^1]: Since Python 3.5 was released in 2015 there have been 41 operators, but since 3.8 is expected soon it's sensible to introduce the latest addition as well.
  [last-post]: {{< relref "the-35-words-you-need-to-python" >}} "Read about Python's 35 keywords"

<blockquote>
  <p>Keep Calm and Carry the One.</p>
  <cite>Almost certainly never said by Alan Turing</cite>
</blockquote>


Python's operators, like its keywords, are _reserved_, meaning that they're a fixed part of the syntax of the language. This means you cannot add new operators, or change the specific locations in which they can occur in your Python code. Unlike keywords, however, you _do_ have some ability to customize their behavior through a process known as [operator overloading][overloading].

  [overloading]: https://en.wikipedia.org/wiki/Operator_overloading "Read about operator overloading"

This article will be a bit of a deep dive into the operators available to you and how they _usually_ work, along with a bit of a roadmap into how and when you'd customize their behavior. It's going to build quite rapidly on the [previous article][last-post], and in turn it will be a resource you'll want to come back to when we get into the _builtin types_ in later articles, as that's where you'll really see these operators in action.

### A Few Conventions {#conventions}

Hopefully you remember the [conventions][keyword-conventions] from the previous article; if not you may want to familiarize yourself with them before carrying on. I'll restate the ones required for this article below, expanding on them slightly, and I'll also add some new ones.

  [keyword-conventions]: {{< relref "the-35-words-you-need-to-python#conventions" >}} "Revisit the conventions from the previous article"

OPERATOR
: A reserved _symbol_ that indicates an action to be performed. We'll visit all of the different ones available below. What an OPERATOR actually does is determined by what OBJECT(s) it is _bound_ to at runtime.

OBJECT
: Any individual _thing_ you can interact with and act on using OPERATORs. The available OPERATORs for any given OBJECT are determined by the TYPE of that OBJECT. Confusingly, though, a TYPE is _also_ an OBJECT in Python; in fact _everything_ you can interact with in Python is an OBJECT.

TYPE
: An abstract _kind_ or _class_ of OBJECT, it defines the _state_ and _behaviors_ associated with any specific OBJECT of that TYPE. Recall that in Python you implement [new TYPEs][newtype] using the {{< definition-relref "class" "the-35-words-you-need-to-python#class" >}} keyword.

  [newtype]: {{< relref "the-35-words-you-need-to-python#newtype" >}} "Revisit custom type creation"

INSTANCE
: A specific, concrete example of an OBJECT of a given TYPE.

For example the number `4` is an INSTANCE of the [int][int] (short for "integer") TYPE, while `"Hello"` is an INSTANCE of the [str][str] (short for "string") TYPE. Both are OBJECTs, but the OPERATORs you can use with them -- and what those OPERATORs do -- is determined by the behavior defined by each of their respective TYPEs. 

  [int]: https://docs.python.org/3/library/functions.html#int "Read about the int type"
  [str]: https://docs.python.org/3/library/functions.html#func-str "Read about the str type"

CALLABLE
: An OBJECT that represents some action to perform: it performs that action when you call it with some number of _arguments_ then it _returns_ (or gives back) an OBJECT.

FUNCTION
: a CALLABLE that is _generic_, meaning that it's not tightly bound to a particular TYPE. The [**print**][print] builtin, for instance, is a FUNCTION that will work on many different TYPEs. These are called using the `FUNCTION(argument[, argument])` form.

  [print]: https://docs.python.org/3/library/functions.html#print "Read about the print builtin function"

METHOD
: a CALLABLE that is tightly bound to a particular INSTANCE (or, more rarely, a TYPE). The [**str.upper**][str.upper] builtin, for instance, is an INSTANCE METHOD that will work _only_ on an INSTANCE of the [str][str] TYPE. These are called using the `INSTANCE.METHOD(argument[, argument])` form, which differes from a FUNCTION because the INSTANCE itself will be implicitly provided as the first argument (by convention given the name **self**) to the METHOD.

  [str.upper]: https://docs.python.org/3/library/stdtypes.html#str.upper "Read about the str.upper builtin method"

In Python there are two forms of OPERATOR to be aware of:

UNARY:
: An OPERATOR that binds exactly one OBJECT, which appears to the immediate right of the OPERATOR.

BINARY:
: An OPERATOR that binds exactly two OBJECTs, which appear to the immediate left and right of the OPERATOR (this is known as _infix_ notation).

Most of the OPERATORs are BINARY, but there are a few that can be either UNARY or BINARY depending on the context. We'll pay special attention to them below.

NAME
: Any word that _is neither_ a [keyword][last-post] nor an OPERATOR, and that is used as an _alias_ to _refer to_ some specific OBJECT. Usually created with the {{< operator-relref "+">}} _assignment_ OPERATOR via `NAME = OBJECT`.

EXPRESSION
: Any composite form of the above that can be _evaluated_ to an OBJECT. For example, `4`, `2 + 2`, `1 * 3 + 1` and `sum([1, 1, 1, 1])` are all EXPRESSIONs that evaluate to `4`. The EXPRESSION represents the smallest discrete unit of work in Python.

STATEMENT
: Any single line of code that is composed of at least one of the above. These can get quite complex, but to _do_ anything they'll usually need to include KEYWORDs and/or OPERATORs plus EXPRESSIONs. You've already met a _useful_ STATEMENT in `number = 2`. If you read each STATEMENT in a program out in turn you can track the program as it does its work.



Now we've got all the simple building blocks defined and we can start organizing them into composite structures.


That covers any given _line_ of code, but there are also a couple of higher level structures we need to define for the moment:

BLOCK
: At least two STATEMENTs that are bound together; the first STATEMENT will end in a **:** character and indicates the start of the BLOCK. The second and all further STATEMENTs inside that BLOCK will be indented further right than the initial STATEMENT, to indicate that they _belong_ to the same BLOCK. The last such indented STATEMENT represents the end of the BLOCK.

MODULE
: A single Python .py file; it's composed of some number of STATEMENTS. All Python programs are comprised of at least one MODULE. As you'll see below we write all of our functionality inside MODULEs, and we use KEYWORDs and NAMEs to _import_ functionality from other MODULEs.



In computer programming an [operator][operator] is really just a _symbol_ that denotes a particular _action_ to perform on some specified _thing_ or, usually, _things_. They're usually composed of one or more punctuation characters (as in {{< operator-relref "+">}} and {{< operator-relref "**" >}}), but they can also be a word or even words (as in {{< operator-relref "and" >}} and {{< operator-relref "not in" >}}).

  [operator]: https://en.wikipedia.org/wiki/Operator_(computer_programming) "Read about operators in computer programming"



### Punctuation
{{< operator "." >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "." >}}

{{< operator "," >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "," >}}

{{< operator ":" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref ":" >}}

{{< operator ";" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref ";" >}}

{{< operator "..." >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "..." >}}

{{< operator "->" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "->" >}}

{{< operator "(" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "(" >}}

{{< operator ")" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref ")" >}}

{{< operator "[" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "[" >}}

{{< operator "]" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "]" >}}

{{< operator "{" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "{" >}}

{{< operator "}" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "}" >}}

### Two Assignment Operators

For virtually every task you'll need to [assign][assignment] _something_ to a NAME you can work with. For most of Python's history there's been just one way to do that.

  [assignment]: https://en.wikipedia.org/wiki/Assignment_(computer_science) "Read about assignment"

{{< operator "=" >}}
: Used in a STATEMENT to assign the NAME(s) to its left to the OBJECT(s) to its right, ie `x = 2`.
: Used in a SIGNATURE to define a default value for a named PARAMETER, ie `def foo(x=2)`.
: Used in a CALL to assign a specific value to a given named ARGUMENT, ie `foo(x=4)`.

A repurposing of the [equals sign][equals_sign] first recorded by Robert Recorde in 1557. Confusingly for mathematicians the single equals _does not_ indicate either _equality_ or an _equation_, but instead is used to assign a name to refer to a specific object. For equality, see the {{< operator-relref "==" >}} operator.

  [equals_sign]: https://en.wikipedia.org/wiki/Equals_sign "Read about the equals sign"
{{< /operator >}}

The most common usage is to fully evaluate whatever is on the right, then assign the resulting OBJECT directly to a NAME; this behavior _cannot_ be overloaded.

```python
NAME = EXPRESSION
```

Another common usage is to assign to an ATTRIBUTE on an OBJECT; this behavior _can_ be overloaded via the `CLASS.__setattr__` dunder method, though it is not common to do so in practice because this changes how _all_ such attributes are assigned for the OBJECT. In a later article I'll discuss a more useful way to control assignment on an attribute by attribute basis using the `property` builtin function.

```python
OBJECT.ATTRIBUTE = EXPRESSION
```

Assignment can also be made to a particular item in a MUTABLE COLLECTION; this behavior _can_ be overloaded via the `__setitem__` dunder method, though it is also rare to do so.

```python
COLLECTION[INDEX] = EXPRESSION
```

In addition to the single assignment form shown above a comma can be used to separate multiple OBJECTs on the right; these will be implicitly combined into a **tuple**, which will be what the NAME actually refers to:

```python
NAME = EXPRESSION_A, EXPRESSION_B
```

You can optionally include parentheses to make the tuple creation more explicit:

```python
NAME = (EXPRESSION_A, EXPRESSION_B)
```

Additionally you can use a {{< operator-relref "*" >}} _iterable unpacking_ to include the contents of a COLLECTION in the tuple:

```python
NAME = EXPRESSION_A, *COLLECTION
```

In all the above cases the entire right-hand side is evaluated, proceeding left to right, and finally the tuple is created and assigned to NAME.

At times you want to set multiple NAMEs to the same OBJECT; this is a good use of _assignment chaining_:

```python
NAME_A = NAME_B = EXPRESSION
```

Unlike many languages Python also supports several forms of _multiple assignment_. For instance you can use commas on both sides to assign some number of NAMEs to an equal number of EXPRESSIONs:

```python
NAME_A, NAME_B = EXPRESSION_A, EXPRESSION_B
```

This might look a little confusing at first, but the same process occurs: Python evaluates the right-hand side, proceeding left to right, and once _both_ EXPRESSIONs are evaluated the two resulting OBJECTs are assigned to the two corresponding NAMEs.

But you can also directly unpack a COLLECTION with exactly one item per NAME on the right:

```python
NAME_A, NAME_B = COLLECTION
```

Often though you don't know the specific size of the COLLECTION, though, and you can use a single {{< operator-relref "*" >}} before a NAME to indicate that it should build a **list** of whatever items in the COLLECTION do not correspond to a fixed NAME on the right.

For instance, some times it's useful to have the first item of a COLLECTION and a list of everything that remains:

```python
HEAD, *TAIL = COLLECTION
```

Or the last item and everything that preceded it:

```python
*HEAD, TAIL = COLLECTION
```

Note that in both of the above cases the COLLECTION needs to contain _at least_ one item, since that will be assigned to the fixed NAME that corresponds to its position in the COLLECTION.

From that you can see why this would require at least two items, but would collect up any more than that into a list.

```python
HEAD, *MID, TAIL = COLLECTION
```

You can also use parentheses to build sub-assignments that can get arbitrarily complex:

```python
HEAD, (SUBHEAD, *SUBTAIL), *TAIL = OBJECT, COLLECTION, *COLLECTION
```

However this can get quite unwieldy pretty quickly, so you should endeavour to keep your code as simple as it _needs_ to be.

#### New in Python 3.8

For many years {{< operator-relref "=" >}} has been the obvious, and indeed _only_, want to assign a new NAME, but as Python 3.8 is, at the time of writing, just about to drop it's worth at introducing you to a new shortcut that's likely to catch on (at least for those not worried about backwards compatability).

{{< operator ":=" >}}
: Used in an EXPRESSION to assign the NAME on its left to the OBJECT(s) to its right; usually used as shorthand to capture a value being generate "on-the-fly". _Cannot_ be used as a STATEMENT without parentheses to avoid confusion with the normal assignment form. (ie `(x:= 2)` is valid but `x := 2` is not and should be replaced with `x = 2`).

More or less affectionately known as the _walrus operator_ (notice the two eyes and long tusks, when viewed sideways), this new operator has been borrowed from languages like ALGOL and Pascal, where it's used instead of {{< operator-relref "=" >}} to represent assignment. In Python it exists to distinguish its intended use inside an EXPRESSION.
{{< /operator >}}

Since it's a new addition its real-world uses are still being determined. It's most common usage will be in loops:

```python
while NAME:= OUTER_FUNCTION():
    INNER_FUNCTION(NAME)
```

Which in Python 3.7 and earlier would have to have been written:

```python
NAME = OUTER_FUNCTION()
while NAME:
    INNER_FUNCTION(NAME)
    NAME = OUTER_FUNCTION()
```

So it cuts down on two lines of vertical space and saves some repetition. However it's considerably more limited than {{< operator-relref "=" >}}, as only a few forms are both allowed and encouraged. Most importantly only single assignment to a NAME is allowed; you cannot assign to an OBJECT attribute or an item in a COLLECTION, and neither chained nor multiple assignment are possible.

One major difference is that no implicit tuple is created if a comma is on the right and {{< operator-relref ":=" >}} will bind only the _first_ item given. For instance:

```python
(NAME := OBJECT_A, OBJECT_B)
```

The overall expression above will evaluate to a tuple `(OBJECT_A, OBJECT_B)` as usual, but the NAME will refer only to the first item of that tuple.

You'll usually want to use explicit parentheses to counteract that:

```python
(NAME := (OBJECT_A, OBJECT_B)
```

Note that {{< operator-relref "*" >}} unpacking is still allowed on the right side, with the caveat just mentioned.

```python
(NAME :=- (EXPRESSION_A, *COLLECTION))
```

It will be interesting to see just how much {{< operator-relref ":=" >}} and assignment expressions get used in the real world, but at least you'll recognize it when it starts to arrive.

### Eight Arithmetic Operators
{{< operator "+" >}}
: UNARY Positive, overloaded by `__pos__`.
: BINARY Addition, overloaded by `__add__` and optionally `__radd__`.
{{< /operator >}}

#### Unary Positive

```python
+EXPRESSION
```
Designates a value as positive. In **int** is `0 + EXPRESSION`, which will not flip the sign.

#### Binary Addition

```python
X + Y
```
Adds Y to X.

{{< operator-relref "+" >}}

{{< operator "-" >}}
: UNARY Arithmetic Negation, overloaded by `__neg__`.
: BINARY Subtraction, overloaded by `__sub__` and optionally `__rsub__`.
{{< /operator >}}

#### Unary Arithmetic Negation

```python
-EXPRESSION
```

Designates a value as negative. In **int** is `0 - EXPRESSION`, hence will flip the sign.

```python
X - Y
```

Subtracts Y from X.

{{< operator-relref "-" >}}

{{< operator "*" >}}
: BINARY Multiplication, overloaded by `__mul__` and optionally `__rmul__`.
{{< /operator >}}

```python
X * Y
```
{{< operator-relref "*" >}}

{{< operator "/" >}}
: BINARY True Division, overloaded by `__truediv__` and optionally `__rtruediv__`.
{{< /operator >}}

```python
X / Y
```

{{< operator-relref "/" >}}

{{< operator "//" >}}
: BINARY Floor Division, overloaded by `__floordiv__` and optionally `__rfloordiv__`.
{{< /operator >}}

```python
X // Y
```

{{< operator-relref "//" >}}

{{< operator "%" >}}
: BINARY Modulus, overloaded by `__mod__` and optionally `__rmod__`.
{{< /operator >}}

```python
X % Y
```

{{< operator-relref "%" >}}

{{< operator "**" >}}
: BINARY Exponentiation, overloaded by `__pow__` and optionally `__rpow__`.
{{< /operator >}}

```python
X ** Y
```

{{< operator-relref "**" >}}

{{< operator "@" >}}
: BINARY Matrix Multiplication, overloaded by `__matmul__` and optionally `__rmatmul__`.
{{< /operator >}}

```python
X @ Y
```

{{< operator-relref "@" >}}

### Bitwise Operators
{{< operator "&" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "&" >}}

{{< operator "|" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "|" >}}

{{< operator "^" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "^" >}}

{{< operator "~" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "~" >}}

{{< operator "<<" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "<<" >}}

{{< operator ">>" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref ">>" >}}

### Comparison Operators
{{< operator "==" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "==" >}}

{{< operator "!=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "!=" >}}

{{< operator "<" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "<" >}}

{{< operator "<=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "<=" >}}

{{< operator ">" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref ">" >}}

{{< operator ">=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref ">=" >}}

### Boolean Operators
{{< operator "and" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "and" >}}

{{< operator "or" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "or" >}}

{{< operator "not" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "not" >}}

### Identity Operators
{{< operator "is" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "is" >}}

{{< operator "is not" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "is not" >}}

### Membership Operators
{{< operator "in" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "in" >}}

{{< operator "not in" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "not in" >}}

### Augmented Assignment Operators
{{< operator "+=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "+=" >}}

{{< operator "-=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "-=" >}}

{{< operator "*=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "*=" >}}

{{< operator "/=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "/=" >}}

{{< operator "//=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "//=" >}}

{{< operator "%=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "%=" >}}

{{< operator "**=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "**=" >}}

{{< operator "@=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "@=" >}}

{{< operator "&=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "&=" >}}

{{< operator "|=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "|=" >}}

{{< operator "^=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "^=" >}}

{{< operator "<<=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref "<<=" >}}

{{< operator ">>=" >}}
: Assignment within a STATEMENT
{{< /operator >}}

{{< operator-relref ">>=" >}}








### Bitwise Operations

&  	AND 	Sets each bit to 1 if both bits are 1
| 	OR 	Sets each bit to 1 if one of two bits is 1
^ 	XOR 	Sets each bit to 1 if only one of two bits is 1
~  	NOT 	Inverts all the bits
<< 	Zero fill left shift 	Shift left by pushing zeros in from the right and let the leftmost bits fall off
>> 	Signed right shift 	Shift right by pushing copies of the leftmost bit in from the left, and let the rightmost bits fall off

### Augmented Assignment
+= 	x += 3 	x = x + 3 	
-= 	x -= 3 	x = x - 3 	
*= 	x *= 3 	x = x * 3 	
/= 	x /= 3 	x = x / 3 	
//= 	x //= 3 	x = x // 3 	
%= 	x %= 3 	x = x % 3 	
**= 	x **= 3 	x = x ** 3 	
&= 	x &= 3 	x = x & 3 	
|= 	x |= 3 	x = x | 3 	
^= 	x ^= 3 	x = x ^ 3 	
>>= 	x >>= 3 	x = x >> 3 	
<<= 	x <<= 3 	x = x << 3

### Comparisons
== 	Equal 	x == y 	
!= 	Not equal 	x != y	
> 	Greater than 	x > y 	
< 	Less than 	x < y 	
>= 	Greater than or equal to 	x >= y 	
<= 	Less than or equal to 	x <= y

### Logical Comparisons
and  	Returns True if both statements are true 	x < 5 and  x < 10 	
or 	Returns True if one of the statements is true 	x < 5 or x < 4 	
not 	Reverse the result, returns False if the result is true 	not(x < 5 and x < 10)

### Identity
is  	Returns true if both variables are the same object 	x is y 	
is not 	Returns true if both variables are not the same object 	x is not y

### Membership
in  	Returns True if a sequence with the specified value is present in the object 	x in y 	
not in 	Returns True if a sequence with the specified value is not present in the object 	x not in y

## Precedence
**  # exponentiation
+x, -x, ~x  # unary pos, neg, NOT
*, /, //, %, @  # mult, div, floor div, modulo, matrix mult
+, -    # add, sub
<<, >>  # shift left, shift right
&   # AND
^   # XOR
|   # OR
in,not in, is, is not, <=,<,>,>= # comparisons
==,!=
not # NOT
and # AND
or  # OR
:=  # ASSIGNMENT EXPRESSION

=,:=,+=,-=,*=,/=,//=,%=,**=,&=,|=,^=,<<=,>>= # ASSIGNMENT STATEMENTS ALWAYS BIND LAST


