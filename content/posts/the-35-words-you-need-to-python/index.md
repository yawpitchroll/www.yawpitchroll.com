+++
title = "The 35 Words You Need to Python"
date = "2019-07-28"
tags = ["python", "learning"]
categories = ["articles"]
series = ["The Etymology of Python"]
aliases = ["posts/the-35-words-you-need-to-python/the-35-words-you-need-to-python/"]
summary = "Let's face it, learning to _write_ computer programs is _hard_. Doing so involves picking up a lot of specialized skills and jargon, most of which is unfamiliar, and it also means cultivating a mental approach to the world that, at first, might seem downright _alien_. It's a long journey, but fluency starts with learning how to _read_ computer programs, and that _really_ shouldn't be so hard."

+++

## In the Beginning, there were the Words

Let's face it, learning to _write_ computer programs is _hard_. Doing so involves picking up a lot of specialized skills and jargon, most of which is unfamiliar, and it also means cultivating a mental approach to the world that, at first, might seem downright _alien_. It's a long journey, but fluency starts with learning how to _read_ computer programs, and that _really_ shouldn't be so hard.

<blockquote>
  <p>Programs must be written for people to read, and only incidentally for machines to execute.</p>
  <cite>Harold Abelson</cite>
</blockquote>

One of the defining traits of the Python programming language is that it's _designed_ to be readable by humans. For the most part it fulfills that promise, however, after several years of helping others understand Python, I've come to realize that there's an important caveat to that statement; it's really only true for someone with a _significant_ and _specialized_ English-language vocabulary.

The truth is you need enough mastery of the "rules" of English grammar and wordplay to recognize and understand, at a glance, words _written_ in English that _are not_ actually words you'll find in an English dictionary. Nonstandard terms like **def** (a _contraction_), **elif** (a _portmanteau_) and **nonlocal** (a _neologism_) all abound, so even for those with quite advanced _native_ English fluency the task of learning Python is very much like trying to learn a foreign language that's _slightly_ related to their native tongue. For those without that fluency learning Python is like learning a foreign language _inside_ a foreign language, and is therefore _far_ more difficult.

To make that task a little easier I'm going to try, in this post and the ones that follow, to shed some light on the meaning of -- and a _little_ of the etymological history behind -- the fundamental units of Python fluency. In this first part we will start with the most basic of those units, Python's 35 _keywords_[^1].

  [^1]: There are 35 keywords as of Python 3.7, the current major version of the language as of the time of writing. New keywords are added quite rarely, and it's even more rare for keywords to be removed, but in whatever version you're on you can use `from keyword import kwlist; print(kwlist)` to view the current list.

That's right; the entire vocabulary of Python you actually _need_ to know to start to do meaningful work is just 35 words. It's not the smallest language, but it's _far_ from the largest, and just compare it to the roughly 10,000 words required to achieve basic fluency in a non-programming language.

### First, Some Conventions

Python is what is known as a _statement_-oriented language; but what _is_ a statement? Well, for the purposes of this article we're just going to say that in Python a statement is a _single_ line of code that does _something_. _What_ it does, specifically, depends on the building blocks of that statement.

But what are those building blocks? Well, let's define them quickly and _very_ roughly, since we'll go into more detail about them in later posts. I'll use UPPERCASE letters to make it easier to visually distinguish these abstract forms from the specific instances we'll talk about later.

KEYWORD
: A reserved _word_ the meaning of which _cannot_ be changed by the user. We will visit all 35 of these in the next section of this article.

OPERATOR
: A reserved _symbol_ that indicates an action to be performed. For example, `=` is the _assignment_ OPERATOR and `+` is the _addition_ OPERATOR. There are quite a few others others, but we'll save them for the next post. A small number of KEYWORDs behave like OPERATORs, and I'll point those out below.

These are both provided by Python and you can't directly change their meaning, which means that they're somewhat inflexible. To do most work you'll need something more flexible, which is why Python gives you the ability to represent _anything_.

OBJECT
: An individual _thing_ you can interact with. Unlike KEYWORDs and OPERATORs, you can directly manipulate these, though the degree to which you can manipulate them depends on what _type_ of OBJECT they are. You can also use KEYWORDs to define entirely new _types_, which makes them a very expressive way of building new _things_ of your own. So expressive, in fact, that practically speaking _everything_ you interact with in Python will be an OBJECT.

That can be a bit abstract and hard to wrap your head around at this point, though. For now just know that OBJECTs tend to fall into three main categories.

VALUE
: An OBJECT that represents a single, concrete _thing_; for the purposes of this discussion what that thing actually _is_ is irrelevant, but as an example, `4` is a VALUE of the [**int**][int] (short for _integer_ type) and `hello` is a VALUE of the [**str**][str] (short for _string_) type. These are both examples of _primitive_ types, which have a single meaningful value, but there are also _composite_ types for describing things the meaning of which is defined by more than one _attribute_. A real-world example would be a square, which cannot be defined without both height and width. As you'll see below three special KEYWORDs all behave like VALUEs, though as before you cannot change their meaning.

  [int]: https://docs.python.org/3/library/functions.html#int "Read about the int type"
  [str]: https://docs.python.org/3/library/functions.html#func-str "Read about the str type"

COLLECTION
: An OBJECT that groups together or contains other OBJECTs; there are _many_ different types of COLLECTION in Python, but for the moment all we care about is that a COLLECTION _contains_ zero or more OBJECTs. For example the statement `[2, 3, 4]` creates a COLLECTION of the type [**list**][list] that holds three VALUEs inside of it. A COLLECTION can contain _any_ OBJECT, so you can _nest_ a COLLECTION inside another COLLECTION.

  [list]: https://docs.python.org/3/library/stdtypes.html#list "Read about the list type"

CALLABLE
: An OBJECT that represents some action to perform: it performs that action when you call it with some number of _arguments_ then it _returns_ (or gives back) an OBJECT. For instance [**sum**][sum] is a CALLABLE and when we call it using `sum([2, 3, 4])` it gives us back the VALUE `9`. There are several different kinds of CALLABLE, and we'll touch on them in more detail below.

  [sum]: https://docs.python.org/3/library/functions.html#sum "Read about the sum builtin function"

It wouldn't be very efficient to type out the same OBJECT every time you needed to refer to it, though. It's often very helpful to be able to refer to things _indirectly_.

NAME
: Any word that _is not_ a KEYWORD, and that is used as an _alias_ to _refer to_ some specific OBJECT. Unlike a KEYWORD the meaning of a NAME _may_ change over the course of a program, which is why these are often -- if a little incorrectly -- thought of as _variables_. There are several ways to create new NAMEs (and one to destroy them), as we'll see below, but as a simple example in `number = 2` the _assignment_ OPERATOR **=** creates the NAME **number** and assigns it to refer to the VALUE **2**. When later that is followed by `number += 2`, however, the _augmented assignment_ operator **+=** will re-assign **number** to refer to **4**.

Now we've got all the simple building blocks defined and we can start organizing them into composite structures.

EXPRESSION
: Any composite form of one or more of the above that can be _evaluated_ to an OBJECT. For example, `4`, `2 + 2`, `1 * 3 + 1` and `sum([1, 1, 1, 1])` are all EXPRESSIONs that evaluate to `4`. The EXPRESSION represents the smallest discrete unit of work in Python.

STATEMENT
: Any single line of code that is composed of at least one of the above. These can get quite complex, but to _do_ anything they'll usually need to include KEYWORDs and/or OPERATORs plus EXPRESSIONs. You've already met a _useful_ STATEMENT in `number = 2`. If you read each STATEMENT in a program out in turn you can track the program as it does its work.

That covers any given _line_ of code, but there are also a couple of higher level structures we need to define for the moment:

BLOCK
: At least two STATEMENTs that are bound together; the first STATEMENT will end in a **:** character and indicates the start of the BLOCK. The second and all further STATEMENTs inside that BLOCK will be indented further right than the initial STATEMENT, to indicate that they _belong_ to the same BLOCK. The last such indented STATEMENT represents the end of the BLOCK.

MODULE
: A single Python .py file; it's composed of some number of STATEMENTS. All Python programs are comprised of at least one MODULE. As you'll see below we write all of our functionality inside MODULEs, and we use KEYWORDs and NAMEs to _import_ functionality from other MODULEs.

There are many other concepts you'll need to become familiar with, but with these building blocks we can investigate all 35 words in Python's relatively small vocabulary, and thus understand the skeleton of any Python program.

## On to the Keywords

### One That Does Nothing

{{< definition doclink="https://docs.python.org/3/tutorial/controlflow.html?highlight=pass#pass-statements" >}}
pass
: A placeholder; technically known as Python's _null operation_, {{< definition-relref "pass" >}} does nothing whatsoever; it exists solely to allow you to write a syntactically valid BLOCK.

The general meaning here comes from a Middle English verb borrowed via Old French from the Latin **_passus_** that implies _"to move by [a place, without stopping]"_. More specifically the meaning in Python is borrowed from its use in sequential-play card games such as Bridge, where if you do not wish to do anything on your turn you **_pass_** control of the game to the next player, doing nothing.
{{< /definition >}}

The need for this is simple; once you begin a BLOCK in Python it _must_ contain _at least one_ indented STATEMENT to be considered valid syntax. The {{< definition-relref "pass" >}} statement exists to allow you to write a valid BLOCK structure _before_ you're ready to start writing meaningful statements.

```python
STATEMENT:
    pass
```

Because it's mainly used early on when building the rough structure of a program you'll rarely, if ever, see {{< definition-relref "pass" >}} in working code, but it's good to know it exists.

### Three That Are Objects

The next three keywords are specialized because they each behave like a primitive VALUE. This means they can be assigned to a NAME, kept within a COLLECTION, and can be the result of evaluating an EXPRESSION. They're also the only keywords that start with a capital letter, which makes them easy to distinguish.

#### Boolean values

These two are used in most, if not all, programs, and are essential whenever performing [Boolean logic][boolean].

  [boolean]: https://en.wikipedia.org/wiki/Boolean_algebra "Learn about Boolean algebra"

{{< definition doclink="https://docs.python.org/3.7/library/stdtypes.html#boolean-values" >}}
True
: Indicator of logical _truth_ and the opposite of {{< definition-relref "False" >}}; behaves like the _integer_ `1`, except that it will always be displayed as {{< definition-relref "True" >}}.

From the Old English adjective **_triewe_**, which has German roots; the general meaning is of being "worthy of trust" and "consistent with fact". In logic, though, the specific meaning is really just "that which is not false", and in computer programming it's usually a proxy for the binary digit 1.
{{< /definition >}}

{{< definition doclink="https://docs.python.org/3.7/library/stdtypes.html#boolean-values" >}}
False
: Indicator of logical _untruth_ and the opposite of {{< definition-relref "True" >}}; behaves like the _integer_ `0`, except that it will always be displayed as {{< definition-relref "False" >}}.

From late Old English, borrowed via the Old French **_faus_** from the Latin **_falsus_**; the general meaning is of "fake, incorrect, mistaken, or deceitful". In logic the meaning is not so sinister, it just means "that which is not true", and in computer programming it's usually a proxy for the binary digit 0.
{{< /definition >}}

In some lower-level languages you would probably just use `1` and `0` for these, but in Python they've been given special keywords to make it obvious that you're working with the _logical_ meaning instead of the _numerical_ one.

It's important to understand that in Python _every_ OBJECT (hence ever VALUE and COLLECTION, and therefore every EXPRESSION), has a _logical_ value, in that it's considered to be logically equivalent to either True or False. Testing the state of that logical value is known as [truth-value testing][truth-value], and as you'll see below keywords like {{< definition-relref "and" >}}, {{< definition-relref "or" >}}, and {{< definition-relref "if" >}} all rely on truth-value testing for their operation.

  [truth-value]: https://docs.python.org/3/library/stdtypes.html#truth-value-testing "Read about truth-value testing"

I will go into deeper detail about the specifics of truth-value testing in later articles, but for now you just need to know that most things are considered {{< definition-relref "True" >}} by default, except for "no value" VALUEs like `0`, {{< definition-relref "None" >}}, and `False` itself, as well as "no content" COLLECTIONs like `[]`.

#### The null value

This is most commonly used to represent the absence of any other VALUE.

{{< definition doclink="https://docs.python.org/3/library/stdtypes.html#the-null-object" >}}
None
: A special name for nothing whatsoever; technically Python's _null object_; it's considered equivalent to {{< definition-relref "False" >}} for truth-value testing, but essentially represents no value at all. Is very commonly used in Python, and will always appear as {{< definition-relref "None" >}}.

A Middle English pronoun from the Old English **_nan_**, meaning "not one" or "not any". The meaning in programming, however, relates more to **_null_**, which means "not [any] thing" or just "nothing". Python chose to use **_none_** because it's a more commonly familiar word. It also helps to distinguish it from the use of the special value NULL in the C programming language, which has a similar meaning but behaves in a _very_ different way.
{{< /definition >}}

The notion of making _something_ that explicitly represents _nothing_ might seem a little odd, at first, but the need for {{< definition-relref "None" >}} becomes obvious when you start building _useful_ code.

### Three for Making Decisions

Being able to tell if something is considered {{< definition-relref "True" >}} or {{< definition-relref "False" >}} isn't very useful unless you have the means to take different actions based on that knowledge. For that _most_ programming languages have some notion of _conditional operations_. In Python there are three keywords dedicated to conditional tasks.

{{< definition doclink="https://docs.python.org/3/reference/compound_stmts.html#the-if-statement" >}}
if
: Starts a conditional BLOCK by checking the _truth-value_ of the EXPRESSION that follows it; the STATEMENT(s) indented underneath the {{< definition-relref "if" >}} will be executed only if the EXPRESSION is considered {{< definition-relref "True" >}}.

A Middle English conjunction from the Old English **_gif_** which means, "in the event" or "whether" or, oddly, just "**_if_**". Has many Scandinavian/Germanic relatives, and possibly arrives via an Old Norse term for "doubt, hesitation". The general use is to make one word or phrase conditional on another being true, as in "_if_ it is raining, open your umbrella". The sense in computing is more formal but essentially the same; "_if_ [this condition is true], then [do some action].
{{< /definition >}}

{{< definition >}}
elif
: Optionally _continues_ a conditional by adding another BLOCK; if present it _must_ follow either the initial {{< definition-relref "if" >}} or another {{< definition-relref "elif" >}}. Behaves exactly like an {{< definition-relref "if" >}}, except that its conditional EXPRESSION will only be evaluated when no previous {{< definition-relref "if" >}}/{{< definition-relref "elif" >}} STATEMENT has evaluated as {{< definition-relref "True" >}}.

Not a proper English word, but instead a [portmanteau][portmanteau] that contracts **_else_** and **_if_** into a single artificial word, **_elif_**. Together it means "otherwise, if" or "as an alternative, if", both of which imply that the action controlled by the **_elif_** is contingent on the outcome of some previous test or tests. So, in computing, "**_else_** [after checking some prior condition] **_if_** [this other condition is True], then [do some other action]".

  [portmanteau]: https://en.wikipedia.org/wiki/Portmanteau "Explanation of portmanteau"
{{< /definition >}}

{{< definition >}}
else
: Optionally _terminates_ a conditional by adding a final BLOCK; if present it _must_ follow the last {{< definition-relref "if" >}}/{{< definition-relref "elif" >}} in the BLOCK. If no previous {{< definition-relref "if" >}}/{{< definition-relref "elif" >}} STATEMENT evaluated to {{< definition-relref "True" >}} then the indented STATEMENT(s) below {{< definition-relref "else" >}} will be run.
: Can also be used to terminate blocks started with other KEYWORDs; see {{< definition-relref "for" >}}, {{< definition-relref "while" >}}, and {{< definition-relref "try" >}} below.

An adverb from the Old English **_elles_**, meaning "[to do] instead of [some other action]" or "as an alternative", or just "otherwise". In computing it means "[check if any prior condition is true] **_else_** [perform some final action]". It is used to take some default or fallback action when no better, more specific action should be taken.
{{< /definition >}}

Conditionals are key to a lot of Python programming, and are needed to better explain some of the keywords that follow, so I'll provide a few examples of how they work.

Sometimes you only want to take _any_ action if some condition is met; this is the simplest form:

```python
if EXPRESSION:
    STATEMENT
```

Many situation are binary, though, and so you'll always want to take some fallback action if the condition is _not_ met:

```python
if EXPRESSION:
    STATEMENT_A
else:
    STATEMENT_B
```

In complex cases you may need to have any number of alternative actions based on mutually exclusive conditions, as well as a fallback:

```python
if EXPRESSION_A:
    STATEMENT_A
elif EXPRESSION_B:
    STATEMENT_B
else:
    STATEMENT_C
``` 

For the middle, "either/or" case there's another form you will sometimes see, known as the _ternary operator_ form. This is useful mainly because, unlike a standard {{< definition-relref "if" >}} conditional, it behaves like an EXPRESSION, and the value it evaluates to can be directly assigned to a NAME:

```python
NAME = STATEMENT_A if EXPRESSION else STATEMENT_B
```

Which is a much shorter way of writing:

```python
if EXPRESSION:
    NAME = STATEMENT_A
else:
    NAME = STATEMENT_B
```
We'll find this useful when we look at the OPERATOR-like keywords below.

### Five That Are Operators

The next five keywords all behave like an OPERATOR to denote actions performed on OBJECTs and/or EXPRESSIONS.

#### Boolean logic operators

These are used for making meaningful comparisons between things based on their _truth-value_.

{{< definition doclink="https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not">}}
not
: A _unary_ OPERATOR that inverts the _truth-value_ of whatever follows it, as in `not EXPRESSION`.
: Can be used to invert the meaning of another KEYWORD; see {{< definition-relref "is not" "is" >}} and {{< definition-relref "not in" "is_in" >}} below.

A Middle English adverb from the Old English _nawiht_, implying "nothing" or "zero". The general meaning today negates (or flips) the meaning of the word or phrase that follows it. Compare "I do have apples" to "I do **_not_** have apples". In programming, however, the specific meaning comes from [logical negation][not], and thus **_not_** negates true to false, and vice versa.

  [not]: https://en.wikipedia.org/wiki/Negation "Read about logical negation"
{{< /definition >}}

This is Python's _Boolean negation_ OPERATOR, used whenever you need the opposite of the truth-value of a thing. It is _unary_, which means that it acts on whatever is to its immediate right.

The usage of {{< definition-relref "not" >}} is straightforward:

```python
not EXPRESSION
```

If `EXPRESSION` is considered {{< definition-relref "True" >}} then `not EXPRESSION` evaluates to {{< definition-relref "False" >}} and otherwise it evaluates to {{< definition-relref "True" >}}.

That can be easier to understand if you think of {{< definition-relref "not" >}} as working like the following _ternary_ {{< definition-relref "if" >}}:

```python
True if EXPRESSION else False
```
 
{{< definition doclink="https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not">}}
and
: A _binary_ OPERATOR that checks the _truth-value_ of two things, evaluating to the thing on the left if it tested {{< definition-relref "False" >}}, otherwise to the thing on the right.

An ancient Old English conjunction with Germanic roots vaguely meaning "thereupon" or "next [to]" and used to combine two words or phrases, as in "coffee **_and_** tea". The meaning in Python, however, comes entirely from [logical conjunction][and], and implies that either _both_ things it combines are true or the whole combination is false.

  [and]: https://en.wikipedia.org/wiki/Logical_conjunction "Read about logical conjunction"
{{< /definition >}}

This is Python's _Boolean conjunction_ OPERATOR; used whenever you need to test if _both_ sides of the {{< definition-relref "and" >}} are considered {{< definition-relref "True" >}}. It is a _short-circuiting_ operation; if the left-hand EXPRESSION is considered {{< definition-relref "False" >}} the entire operation is considered {{< definition-relref "False" >}} and the right-hand side will never be evaluated at all. And unlike {{< definition-relref "not" >}} it does not necessarily evaluate to either {{< definition-relref "True" >}} or {{< definition-relref "False" >}}, evaluating instead to either the left side (if considered {{< definition-relref "False" >}}) or the right side.

Thus the usage:

```python
EXPRESSION_A and EXPRESSION_B
```

Can be thought of as working like the following _ternary_ {{< definition-relref "if" >}}:

```python
EXPRESSION_B if EXPRESSION_A else EXPRESSION_A
```

Which is why you may one day find yourself surprised to find that `True and 1` evaluates to `1` while `1 and True` evaluates to {{< definition-relref "True" >}}.
  
{{< definition doclink="https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not">}}
or
: A _binary_ OPERATOR that checks the _truth-value_ of two things, evaluating to the thing on the left if it tested {{< definition-relref "True" >}}, otherwise to the thing on the right.

Derived from the Old English conjunction **_oþþe_**, meaning "either", and implying that either of the ideas conjoined are acceptable, as in "coffee **_or_** tea". In Python the meaning comes from [logical disjunction][or], and implies that either _one_ of the things it combines is true or the whole combination is false.

  [or]: https://en.wikipedia.org/wiki/Logical_disjunction "Read about logical disjunction"
{{< /definition >}}

This is Python's _Boolean disjunction_ OPERATOR; used whenever you need to test if _either_ side of the {{< definition-relref "or" >}} is considered {{< definition-relref "True" >}}. It is a _short-circuiting_ operation; if the left-hand EXPRESSION is considered {{< definition-relref "True" >}} the entire operation is considered {{< definition-relref "True" >}} and the right-hand side will never be evaluated at all. Also, unlike {{< definition-relref "not" >}} it does not necessarily evaluate to either {{< definition-relref "True" >}} or {{< definition-relref "False" >}}, evaluating instead to either the left side (if considered {{< definition-relref "True" >}}) or the right side.

Thus the usage:

```python
EXPRESSION_A or EXPRESSION_B
```

Can be thought of as working like the following _ternary_ {{< definition-relref "if" >}}:

```python
EXPRESSION_A if EXPRESSION_A else EXPRESSION_B
```

This subtlety can catch you out when you find that `True or 1` evaluates to {{< definition-relref "True" >}} but `1 or True` evaluates to `1`.

#### Identity checking operator(s)
{{< definition doclink="https://docs.python.org/3/reference/expressions.html#is" >}}
is
: A _binary_ OPERATOR that tests if the OBJECT on the left has the same [identity][identity] as the OBJECT on the right and then evaluates to either {{< definition-relref "True" >}} or {{< definition-relref "False" >}}.
: Can be inverted by {{< definition-relref "not" >}} to become the {{< definition-relref "is not" "is" >}} operator.

  [identity]: "https://en.wikipedia.org/wiki/Identity_(object-oriented_programming)" "Read about identity in programming"

An Old English verb from the Germanic stem **_\*es-_**; it's the third person singular present indicative form of the word **_be_**, so it generally means "to be [a thing]". In Python its meaning is specific to _identity_, and implies something more like "to be [some unique thing]".
{{< /definition >}}

The usage is straightforward:

```python
EXPRESSION_A is EXPRESSION_B
```

And the usage with {{< definition-relref "not" >}} is:

```python
EXPRESSION_A is not EXPRESSION_B
```

The notion of _identity_ is a little abstract, but think of it like this: Tom and Bob are twins, they're the same height, age, and weight, and they share the same birthday, but they _do not_ have the same identity. Tom is Tom, and Bob is Bob, but Tom is not Bob.

In most implementations of Python the identity of an OBJECT can be thought of as its unique address in memory, and since _every_ OBJECT you work with will have its own unique address, {{< definition-relref "is" >}} is usually only useful for telling if a NAME refers to a specific OBJECT:

```python
NAME is OBJECT
NAME is not OBJECT
```

Or for testing if two different NAMEs refer to the same OBJECT in memory.

```python
NAME is OTHER_NAME
NAME is not OTHER_NAME
```

There _are_ however some special cases: for instance, {{< definition-relref "True" >}}, {{< definition-relref "False" >}}, and {{< definition-relref "None" >}} are all [singletons][singleton] in memory, meaning there is only _ever_ one copy of {{< definition-relref "True" >}} in _any_ Python program. For the most part this is just a space-saving detail you don't need to worry about, but it explains why in Python we use `VALUE == True` and _not_ `VALUE is True` when checking if something is considered _equivalent_ to {{< definition-relref "True" >}}. Testing _identity_ is _not_ the same as testing _value_.

  [singleton]: https://en.wikipedia.org/wiki/Singleton_pattern "Read about the singleton pattern"

For this reason the uses of {{< definition-relref "is" >}} are limited and specific, which is why you'll only rarely see {{< definition-relref "is" >}} and {{< definition-relref "is not" "is" >}} used in practice.

#### Membership testing operator(s)
{{< definition doclink="https://docs.python.org/3/reference/expressions.html#membership-test-operations" >}}
in
: A _binary_ OPERATOR that tests if the OBJECT on the left is a member of the COLLECTION on the right and then evaluates to either {{< definition-relref "True" >}} or {{< definition-relref "False" >}}. Also known as Python's _inclusion operator_.
: Can be inverted by {{< definition-relref "not" >}} to become the {{< definition-relref "not in" "in" >}} _exclusion operator_.
: Also used with {{< definition-relref "for" >}}, see below.

A Middle English merger of the Old English words **_in_**, meaning "among", and **_inne_**, meaning "within" or "inside". The merged word has many usages and meanings, but the general sense here is from the prepositional form, which implies that some thing is contained within or inside some larger thing, as in "a page **_in_** a book" or "a book **_in_** a library". In Python it is specifically used for _membership testing_, when checking if an item is contained within a group of items.
{{< /definition >}}

The usual usage of {{< definition-relref "in" >}} is to test if an OBJECT is a member of a specific CONTAINER:

```python
OBJECT in CONTAINER
```

Or to test if OBJECT is {{< definition-relref "not" >}} a member of CONTAINER:

```python
OBJECT not in CONTAINER
```

It can be tempting to think you can use {{< definition-relref "is" >}} with {{< definition-relref "in" >}}, but that's invalid syntax. It helps to remember that since {{< definition-relref "is" >}}, {{< definition-relref "is not" "is" >}}, {{< definition-relref "in" >}}, and {{< definition-relref "not in" "in" >}} are all binary OPERATORs they _must_ have either an OBJECT or EXPRESSION on either side, _not_ another KEYWORD.

### Four Used to Loop

The above keywords give you everything you need to perform simple decision making and to take basic actions, but they're useless whenever you need to do something _repeatedly_; that's where _looping_ comes in. In Python the following four keywords give you everything you need to do that.

#### Starting a loop

There are two ways to start a loop in Python, and they're conceptually pretty similar, but your choice of which depends a great deal on exactly what you need to do with that loop.

##### Looping until some condition is reached

{{< definition doclink="https://docs.python.org/3/reference/compound_stmts.html#the-while-statement" >}}
while
: Starts a loop BLOCK by testing a the truth-value of an EXPRESSION; will iterate continuously until EXPRESSION evaluates to False.

From the Old English word **_hwile_** for "a duration of time", but here we're using the conjunctive form which implies "[during the] time [that something is true]" or "for as long as [something is true]". In programming languages the keyword is always associated with something to _test_ and something to _do_, so the meaning becomes "**_while_** [the test is true], [do something]".
{{< /definition >}}

The form of a {{< definition-relref "while" >}} loop BLOCK is always the same:

```python
while EXPRESSION:
    STATEMENT
```

If the EXPRESSION evaluates as {{< definition-relref "True" >}} then STATEMENT will be reached and executed. When the end of the indented BLOCK is reached, control returns immediately to the top, then EXPRESSION is tested again, and so on. So long as EXPRESSION evaluates as {{< definition-relref "True" >}} the entire indented BLOCK will be run again and again.

The {{< definition-relref "while" >}} loop can also _optionally_ be terminated by an {{< definition-relref "else" >}} BLOCK:

```python
while EXPRESSION:
    [...]
else:
    STATEMENT
```

In this case the STATEMENT inside the {{< definition-relref "else" >}} block will executed if the {{< definition-relref "while" >}} loop runs all the way to completion (its test evaluates to {{< definition-relref "False" >}}) _without_ encountering {{< definition-relref "break" >}}. This can be useful when there is some cleanup action that needs to occur when a {{< definition-relref "while" >}} loop has exited naturally.

The {{< definition-relref "while" >}} is the most basic form of loop, but it's a little dangerous if not used with care. This is because any EXPRESSION that _always_ evaluates as {{< definition-relref "True" >}} will run _forever_. For this reason it's generally important to design the EXPRESSION so that it will _eventually_ evaluate to {{< definition-relref "False" >}}.

##### Looping through the members of a COLLECTION

{{< definition doclink="https://docs.python.org/3/reference/compound_stmts.html#the-for-statement" >}}
for
: Starts a loop BLOCK that will iterate _once_ over a COLLECTION, visiting every item in it.
: Can also be marked with {{< definition-relref "async" >}}, to start an {{< definition-relref "async for" "async" >}} loop, see below.

An Old English word via the German **_für_** with a great many meanings; the general meaning is taken from a prepositional sense of "[performing an action] on behalf of [some thing]". In computing, though, the meaning is actually taken from the contraction of the word **_for_** with either **_every_** (meaning "each [item] in a group") or **_each_** (meaning "all [of a group]") to form **_for every_** or **_for each_**, both of which mean "[to perform an action] on behalf of each item [in a group]". In programming languages that descend from ALGOL [**_for_**][for] has traditionally been the most common name for such a loop, with **_do_** used in a smaller number of languages. Python takes the name from the traditional usage in ALGOL via C, however it is more accurate to describe Python's version as a [**_foreach_**][foreach] loop, because there is no explicit counter and the thing being looped over must be [_iterable_][iteration].

  [for]: https://en.wikipedia.org/wiki/For_loop "Read about the for loop"
  [foreach]: https://en.wikipedia.org/wiki/Foreach_loop "Read about the foreach loop"
  [iteration]: https://en.wikipedia.org/wiki/Iteration "Read about iteration"
{{< /definition >}}

The usage of {{< definition-relref "for" >}} consistently involves assigning a user-assigned NAME to every OBJECT {{< definition-relref "in" >}} a COLLECTION.

```python
for NAME in COLLECTION:
    STATEMENT
```

Thus {{< definition-relref "for" >}} every item in the COLLECTION the NAME will refer to that item _inside_ the scope of the BLOCK; this allows the STATEMENT to use NAME to act on that thing.

This can be a little easier to grasp if you think of {{< definition-relref "for" >}} as a specialized form of {{< definition-relref "while" >}} loop:

```python
while [items remain in COLLECTION to visit]:
    NAME = [increment to the next item]
    STATEMENT
```

But obviously the {{< definition-relref "for" >}} loop is much simpler to work with, as you don't need to worry about implementing the machinery necessary to track the start and stop conditions of the loop. You'll find that you can, and usually should, use a {{< definition-relref "for" >}} loop whenever you're visiting the individual contents of a COLLECTION, rather than risk a runaway {{< definition-relref "while" >}} loop.

The {{< definition-relref "for" >}} loop can also _optionally_ be terminated by an {{< definition-relref "else" >}} BLOCK:

```python
for NAME in COLLECTION:
    [...]
else:
    STATEMENT
```

In this case the STATEMENT inside the {{< definition-relref "else" >}} block will executed if the {{< definition-relref "for" >}} loop has run to completion _without_ encountering {{< definition-relref "break" >}}. This can be useful when there is some cleanup action that needs to occur when a `for` loop has exited naturally.

#### Controlling a loop

You don't always want to simply run the loop to completion; there may be good reason to exit early, or to skip a round of the loop.

{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-break-statement" >}}
break
: Used to immediately interrupt the current loop iteration, ending the BLOCK it is found within. For this reason must _only_ be used within a loop BLOCK.

From the Old English word **_brecan_**, which has several forms and meanings. The noun form generally means "to damage, destroy, or render unusable", as in "to **_break_** a leg". Here, however, we use the alternative meaning "to interrupt [a continuous sequence]", as in "to **_break_** an electrical circuit". In programming it specifically means to interrupt a loop from inside that loop.
{{< /definition >}}

The {{< definition-relref "break" >}} statement always forms a line of its own, and it _must_ be used in either a {{< definition-relref "for" >}} or {{< definition-relref "while" >}} loop. The most common use is to stop a loop immediately if some particular condition is reached:

```python
while True:
    if EXPRESSION:
        break
    STATEMENT
```

```python
for NAME in COLLECTION:
    if EXPRESSION:
        break
    STATEMENT
```

This is particularly useful if there's some situation that warrants stopping the loop before it would normally be completed.

{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-continue-statement" >}}
continue
: Immediately skips the rest of the current loop BLOCK, allowing the loop to continue on to the next iteration. For this reason must _only_ be used within a loop BLOCK.

A Middle English verb borrowed via the Old French **_continuer_** from the Latin **_continuare_**. The general meaning used here is to "go forward or onward", "carry on", or "proceed". In programming it means to cause a loop to start executing the next iteration, skipping any instructions that follow it.
{{< /definition >}}

The {{< definition-relref "continue" >}} statement always forms a line of its own, and it must be used in either a {{< definition-relref "for" >}} or {{< definition-relref "while" >}} loop. The most common use is to skip to the next iteration of a loop immediately when some particular condition is reached:

```python
while True:
    if EXPRESSION:
        continue
    STATEMENT
```

```python
for NAME in COLLECTION:
    if EXPRESSION:
        continue
    STATEMENT
```

This is particularly useful if there's some situation that warrants skipping the current loop; for example if you only wanted to act on every second iteration.

### Three for Importing Other Things

All of the above, plus the _builtin_ functions we'll talk about in a later article, are sufficient to let you start using Python as a _scripting_ language, where you glue together things others have written with your own code to do some task you want to accomplish. But you need to be able to access those "things others have written" to do so. That's what Python's _import mechanism_ is for.

{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-import-statement" >}}
import
: Used to bring the functionality of an external MODULE into your own code.

A verb from the Middle English **_importen_**, via the Old French from the Latin **_importare_**. The general meaning is to "bring/carry [goods into this country] from abroad". In computing it means to bring or **_import_** some functionality _exported_ by another program written in the same language into the current program.
{{< /definition >}}

The most common usage is very simple, the keyword is followed by the MODULE you want to access:

```python
import MODULE
```

You can also import multiple MODULEs separated by commas:

```python
import MODULE_A, MODULE_B
```

And for organizational purposes you can put parentheses around them as well:

```python
import (MODULE_A, MODULE_B)
```

Any NAME inside the imported MODULE(s) can then be accessed within your own program using the _dot access_ pattern in the form MODULE.NAME. So, for instance, if you wanted to get the circumference of a circle:

```python
import math

radius = 3
circumference = math.tau * radius
```

Usually you'll find all the {{< definition-relref "import" >}} usage at the top of a MODULE, which makes it pretty easy to determine where such functionality comes from.

{{< definition >}}
from
: Modifies {{< definition-relref "import" >}} to allow you to import specific NAMEs from within an external MODULE.
: Can also be used with {{< definition-relref "raise" >}} and {{< definition-relref "yield" >}}, see below.

A Middle English word from the Old English **_fram_**, here we use the preposition form, with a general sense of "departure or movement away [from something]"; in computing we use a more specific sense of "taken **_from_** a source".
{{< /definition >}}

It's used to modify {{< definition-relref "import" >}} to import a specific NAME from a MODULE, rather than the _entire_ MODULE:

```python
from MODULE import NAME
```

If you wish to import more than one NAME they can be separated by commas:

```python
from MODULE import NAME_A, NAME_B
```

And for organizational purposes you can put parentheses around them as well:

```python
from MODULE import (NAME_A, NAME_B)
```

In all cases you can then use the imported NAME directly, so for instance if you want the area of a circle:

```python
from math import tau

radius = 3
area = tau * radius ** 2 / 2
```

The main reason for {{< definition-relref "from" >}} is to remove the need to have many references to a MODULE peppered throughout your code, but it's best reserved for when the MODULE has many NAMEs that it exports and you want to just use one or two.

{{< definition >}}
as
: Modifies {{< definition-relref "import" >}} to create an alternative NAME (or alias) for an imported NAME.
: Can also be used with {{< definition-relref "except" >}} and {{< definition-relref "with" >}}, see below.

From the Old English **_eallswā_** meaning "just so" or simply "all so", which makes it a reduced form of **_also_**. The usage here comes from the adverb form meaning "[to act] in the manner or role [of some other thing]". In Python it very specifically means "[from here on refer to this thing] **_as_** [this instead]".
{{< /definition >}}

Because {{< definition-relref "from" >}} exists there are two forms of usage:

```python
import MODULE as MODULE_ALIAS
from MODULE import NAME as NAME_ALIAS
```

The point of {{< definition-relref "as" >}} is to allow you to {{< definition-relref "import" >}} some MODULE or NAME but refer to it by some other name. This is useful if the original name is particularly long, would conflict with one already in use in your code, or could simply use some extra information in context.

```python
from math import pi as half_as_good_as_tau
```

### Five for Exceptional Situations

Now that you've got the basics down, you're getting into more complicated territory. What happens if you find yourself reaching a point in the code where you're in an obvious error state and you don't want to continue? This is where the notion of [exception handling][exceptions] come into play. We'll go into more detail on the standard Exceptions in later articles, but for now let's just say that an EXCEPTION is a special type of VALUE that signifies a specific issue that has come up in your program. That issue _might_ be an _error_, in which case you might want to crash out of the program, or it might be a signal that something _unusual_ but expected has occurred. Either way you need to be able to emit those signals from your own code, as well as catch and react to such signals emitted by other code.

  [exceptions]: https://en.wikipedia.org/wiki/Exception_handling "Article on exception handling"

#### To signal that there's a problem
{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-raise-statement" >}}
raise
: Used to raise a specified EXCEPTION, which will cause the program to stop immediately and exit if not handled by an {{< definition-relref "except" >}} BLOCK.
: If used without an argument inside an {{< definition-relref "except" >}} or {{< definition-relref "finally" >}} BLOCK, re-raises the EXCEPTION being handled by the BLOCK.

A Middle English word with _many_ meanings, but in this case it comes from the verb form meaning "to lift upright, build, or construct" or "to make higher". The meaning in computing is more specifically from a newer sense of "to mention [a question, issue, or argument] for discussion", as in "to **_raise_** attention [to an issue]". In several other programming languages **_throw_** is used with similar meaning.
{{< /definition >}}

The usage is _usually_ going to be:

```python
raise EXCEPTION
```

Quite rarely you might see the _chained_ form:

```python
raise EXCEPTION from OTHER_EXCEPTION
```

Which is used to indicate that the EXCEPTION being raised was _caused by_ (or _came from_) some other EXCEPTION. This isn't used often, but sometimes is useful when you attempt to handle an exception raised by other code but somehow cannot do so.

Lastly _inside_ an {{< definition-relref "except">}} BLOCK you can simply:

```python
raise
```

Which will re-raise whatever EXCEPTION is currently being handled inside that BLOCK.

#### To signal that a particular condition is not met
{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-assert-statement" >}}
assert
: Used to test if some EXPRESSION is considered True, and if not raise an AssertionError.

From the Latin **_assertus_**, with the general sense of "declared, protected, or claimed". In programming it specifically means to specify that a condition must be met at a particular point in the code, and to error if it is not.
{{< /definition >}}

The usage of {{< definition-relref "assert" >}} is usually going to be in the form:

```python
assert EXPRESSION
```

Which will simply {{< definition-relref "raise" >}} an AssertionError if EXPRESSION does not evaluate as {{< definition-relref "True" >}}.

An alternative form allows you to specify a message:

```python
assert EXPRESSION, "something is wrong!"
```

And this message will be incorporated into the AssertionError.

The {{< definition-relref "assert" >}} statement exists for you to test the things that _must_ be {{< definition-relref "True" >}} for your program to continue to work (we call these your _invariants_). This can be very helpful when developing and debugging, but should not be relied on, _at all_, in production code, as the person running your program can elect to disable all {{< definition-relref "assert" >}} statements by passing the `-O` command line option to Python. Basically you can imagine that {{< definition-relref "assert" >}} works like:

```python
if [the -O command line flag was not passed]:
    if not EXPRESSION:
        raise AssertionError
```

... except that if the `-O` flag was passed the {{< definition-relref "assert" >}} statement will simply be replaced by [`pass`]({{< relref "#pass">}}) and nothing whatsoever will happen.

#### To catch a signal and react to it

With both [`raise`]({{< relref "#raise">}}) and [`assert`]({{< relref "#assert">}}) in your toolkit you know how to signal an EXCEPTION, but how do you catch and react to (or ignore) one? This is where [Python's exception handling][handling] mechanism comes into play.

  [handling]: https://docs.python.org/3/tutorial/errors.html#handling-exceptions "Documentation on exception handling"

{{< definition doclink="https://docs.python.org/3/reference/compound_stmts.html#the-try-statement" >}}
try
: Starts an exception handler BLOCK; _must_ be followed either an {{< definition-relref "except" >}} BLOCK, an {{< definition-relref "else" >}} block or a {{< definition-relref "finally" >}} BLOCK in order to be valid syntax.

A verb borrowed from the Old French word **_trier_**, meaning to "test", "experiment", or "attempt to do". The meaning in Python is essentially the same, "[start a] test [of something that _may_ error]".
{{< /definition >}}

{{< definition >}}
except
: Optionally _continues_ an exception handler BLOCK by catching EXCEPTIONs; can (and _should_) be limited to specific types of EXCEPTION. More than one of these can follow a {{< definition-relref "try" >}} and each will be checked in turn until either the EXCEPTION is handled or no more {{< definition-relref "except" >}} statements remain.

A verb borrowed from the Middle French **_excepter_** and Latin **_exceptus_**; the original meaning is "to receive", but the more general uses it to "exclude [something]" or "object to [something]", as in "every fruit except apples". The meaning in Python is a little vague, but can be thought of as "catch, capture, or trap [an exception]". In fact in many other languages **_catch_** is used for the same purpose; Python's **_except_** is the exception to that rule.
{{< /definition >}}

{{< definition >}}
finally
: Optionally _cleans up_ an exception handler BLOCK to provide a means of _always_ performing some action whether or not the EXCEPTION was handled. _Must_ follow any {{< definition-relref "except" >}} BLOCKS and the optional {{< definition-relref "else" >}} BLOCK, if present. If no {{< definition-relref "except" >}} BLOCK is present then {{< definition-relref "finally" >}} _must_ terminate the exception handler.

From the Middle English **_fynaly_** meaning "at the end or conclusion" or just "lastly". It implies the very last thing to do in a sequence, which is the meaning here as well.
{{< /definition >}}

Exception handling is the first circumstance you've encountered in which one BLOCK _must_ be followed by another, and the rules are somewhat more complicated than anything you've yet seen. For instance there are _two_ different _minimal syntactically valid_ forms of exception handler:

```python
try:
    BLOCK
finally:
    STATEMENT
```

This form does not actually handle any EXCEPTION raised within BLOCK, it merely ensures that STATEMENT is run in all circumstances. Any EXCEPTION not handled will continue to "raise up" until it is either handled or crashes your program. This is useful for situations in which you want to do the same action (such as closing a file or database connection) whether or not there has been an error.

The second form _does_ handle an EXCEPTION:

```python
try:
    BLOCK
except:
    STATEMENT
```

**Note**: because this form will catch _any_ EXCEPTION, including several that are used by Python to perform critical operations, you should, practically speaking, **never** use the above form. Instead use the _minimum safe_ form:

```python
try:
    BLOCK
except EXCEPTION:
    STATEMENT
```

This ensures that the exception handler _only_ handles the EXCEPTION _type_ specified. The [hierarchy of built-in exceptions][hierarchy] in Python is complex and touches on concepts we can't cover in this article, but for now just know that `except Exception` is the _least_ specific {{< definition-relref "except" >}} statement you should ever use in production code.

  [hierarchy]: https://docs.python.org/3/library/exceptions.html#exception-hierarchy "Python's Exception hierarchy"

That minimum safe form, however, isn't particularly useful, because the STATEMENT can't actually know what EXCEPTION it's handling. Most of the time you'll see something like this:

```python
except EXCEPTION as NAME:
    STATEMENT
```

Which uses {{< definition-relref "as" >}} to provide an alias NAME that can be used to inspect the actual EXCEPTION that was raised. This can be very helpful for seeing precisely what went wrong, which will help you decide if you can ignore the problem or need to respond in some way.

You can also specify multiple different types of EXCEPTION to catch, which can be helpful if you want to respond to any of those forms in the _same_ way:

```python
except (EXCEPTION_A, EXCEPTION_B, EXCEPTION_C) as NAME:
    STATEMENT
```

And if you want to respond to them each in a _different_ way  you can just stack {{< definition-relref "except" >}} BLOCKS:

```python
except EXCEPTION_A as NAME:
    STATEMENT_A
except EXCEPTION_B as NAME:
    STATEMENT_B
```

You can also optionally use {{< definition-relref "else" >}} with an exception handler, so long as at least one {{< definition-relref "except" >}} statement is used, and as long as the {{< definition-relref "else" >}} is positioned _before_ any {{< definition-relref "finally" >}}:

```python
try:
    BLOCK_A
except EXCEPTION as NAME:
    BLOCK_B
else:
    STATEMENT
```

However this is relatively rare, because the STATEMENT indented under {{< definition-relref "else" >}} will _only_ be executed when no EXCEPTION was raised inside the {{< definition-relref "try" >}} BLOCK _and_ no {{< definition-relref "break" >}}, {{< definition-relref "continue" >}}, or {{< definition-relref "return" >}} statements were encountered within it.

As you've seen exception handling has some fairly dense syntax compared to the rest of Python. A fully fleshed out exception handler in a program that does something fairly complex, like interacting with a database, might involve all these parts.

```python
try:
    [connect to database]
    [query the database]
except ConnectionError as error:
    [log the error]
else:
    [log success]
finally:
    [close the connection]
```

But, thankfully, it's often not that complex, and you usually only have to deal with exception handling when something truly exceptional has happened.

### Four for Writing Functions

Now that you've got all the structures you need to write an arbitrarily complex program, with the ability to make decisions, loop, and handle errors, your biggest problem is going to be organizing those structures into re-usable units. For instance you don't want to type out a complex exception handler for every single time you connect to and query a database, as that would quickly lead to an unmanageable amount of repetition.

  [DRY]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself "Read about DRY"

One of the key mantras of programming is [Don't Repeat Yourself][DRY] (aka **DRY**); the less boilerplate, the better, and so you want to be able to create [subroutines][subroutine], which are the most basic form of _code re-use_. In Python the most common form of subroutine is the _function_, which comes in two primary forms.

  [subroutine]: https://en.wikipedia.org/wiki/Subroutine "Read about subroutines"

#### Anonymous (unnamed) functions

A lot of people teaching (and learning) Python tend to skip over anonymous functions, or treat them as an advanced feature, but that's really just because they're poorly named. The "anonymous" part just means the function isn't given a specific name at creation time. That might not sound like the easiest thing to re-use -- and you're right -- but it's useful to understand them before we head on to _named_ functions because they're fundamentally simpler and more constrained.

Unfortunately the powers that be decided that anonymous functions, already saddled with a bad and confusing name, should _definitely_ get a worse name in Python.

{{< definition doclink="https://docs.python.org/3/reference/expressions.html#lambda" >}}
lambda
: Used to define a CALLABLE [anonymous function][anonymous] and its _signature_.

  [anonymous]: https://en.wikipedia.org/wiki/Anonymous_function "Read about anonymous functions"

The 11th letter of the Classical Greek alphabet, **_λ_**; it has no general meaning in English. In Python it is used because anonymous functions are a fundamental unit of [Alonzo Church's Lambda Calculus][lambda], which provides much of the mathematical underpinnings of modern computation. As an honor, that's nice; in reality **_lambda_** would be used more often if it had a more fun name.

  [lambda]: https://en.wikipedia.org/wiki/Lambda_calculus "Read about the Lambda Calculus"
{{< /definition >}}

Despite the name a {{< definition-relref "lambda" >}} is actually the conceptually simplest form of function in Python, because you can think of it as a just a way of creating a delayed-evaluation EXPRESSION that's stated with a specific form:

```python
lambda : EXPRESSION
```

Which evaluates to a CALLABLE that will evaluate the EXPRESSION that comes _after_ the colon only when the CALLABLE is itself called. To call it you use the _call syntax_ that is common to all Python CALLABLEs, however since the {{< definition-relref "lambda" >}} is itself an EXPRESSION you need to surround it with parentheses to do that.

```python
(lambda : EXPRESSION)()
```

And _voila_, everything you've just written will instantly be replaced by whatever the inner EXPRESSION evaluates to.

Thus all three of these are entirely identical:

```python
x = (lambda : 2 + 2)()
x = 2 + 2
x = 4
```

But just delaying an EXPRESSION isn't really the most useful tool. So the {{< definition-relref "lambda" >}} introduces the idea of a _function signature_: you can add a NAME to the left side of the colon and the thing that NAME refers to will able to be used inside the inner EXPRESSION when it evaluates. This name is known as a _parameter_ of the function.

Here's a {{< definition-relref "lambda" >}} with a single parameter:

```python
lambda NAME: EXPRESSION
```

And here's one with two parameters:

```python
lambda NAME_A, NAME_B: EXPRESSION
```

And when we want to use the {{< definition-relref "lambda" >}} we just call it, passing in a concrete VALUE for every parameter in the signature:

```python
(lambda NAME_A, NAME_B: EXPRESSION)(VALUE_A, VALUE_B)
```

Which you can imagine can be useful if we want to calculate the area of a rectangle:

```python
lambda width, height: width * height
```

But, again, we're going to end up writing that a lot if we don't assign it to a NAME:

```python
area = lambda width, height: width * height
square = area(2, 2)
rectangle = area(3, 5)
```

Great! The `square` is now `4` and `rectangle` is `15`; we've got the basis of code re-use!

But {{< definition-relref "lambda" >}} is going to get pretty nasty when the EXPRESSION starts to get long. And beyond that there are some pretty significant limitations, since we actually _cannot_ execute many kinds of STATEMENT within a {{< definition-relref "lambda" >}}, much less an arbitrary BLOCK. They have their place, but maybe there's a better and more flexible way?

Since we've just gone and assigned what is supposed to be an _anonymous_ (which means "has no name") function to a NAME, let's look at how we should _usually_ write functions in Python.

#### Named functions

The _named_ function builds on the ideas of the {{< definition-relref "lambda" >}} but take them to a _much_ more flexible place, allowing you to re-use large chunks of code quite easily. They're a little more subtle to master too, because they don't evaluate exactly like an EXPRESSION. In fact by default they'll always evaluate to {{< definition-relref "None" >}} unless you explicitly tell them to do otherwise.

{{< definition doclink="https://docs.python.org/3/reference/compound_stmts.html#function-definitions" >}}
def
: Used to define a _named_ function and its _signature_, the indented BLOCK that follows can then be re-used by calling that NAME using the `function()` syntax.
: If used inside a {{< definition-relref "class" >}} defines a named _method_ instead, which is called using the `class.method()` syntax.
: Can also be marked with {{< definition-relref "async" >}}, to start an {{< definition-relref "async def" "async" >}}, see below.

A contraction of the word **_define_**, which comes via the Middle English **_deffinen_** from Old French and Latin roots. It's a verb that means "to specify or fix [the meaning of a word or phrase]". In Python it is used specifically to create a named subroutine. In other languages **_define_**, **_fn_**, **_fun_**, **_func_**, **_function_**, and **_let_** are often used instead.

{{< /definition >}}

Because {{< definition-relref "def" >}} can be used to create arbitrarily complex CALLABLEs, it's going to require some explanation. Essentially it's used to create a new NAME that refers to a CALLABLE. In fact, from now on let's just use FUNCTION to mean exactly that:

```python
def FUNCTION():
    STATEMENT
```

This defines a FUNCTION that can be called using `FUNCTION()`, which will then execute every STATEMENT inside the indented BLOCK. As you can see it's conceptually equivalent to the "named" {{< definition-relref "lambda" >}} form you saw earlier. Compare these two forms:

```python
def FUNCTION(NAME_A, NAME_B): STATEMENT
FUNCTION = lambda NAME_A, NAME_B : STATEMENT
```

And you'll see they're _very_ similar, except that the {{< definition-relref "def" >}} version can run an arbitrary number of STATEMENTs[^2].

  [^2]: Putting {{< definition-relref "def" >}} on a single line makes the equivalence with {{< definition-relref "lambda" >}} more obvious, but for the sake of readability don't do this very often.

These STATEMENTs will be executed within the _local scope_ of the function, meaning that _any_ NAME assigned _inside_ the function cannot be _directly_ seen or accessed  by any code _outside_ the function. In this example there are no such names, but there will be as soon as we change the _signature_ of the function:

```python
def FUNCTION(NAME):
    STATEMENT
```

And just as with {{< definition-relref "lambda" >}} we can have multiple parameters:

```python
def FUNCTION(NAME_A, NAME_B):
    STATEMENT
```

Which let's us build the `area` function we made before with a {{< definition-relref "lambda" >}}:

```python
def area(width, height):
    width * height

square = area(2, 2)
rectangle = area(3, 5)
```

Except, wait a minute ... didn't I say just above that {{< definition-relref "def" >}} functions evaluate to {{< definition-relref "None" >}} when called? Yep, right now both `square` and `rectangle` are assigned to {{< definition-relref "None" >}}. We've calculated two areas, but then discard them again as soon as the _local scope_ of `area` is closed. Now, how the heck do we get the area _out_ of `area`, anyway?

##### Stop the function and give back a value
{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-return-statement" >}}
return
: Used to immediately give up control and end execution of the function at the point at which it is encountered. If followed by an EXPRESSION, that is evaluated first and the resulting OBJECT is given back to the caller of the function. If no EXPRESSION is present {{< definition-relref "None" >}} is returned instead. Has no meaning outside a function, thus if present at all it _must_ be inside a BLOCK that follows a {{< definition-relref "def" >}}.

A Middle English verb from the Old French **_retourner_**, meaning "to turn back" or "to go back [to a former position]". In computing it has two meanings:

1. The intransitive meaning is "to give back (or relinquish) control [to the calling procedure]", as in "when the function exits it will **_return_** control".
2. The transitive meaning is "to pass [some data] back to the calling procedure", as in "this function will **_return_** the current time".

In Python both meanings are combined, since a function will always **_return_** both control _and_ data to the caller.
{{< /definition >}}

The most basic usage of {{< definition-relref "return" >}} immediately ends the function and returns {{< definition-relref "None" >}} to the caller:

```python
return
```

This form is relatively rarely used; as mentioned before a function _always_ evaluates to {{< definition-relref "None" >}} by default; thus you can imagine that {{< definition-relref "return" >}} is the implicit last line of _every_ function.

Because of that it is much more common to see:

```python
return EXPRESSION
```

Which immediately evaluates the EXPRESSION and returns the resulting OBJECT back to the caller.

You can also use {{< definition-relref "return" >}} to pass back more than one OBJECT:

```python
return EXPRESSION_A, EXPRESSION_B
```

This evaluates each EXPRESSION in turn, ends the function, and returns a [**tuple**][tuple] (a type of fixed-length COLLECTION) containing one OBJECT for each EXPRESSION.

  [tuple]: https://docs.python.org/3/library/functions.html#func-tuple "Read about the tuple type"

This multiple form is also relatively rare, as it can be a bit of a surprise to the user of the code, and so requires a bit more effort in documentation, but it can be convenient for internal functions that you don't intend to be used by others.

What you'll notice is that {{< definition-relref "return" >}} _terminates_ a function at the moment it's evaluated. Anything below that point in the function essentially doesn't exist (with one exception, the {{< definition-relref "finally" >}} block inside an exception handler). So how would you handle situations in which you needed to give back data, but continue to work afterwards?

##### Pause the function and give back a value
{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-yield-statement" >}}
yield
: Used to immediately pause execution and temporarily give up control at the point at which it is encountered. If followed by an EXPRESSION, that is evaluated first and the resulting OBJECT is yielded back to the caller of the function; if no EXPRESSION is present {{< definition-relref "None" >}} is yielded instead. Has no meaning outside a function, thus if present at all it _must_ be used inside a BLOCK that follows a {{< definition-relref "def" >}}.
: Can be modified by {{< definition-relref "from" >}} to form {{< definition-relref "yield from" "yield" >}}, see below.

Etymologically the oddest word in this list; derives from the Middle English **_yielden_** and the Old English **_gieldan_**, both of which mean "to pay", and share their root with the Old Norse **_gjald_** and the German **_geld_**, both of which mean "money". Today **_geld_** means an ancient form of compelled tax or ransom, but it also means "to castrate". Historically the Dangeld was a tax raised on the English by their king. This tax was raised to pay waves of Danish Vikings to, presumably, not castrate the English (or, at the very least, their king). None of this is directly important here, but might explain a little of why the meaning in computing derives from both "to give way and relinquish control", as in "**_yield_** to oncoming traffic", and "to give back [a result or return on investment]" as in "the fund has a **_yield_** of 5% per year". In both cases the implication is that the situation is not yet final, and is likely recurring: you **_yield_**, then you wait, then you **_yield_** again.

In Python it helps to remember an allegory: {{< definition-relref "return" >}} is Death, and comes exactly once, while {{< definition-relref "yield" >}} is Taxes, and may only end when Death arrives.
{{< /definition >}}

The usage of {{< definition-relref "yield" >}} is similar to {{< definition-relref "return" >}}:

```python
yield
```

```python
yield EXPRESSION
```

```python
yield EXPRESSION_A, EXPRESSION_B
```

However _any_ function that uses {{< definition-relref "yield" >}} actually returns a special kind of COLLECTION known as a GENERATOR when called. Unlike a normal COLLECTION a GENERATOR does not hold all of its items in memory simultaneously, but instead "generates" each item as required by running through the function until {{< definition-relref "yield" >}} is encountered and it gives forth an item. The GENERATOR pauses execution at that point, allowing the code using the GENERATOR to work with that item. When desired it can request the next item, at which point the GENERATOR continues running to the next {{< definition-relref "yield" >}}, and so on until there are no more {{< definition-relref "yield" >}} statements left to run or a {{< definition-relref "return" >}} is encountered.

This is what allows the next form:

```python
yield from GENERATOR
```

Which is a specialized use case that allows you to write a GENERATOR that will {{< definition-relref "yield" >}} every item, in turn, from _another_ GENERATOR.

A thorough explanation of GENERATORs is outside the scope of this series of articles, as they're a fairly advanced topic. For now it's sufficient to know that if you encounter {{< definition-relref "yield" >}} you're looking at a GENERATOR.

### Three for Manipulating Namespaces

Now that you understand the basics of function, you'll need to know about [namespaces][namespaces], as they become very important when you start building more complex programs.

At its simplest a namespace is essentially just the place where Python stores any NAME you create, so they're used whenever Python needs to look up the OBJECT referred to by that NAME. Each namespace has a _scope_, which limits how long the namespace "lives" and whether or not any NAME within it is _readable_ and/or _writable_ by a given STATEMENT. Namespaces form a hierarchy, however, so the rules can be a bit tricky to remember.

  [namespaces]: https://en.wikipedia.org/wiki/Namespace "Read about namespaces"

In any given namespace a STATEMENT can:

1. both _read_ and _write_ any NAME defined in its own namespace
1. _read_, but not _write_, any NAME defined in an enclosing _parent_ namespace
1. neither _read_ nor _write_ any NAME defined in a _sibling_ or _child_ namespace

At the top level is Python's own namespace, which contains all the _builtin_ NAMEs that Python provides for you. This namespace _cannot_ be written to, and any NAME in it essentially lives forever.

Next comes the _global_ namespace, which is the namespace of the MODULE you're working in; it becomes the parent of all other namespaces created within that MODULE. Any NAME defined here _usually_ lives for the duration your program is running.

Next, each CALLABLE you create gets its own unique _local_ namespace _when it is called_; any NAME created here lives only as long as the CALLABLE is running, and when it finishes both the NAME and the OBJECT it refers to will be destroyed, unless either {{< definition-relref "return" >}} or {{< definition-relref "yield" >}} is used to pass it back to the calling scope.

Since you can define a CALLABLE that is nested _inside_ another CALLABLE you can build a namespace hierarchy of arbitrary depth, so any given NAME might exist in any number of namespaces further and further removed from where you're actually trying to use that NAME. This can get unwieldy to think about pretty quick, though, which is why we _try_ to limit the amount of nesting we do in practical code.

The assignment of a new NAME is pretty straightforward: unless modified by one of the keywords below a NAME is _always_ assigned in the scope in which the assignment STATEMENT occurs.

But the _use_ of a NAME is a little less obvious: when used in a STATEMENT Python first searches for the NAME in the immediate _local_ scope. If it cannot find the NAME then it searches the immediate parent (known as the _nonlocal_) scope, and then it keeps searching each successive parent scope until it either finds the NAME or cannot resolve it and errors.

All of this usually somewhat invisible machinery exists to allow you to write code using NAMEs that are appropriate and clear to the scope in which you're working. So long as it isn't a keyword and you don't _need_ to use the NAME from an ancestor's scope you can use whatever NAME you want locally and not worry about it overwriting anything _outside_ its own scope.

_Most_ of the time you don't want to fool around with that machinery, but every so often there's a good reason to. Or a bad one that's gotten you confused.



#### Write to the top from anywhere

In _extremely rare_ circumstances you want to directly manipulate the _global_ namespace in a way you wouldn't normally be allowed.

{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-global-statement" >}}
global
: Used to declare a NAME as part of the _global_ namespace; the NAME _cannot_ have been used previously in the same namespace. In effect this allows a _local_ STATEMENT to both create and assign to a _global_ NAME it otherwise could only read. _Can_ be used within the global namespace, but has no effect.

An adjective borrowed from the French, with the general meaning of "worldwide" and "universal". In computing the meaning is specifically "[a NAME that is] accessible by all parts of a program". In Python it is both the top-most _namespace_, which is _readable_ from within all functions and methods, but is also a keyword that binds a _local_ NAME into the **_global_** namespace, allowing it to be _writable_ from within that _local_ namespace.
{{< /definition >}}

The usage is quite simple; the main restriction is that it cannot appear _after_ the NAME has been used:

```python
global NAME
NAME = EXPRESSION
```

You should be aware that the use of {{< definition-relref "global" >}} is an _immediate_ [code smell][stank], as its use is _almost always_ an indication of bad coding habits, because it _usually_ can -- and almost certainly _should_ -- be replaced with _argument passing_ and _return values_. There are data structures and dynamic code generation tasks that would be impossible to build without it, but the _odds_ are if you're thinking about using it, **don't**.

  [stank]: https://en.wikipedia.org/wiki/Code_smell "Read about code smell"

#### Write to the parent from the child

Slightly more often there's a need for the child to tell the parent what to do.

{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-nonlocal-statement" >}}
nonlocal
: Used exclusively inside _nested_ functions / methods (also known as _closures_) to bind a _pre-existing_ NAME in the _parent_'s namespace. This allows a STATEMENT in the child to have write access to a NAME defined in its parent. _Must_ appear before any reference to that NAME in the local scope.

An adjective formed by combining the prefix **_non-_** ("not") and **_local_** ("pertaining to a particular place"). This is a primarily scientific and technical _neologism_ (literally "new word") that has no true general meaning, only specific meanings within specific fields. In programming it signifies a [non-local variable][nonlocal], meaning "[a NAME that is] accessible in neither the _local_ nor the _global_ namespace". In Python it very specifically applies to the namespace of the enclosing function from the point of view of a nested function, and is also a keyword that binds a _local_ NAME within that nested function into the **_nonlocal_** namespace, allowing it to be _writable_ from within the nested function.

  [nonlocal]: https://en.wikipedia.org/wiki/Non-local_variable "Read about non-local variables"
{{< /definition >}}

Because it is _only_ of use inside a nested function, usage will always involve some enclosing structure:

```python
def OUTER_FUNCTION():
    NAME = VALUE
    def INNER_FUNCTION():
        nonlocal NAME
        NAME = EXPRESSION
    INNER_FUNCTION()
```

The key thing to understand is that {{< definition-relref "nonlocal" >}} is used in a _similar_ fashion to {{< definition-relref "global" >}}, but with the more limited goal of making a variable in the parent of a nested function writable. It has similar caveats as well, though the fact that its impact isn't felt by the _entire_ program makes it inherently less dangerous. Still, its uses are _very_ narrow and _relatively_ few, so try not to abuse it when argument passing will do.

#### Kill it with fire

So far you've seen how to _add_ a NAME to a namespace, but how do you _remove_ a NAME from a namespace?

{{< definition doclink="https://docs.python.org/3/reference/simple_stmts.html#the-del-statement" >}}
del
: Used to delete a NAME (or NAMEs) from a namespace; if no other references exist to the OBJECT that NAME referred to, the underlying OBJECT is deleted as well.
: Can also be used to delete an attribute of an OBJECT or a member (or members) of a COLLECTION _if_ the specific type has allowed this operation.

A contraction of **_delete_**, which is in turn a verb derived from the Latin **_deletus_**. Its general meaning is to "destroy or eradicate", "erase or smudge out", and "utterly remove", and while the specific meaning in computing is a little less violent it has similar effect. In Python the meaning is a little indirect: **_del_** is used to delete a _reference_ that the _user_ directly controls, which _may_ indirectly trigger deletion of the thing referred to from process memory, which the _interpreter_ controls.
{{< /definition >}}

The most common usage is to provide a single NAME:

```python
del NAME
```

However it is also valid to provide multiple NAMEs, comma separated:

```python
del NAME_A, NAME_B, NAME_C
```

In either case Python will proceed left to right, deleting each NAME from the namespace in which the {{< definition-relref "del" >}} invocation has occurred.

Because the effect is limited to the _closest_ namespace, you have to use {{< definition-relref "global" >}} or {{< definition-relref "nonlocal" >}} to delete a NAME outside the local namespace:

```python
global NAME
del NAME
```

You can also use {{< definition-relref "del" >}} to delete attributes of OBJECTs and member(s) of COLLECTIONs, however what actually happens depends on the type of the OBJECT / COLLECTION involved. The **list** COLLECTION, for instance, allows you to use {{< definition-relref "del" >}} to delete both individual _indices_ and _slices_ of its contents:

```python
test = [1, 2, 3]
del test[0]         # deletes the first item
del test[:]         # deletes all items
```

We'll leave a further exploration of this for when we discuss the _builtin_ types in later articles. In the meantime, let's finally meet the keyword that will let you start defining such type-specific behaviors for yourself.

### One for Defining New Types of Object

Up until this point I've been pretty vague about what an OBJECT actually is. In the [Object-Oriented Programming][oop] paradigm, also known as OOP, an object is, basically, a _thing_ that has both _state_ (in the form of named _attributes_) and _behavior_ (in the form of callable _methods_). Two individual things of the same _type_ may have different specific values for those attributes -- we call them different _instances_ of the same _type_ -- but they share the same overall _interface_. However there's a bit more to it than that; the programmer should be able to define partial interfaces, which we'll call _traits_, that types with similar needs can implement in different ways, such that they all share some common attributes and behaviors (a property known as [_polymorphism_][polymorphism]). Additionally these traits should be able to be passed from more generic types to more specific types via an [inheritance][inheritance] mechanism, much as a parent passes on traits to their children.

  [oop]: https://en.wikipedia.org/wiki/Class_(computer_programming) "Read about classes in object-oriented-programming"
  [polymorphism]: https://en.wikipedia.org/wiki/Polymorphism_(computer_science) "Read about polymorphism"
  [inheritance]: https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming) "Read about inheritance"

You can take an example from nature; a duck is a type of bird, and it inherits certain traits it shares will all birds. All birds are a type of animal, and thus inherit certain traits shared will all animals. An animal is a type of life, and so on. Thus Howard, a specific duck, has all the attributes and behaviors of life, animals, birds, and ducks, all rolled up nicely in one instance of the duck type.

In fact it is from just such an example of biological _classification_ that Python takes the keyword it uses for defining new types of OBJECT.

{{< definition doclink="https://docs.python.org/3/reference/compound_stmts.html#class-definitions" >}}
class
: Used to define a template for a new type of OBJECT.

A noun borrowed via the French **_classe_** from the Latin **_classis_**, which meant "a division, army, fleet", "the people of Rome under arms", and, oddly specifically, "any one of the six orders into which Servius Tullius divided the Roman people for the purpose of taxation", which goes a long way towards explaining why English is such a difficult language to master. The general meaning we use here, though, is loosely borrowed from evolutionary taxonomy, implying "a group that shares certain inheritable traits". The specific meaning in Python comes from Object-Oriented Programming and implies "a template for creating objects that share common inheritable state (attributes) and behavior (methods)".
{{< /definition >}}

In Python you define a new type by creating a new NAME that is also a CALLABLE; from now on we'll call that a CLASS. The {{< definition-relref "class" >}} keyword is used to start a new BLOCK that defines the _implementation_ of that CLASS:

```python
class CLASS:
    pass
```

The CLASS can now be called to create a new instance of its type:

```python
NAME = CLASS()
```

Now from the above you might expect that instance to have _no_ attributes or behavior, but in fact it does have the _minimal_ interface that all OBJECTs share (it can be printed and used in comparisons, for instance, though not very usefully). It receives this because _all_ new {{< definition-relref "class" >}} definitions implicitly inherit from [**object**][object], which is Python's _base type_.

  [object]: https://docs.python.org/3/library/functions.html#object "Read about the object type"

You can also specify a more generic CLASS (also known as a _superclass_) to inherit from:

```python
class CLASS(SUPERCLASS):
    pass
```

In fact you'll often want to inherit from more than one superclass in order to mix together their various traits. This is done by separating the superclasses with commas:

```python
class CLASS(SUPERCLASS_A, SUPERCLASS_B):
    pass
```

The notion of [multiple inheritance][mro] can get quite complicated when more than one superclass defines the same attribute or method NAMEs, so for now let's just keep our classes simple and assume no such overlap.

  [mro]: https://docs.python.org/3.7/tutorial/classes.html#multiple-inheritance "Read about multiple inheritance in Python"

Just defining the CLASS and its superclasses without giving it some attributes and methods of its own is unusual, so you'll _normally_ see at minimum a custom _initializer_ method, which by convention is done by defining the special _double underscore_ (or "dunder") _instance method_ **\_\_init\_\_**:

```python
class CLASS:
    def __init__(self, NAME):
        self.NAME = NAME
```

As you can see an instance method is just another kind of function definition made using {{< definition-relref "def" >}}. In fact a METHOD is just a FUNCTION that's been added to the CLASS's namespace. That's right, the {{< definition-relref "class" >}} keyword also creates a new kind of local namespace, this one remains attached to the CLASS and allows names to be looked up on either the _instance_ or the class itself using the _dot access_ patterns INSTANCE.NAME and CLASS.NAME. Notice the **self** parameter name in the method definition above? That's the name given by convention to the _first_ parameter of any instance method, and it's how you access attributes set on the instance itself.

This all sounds a little abstract, so let's demonstrate it by building a CLASS for thinking about circles.

```python
from math import tau

class Circle:
    def __init__(self, radius):
        self.radius = radius

    def diameter(self):
        return self.radius * 2

    def circumference(self):
        return self.radius * tau

    def area(self):
        return tau * self.radius ** 2 / 2
```

Now if we create an instance representing the _unit circle_:

```python
unit = Circle(1)
```

We can access and [**print**][print] the **self.radius** attribute:

  [print]: https://docs.python.org/3/library/functions.html#print "Read about the print builtin function"

```python 
print(unit.radius)
```

And we can also call any of its methods, but notice how we never have to pass the radius of the circle as an argument, since the methods can all access that via **self**:

```python
print(unit.diameter())  
print(unit.circumference())
print(unit.area())
```

Since they're the fundamental building block of _everything_ in Python's [data model][model], there's a _lot_ than can be said [about classes in Python][classes], and there's a lot of subtleties that can go into their proper use (and improper abuse), so we'll come back to them often in later articles in this series. For now though the important thing is to start to recognize how {{< definition-relref "class" >}} is used to create them, and how instances are used when accessing their attributes and methods. It's also helpful to know that there are quite a few "dunder" methods, and that these are used to implement a lot of the common "under-the-hood" functionality that supports all the [builtin functions][builtins] we'll start to meet in later articles.

  [model]: https://docs.python.org/3/reference/datamodel.html "Read about Python's data model"
  [classes]: https://docs.python.org/3.7/tutorial/classes.html#classes "Read about classes in Python"
  [builtins]: https://docs.python.org/3/library/functions.html "Read about Python's builtin functions"

### One for Working Within a Context

Sometimes there are actions you _always_ want to perform within a specific context, such as committing a database transaction or closing a network connection. These sort of things _usually_ involve some form of _exception handling_ or other boilerplate specific to the task, and that can lead to a lot of boilerplate that needs to be repeated. An example is something as simple as reading a file: opening the file must necessarily mean getting some resources from the underlying operating system, and you always want to free up those resources, even if you accidentally tried to open a file that didn't exist or which you did not have permissions to read. The file is a _type_ of OBJECT that will always carry that contextual need to manage a resource with it, and so you'll need to write the same {{< definition-relref "try" >}} and {{< definition-relref "finally" >}} boilerplate _every_ time you open a file.

Unless the language you're working in provides a convenient means of ensuring that it happens for you.

{{< definition doclink="https://docs.python.org/3/reference/compound_stmts.html#the-with-statement" >}}
with
: Starts a [_context manager_][context-manager] BLOCK, which ensures that the indented STATEMENT(s) below it are performed within the context of the OBJECT being managed.
: Can also be marked with {{< definition-relref "async" >}}, to start an {{< definition-relref "async with" "async" >}}, see below.

  [context-manager]: https://docs.python.org/3/reference/datamodel.html#context-managers "Read about context managers in Python"

A Middle English preposition that takes its pronunciation from one Old English term, **_wið_** ("against"), but takes its modern meaning from another, **_mid_** ("in association with") which in turn comes from the German **_mit_**. The meaning in Python derives from **_within_**, meaning "inside the scope or context of [some thing or event]".
{{< /definition >}}

Any use of {{< definition-relref "with" >}} requires an EXPRESSION that evaluates to an OBJECT that satisfies the [context manager type][context-manager-type]'s interface, and thus has implemented both the **\_\_enter\_\_** and **\_\_exit\_\_** "dunder" methods. From now on we'll call that EXPRESSION a CONTEXT_MANAGER, to make the examples clearer.

  [context-manager-type]: https://docs.python.org/3/library/stdtypes.html#context-manager-types

In the most basic usage you simply start a new BLOCK:

```python
with CONTEXT_MANAGER:
    STATEMENT
```

Which will enter the context by calling `CONTEXT_MANAGER.__enter__()`, execute the STATEMENT within the context, and then exit the context by calling `CONTEXT_MANAGER.__exit__()`.


But most often you'll want to use {{< definition-relref "as" >}} to assign the OBJECT returned by `CONTEXT_MANAGER.__enter__()` to an alias NAME so the BLOCK can work with it:

```python
with CONTEXT_MANAGER as NAME:
    STATEMENT
```

This can save you a lot of boilerplate, especially with the many standard OBJECTs that already implement the context manager interface. For instance the recommended way to read a file's contents:

```python
with open(path) as src:
    contents = src.read()
```

Is _much_ simpler than what you'd otherwise have to write:

```python
src = open(path)
try:
    contents = src.read()
finally:
    src.close()
```

Occasionally you'll want to work within more than one CONTEXT_MANAGER:

```python
with CONTEXT_MANAGER_A as NAME_A, CONTEXT_MANAGER_B as NAME_B:
    STATEMENT
```

Which works exactly the same as nesting one {{< definition-relref "with" >}} inside another:

```python
with CONTEXT_MANAGER_A as NAME_A:
    with CONTEXT_MANAGER_B as NAME_B:
        STATEMENT
```

You'll get to meet quite a few context managers as you work your way through the Python standard library. And now you know that building your own is just a matter of creating a new {{< definition-relref "class" >}} and implementing a couple of "dunder" methods.

### And, Finally... Two for Working Asynchronously

Any function or method you write with {{< definition-relref "def" >}} alone is, by definition, _synchronous_, meaning that the moment you call it your running code has to stop everything else and _wait_, however long it takes, for your function to either {{< definition-relref "return" >}} or {{< definition-relref "yield" >}} control back to it before the rest of your code can be executed. For most tasks that happen on a local machine this is sensible and perfectly fine, especially when you _need_ the answer before you can proceed any further.

In much modern programming though it's often necessary to interact with things that _don't_ respond quickly, like network interactions with servers that could be a world away, and sometimes there's _plenty_ of work you could be doing while you wait for them to respond. You still _need_ the answer, but you need it _eventually_. One way this can be addressed is via [asynchronous programming][asynchrony], which as of Python 3.5 has become a first-class part of the Python language.

  [asynchrony]: https://en.wikipedia.org/wiki/Asynchrony_(computer_programming) "Read about asynchrony"

Asynchronous programming is an advanced topic that is fairly specialized, so using it is well outside the scope of this series. It's also quite a new addition to the language, and its usage has fluctuated from version to version. Rather than try to summarize those changed I'll just describe the very basics of using these keywords in Python 3.7 below. If, however, you're curious there's a quite good primer available [here][async-primer] that seems to be kept up to date.

  [async-primer]: https://realpython.com/async-io-python/ "Read a primer on asynchronous programming in Python"

Because asynchronous code does the same work as synchronous code, but _schedules_ the execution of that work differently, only two new keywords needed to be added to the language.

{{< definition doclink="https://docs.python.org/3/reference/compound_stmts.html#coroutine-function-definition" >}}
async
: Used to mark another KEYWORD as one that works asynchronously. As such, {{< definition-relref "async" >}} _cannot_ appear on its own.
: With {{< definition-relref "def" >}} as {{< definition-relref "async def" "async" >}} to define an asynchronous function, also known as a COROUTINE.
: With {{< definition-relref "for" >}} as {{< definition-relref "async for" "async" >}} to loop over an _asynchronous iterator_ inside an {{< definition-relref "async def" "async" >}}.
: With {{< definition-relref "with" >}} as {{< definition-relref "async with" "async" >}} to use an _asynchronous context manager_ inside an {{< definition-relref "async def" "async" >}}, see below.

As you may have guessed, this is a contraction of the Modern English word **_asynchronous_**, which is formed by combining the Latin roots **_a-_** ("not") and **_syn-_** ("together") with **_Khronus_**, the Ancient Greek personification of _time_. It unambiguously means "not occurring at the same time". In Python it more specifically marks an operation as "not occurring in the same time as the caller", which allows the caller to wait for the result of that operation, which will occur at _some_ point in the future.
{{< /definition >}}

Because the meaning of {{< definition-relref "async" >}} is tied to the KEYWORD it marks, its usage is always the same:

```python
async KEYWORD
```

However, unlike other any other keyword we've seen, the usage of {{< definition-relref "async" >}} will _always_ begin with the definition of a new COROUTINE:

```python
async def COROUTINE():
    STATEMENT
```

Both of the other forms of {{< definition-relref "async" >}} exist to allow you to work _within_ a COROUTINE with _other_ COROUTINEs, and thus they can only exist _inside_ an {{< definition-relref "async def" "async" >}}.

For instance you can use {{< definition-relref "async for" "async" >}} to loop over an [asynchronous iterator][async-iter] such as a GENERATOR COROUTINE (which is simply a COROUTINE that uses {{< definition-relref "yield" >}} instead of {{< definition-relref "return" >}}).

  [async-iter]: https://docs.python.org/3/reference/datamodel.html#asynchronous-iterators "Read about asynchronous iterators"

```python
async def COROUTINE():
    async for item in GENERATOR_COROUTINE:
        STATEMENT
```

You can also use {{< definition-relref "async with" "async" >}} to perform work within the context of an [asynchronous context manager][async-with]:

  [async-with]: https://docs.python.org/3/reference/datamodel.html#asynchronous-context-managers "Read about asynchronous context managers"

```python
async def COROUTINE():
    async with CONTEXT_MANAGER_COROUTINE as NAME:
        STATEMENT
```

Virtually every COROUTINE will need to wait on other COROUTINE(s), which is why there's another keyword that can only be used within an {{< definition-relref "async def" "async" >}}.

{{< definition doclink="https://docs.python.org/3/reference/expressions.html#await-expression" >}}
await
: Used to suspend the execution of the COROUTINE it is found _within_ and waits for the COROUTINE to its right to complete; can only be used inside an {{< definition-relref "async def" "async" >}}.

From the Middle English verb **_awaiten_** ("to wait for") from the Old French **_awaitier_**/**_agaitier_** ("to lie in wait for, watch, or observe"). The general sense is more active and hostile than **_wait_**, which it's a modification of. In asynchronous programming it means to "[suspend execution] and wait [for something to finish]".
{{< /definition >}}

The {{< definition-relref "await" >}} keyword is always going to be used to call a COROUTINE inside an {{< definition-relref "async def" "async" >}}:

```python
async def OUTER_COROUTINE():
    await COROUTINE()
```

Which will pause the execution of the outer COROUTINE and wait until the called COROUTINE, eventually, returns control. Any VALUE returned by the called COROUTINE is passed through {{< definition-relref "await" >}}, so you can think of `await COROUTINE()` as an asynchronous EXPRESSION that will, _eventually_ evaluate to whatever the COROUTINE returns when called.

Of course now that you've got the basics of doing asynchronous work down, how do you actually _perform_ such work? Well, as of Python 3.7 that still requires using functionality provided by the [asyncio][asyncio] module, the details of which are _well_ outside the scope of these articles. See the [primer][async-primer] I mentioned earlier for details.

  [asyncio]: https://docs.python.org/3/library/asyncio.html "Read about the asyncio module"

## Whew...

There you have them, Python's 35 keywords: in and of themselves not enough to make you fluent in Python, but if you've read this far and digested it you're well on your way to truly _understanding_ (and not merely _using_) the skeleton of _what is going on_ in one of the fastest growing general programming languages around. In the next post in this series we'll take a step away from _words_ and look instead at _symbols_, with a dive into Python's slightly smaller, but thankfully _much_ simpler, list of _operators_.
