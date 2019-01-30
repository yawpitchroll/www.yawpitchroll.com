---
title: Basic Hugo Markdown Elements
description: Demonstrated Hugo-suppoorted Markdown elements for text formatting.
date: 2019-01-22
draft: false
categories:
- Development
tags:
- HTML
- CSS
- Basic Elements
series: null
---

# PURPOSE

Collects together all the Markdown-syntax supported by Hugo's default Blackfriday renderer; this
is intended to be a test-bed for themes.

# Syncope

Syncope is a WYSIWYG tool that helps web designers and developers chose the optimal vertical rhythm of the typography for their web pages.

Basically, it's a set of tools which adjust the rhythm and output the styles in a preferred, production–friendly format. It is also a lot of fun to play with! In fact, if it weren't for that, this tool wouldn't have seen the light of day.

## Rhythm matters

Vertical rhythm is a typographic concept in which lines of text are evenly spaced, i.e. regardless of font size or variant, each line must be precisely aligned to the grid of the rhythm. Just like the text you're reading at this moment.

When visually organized in such way, the text is usually easier to read and simply looks better as a part of the web page ecosystem. Long story short, it is something that every website should implement to provide the best reading experience. 



## LINE LENGTH GUIDE

Use the below for judging line length; 2-3 alphabets should be about right.

<span hyphens: none>
abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz  </span>

## PARAGRAPHS, LINE BREAKS, AND SPANS

A paragraph is simply one or more consecutive lines of text, seperated by or or more blank lines. (A blank line is any line that looks like a blank line -- a line containing nothing bug spaces or tabs is considered blank.) Normal paragraphs should not be indented with spaces or tabs.

Paragraphs in Markdown are _hard-wrapped_, which means that to insert a `<br/>` you'll need to end a line with two or more space, _then_ hit return:  
For instance this line should follow a `<br>`.

While this line starts a new paragraph. This can be particularly problematic if your text editor is set to remove trailing whitespace.

Single surrounding *asterixes* result in an `<em>` tag, as do single _underscores_. Double surrounding **asterixes** result in a `<strong>` tag, as do double __underscores__. Surrounding `backticks` will produce an inline `<code>` tag. With two tildes on either side you get ~~strikethrough~~.

An `<hr>` can be created with three or more hyphens, asterixes, or underscores on a line by themselves:

***

Most links like http://example.com will be automatically linked, but it's generally better to be explicit.

This is [an example](http://example.com/ "Title") of an inline link with title, while [this](http://example.net/) has no title attribute.

An inline link can be relative to other [local pages](/page/about/). 

Links can also [be defined][explicit] using named references, including the [implicit][] reference.

   [explicit]: http://example.com  "Explicit Example"
   [implicit]: http://example.com  "Implicit Example"

Just _make sure_ you don't indent them sufficiently to force a `<code>` tag.

***

## HEADINGS

Markdown supports two formats for the HTML `<h1>` - `<h6>` elements; the most common form is _atx_-style:

# Heading 1 
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

You can also close the header, if you prefer, with trailing `#` characters; the number is irrelevant.

### Heading 3 ###
#### Heading 4 ####

The second supported format is _setext_-style "underlined", though only `<h1>` and `<h2>` work:

Heading 1
=========

Heading 2
---------

Headers will usually be presented with intervening text:

# Section

I'm just a poor boy and nobody loves me.

## Subsection

He's just a poor boy, from a poor family.

### Sub-Subsection

Spare him his life from this monstrosity.

#### Sub-Sub-Subsection

Easy come easy go will you let me go.

##### Sub-Sub-Sub-Subsection

Bismillah, no we will not let you go, let him go!

###### Sub-Sub-Sub-Sub-Subsection

Oh mama mia, mama mia, mama mia let me go...

***

## BLOCKQUOTES

Markdown allows blockquotes to be hard-wrapped with a `>` before every line:

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
> 
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.

Markdown allows you to be lazy and only put the `>` before the first line of a hard-wrapped paragraph:

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.

Blockquotes can be nested (i.e. a blockquote-in-a-blockquote) by adding additional levels of `>`:

> This is the first level of quoting.
>
> > This is nested blockquote.
> >
> > > This is a deeply-nested blockquote
>
> Back to the first level.

Blockquotes can contain other Markdown elements, including headers, lists, and code blocks:

> ## This is a header.
> 
> 1.   This is the first list item.
> 2.   This is the second list item.
> 
> Here's some example code:
> 
>     return shell_exec("echo $input | $markdown_script");

***

## LISTS

Markdown supports ordered (numbered) and unordered (bulleted) lists.

Unordered lists can use created using a preceding asterix, plus, or dash.

*   Red
*   Green
*   Blue

Ordered lists use numbers followed by periods, however the actual number value is irrelevant to the output code:

1.  Bird
1.  McHale
1.  Parish

Lists can be arbitrarily nested:

1. First Parent
    1. First Child
    2. Second Child
    3. Third Child
        1. First Grandchild
        2. Second Grandchild
            * First Toy
            * Second Toy
2. Second Parent

To make lists look nice, you can wrap items with hanging indents:

*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.

But if you want to be lazy, you don’t have to:

*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
Suspendisse id sem consectetuer libero luctus adipiscing.

List items may consist of multiple paragraphs. Each subsequent paragraph in a list item must be intended by either 4 spaces or one tab:

1.  This is a list item with two paragraphs. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.

    Vestibulum enim wisi, viverra nec, fringilla in, laoreet
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

2.  Suspendisse id sem consectetuer libero luctus adipiscing.

It looks nice if you indent every line of the subsequent paragraphs, but here again, Markdown will allow you to be lazy:

*   This is a list item with two paragraphs.

    This is the second paragraph in the list item. You're
only required to indent the first line. Lorem ipsum dolor
sit amet, consectetuer adipiscing elit.

*   Another item in the same list.

To put a blockquote within a list item, the blockquote’s `>` delimiters need to be indented:

*   A list item with a blockquote:

    > This is a blockquote
    > inside a list item.

To put a code block within a list item, the code block needs to be indented twice – 8 spaces or two tabs:

*   A list item with a code block:

        <code goes here>

***

## CODE BLOCKS

The simplest way to include a code block is to indent every line by 4 spaces or a tab:

    # here is a comment that's 50 characters wide.
    for i in range(1, 21):
        print(i)

Though for some stupid reason it seems to be guessing:

    if there's a code block
    as opposed to just a pre.

However _if_ Hugo has been configured with `pygmentsCodeFences` then Github-style triple-tilde fences work as well, which also allows hinting for language syntax highlighting.

```python
#! /usr/bin/env python
"""
Module level docstring: for the purpose of deciding on sizing we will take this
to exactly 80 characters before breaking.
"""
from enum import Flag, auto
import re

THING = None
PATT = re.compile(r"(\d+)(\.\d+)", re.ASCII)

class Allergens(Flag):
    """
    Bit flags representing specific allergens.
    """
    EGGS = auto()  # end of line comment
    PEANUTS = auto()
    SHELLFISH = auto()

@portos(thing="2")
def main(b: int) -> None:
    for a in Allergens:
        print(PATT.match(a.name))

if __name__ == "__main__":
    main()
```

```python
Traceback (most recent call last):
  File "lib/discord/ext/commands/core.py", line 50, in wrapped
    ret = yield from coro(*args, **kwargs)
  File "/home/bill/stimzo-bots/ned/cogs/errorlogs.py", line 47, in _raise
    raise Exception()
Exception

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "lib/discord/ext/commands/bot.py", line 846, in process_commands
    yield from command.invoke(ctx)
  File "lib/discord/ext/commands/core.py", line 374, in invoke
    yield from injected(*ctx.args, **ctx.kwargs)
  File "lib/discord/ext/commands/core.py", line 54, in wrapped
    raise CommandInvokeError(e) from e
discord.ext.commands.errors.CommandInvokeError: Command raised an exception: Exception: 
```

```c
#pragma pack(push, 1)
struct PackedStructure
{
  char a;
  int b;
  short c;
};
#pragma pack(pop)
// sizeof(PackedStructure) == 7
```

```html
<!DOCTYPE html>
<html lang="en">
</html>
```

Additionally Hugo's own `\{\{< highlight >\}\}` templating can be used when specific line numbers or a highlighting are required:

{{< highlight html "linenos=table,hl_lines=8 15-17,linenostart=199" >}}
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Example HTML5 Document</title>
</head>
<body>
  <p>Test</p>
</body>
</html>
{{< /highlight >}}

```go
/*
This block demonstrates a mult-line comment.
It needs to be several lines long.
*/

package main

import (
    "fmt"
    "math/rand"
    "time"
)

type Moo struct {
    Cow   int
    Sound string
    Tube  chan bool
}

// A cow will moo until it is being milked
func cow(num int, mootube chan Moo) {
    tube := make(chan bool)
    for {
        select {
        case mootube <- Moo{num, "moo", tube}:
            fmt.Println("Cow number", num, "mooed through the mootube")
            <-tube
            fmt.Println("Cow number", num, "is being milked and stops mooing")
            mootube <- Moo{num, "mooh", nil}
            fmt.Println("Cow number", num, "moos one last time in relief")
            return
        default:
            fmt.Println("Cow number", num, "mooed through the mootube and was ignored")
            time.Sleep(time.Duration(rand.Int31n(1000)) * time.Millisecond)
        }
    }
}

// The farmer wants to turn on all the milktubes to stop the mooing
func farmer(numcows int, mootube chan Moo, farmertube chan string) {
    fmt.Println("Farmer starts listening to the mootube")
    for unrelievedCows := numcows; unrelievedCows > 0; {
        moo := <-mootube
        if moo.Sound == "mooh" {
            fmt.Println("Farmer heard a moo of relief from cow number", moo.Cow)
            unrelievedCows--
        } else {
            fmt.Println("Farmer heard a", moo.Sound, "from cow number", moo.Cow)
            time.Sleep(2e9)
            fmt.Println("Farmer starts the milking machine on cow number", moo.Cow)
            moo.Tube <- true
        }
    }
    fmt.Println("Farmer doesn't hear a single moo anymore. All done!")
    farmertube <- "yey!"
}

// The farm starts out with mooing cows that wants to be milked
func runFarm(numcows int) {
    farmertube := make(chan string)
    mootube := make(chan Moo)
    for cownum := 0; cownum < numcows; cownum++ {
        go cow(cownum, mootube)
    }
    go farmer(numcows, mootube, farmertube)
    farmerSaid := <-farmertube
    if farmerSaid == "yey!" {
        fmt.Println("All cows are happy.")
    }
}

func main() {
    runFarm(4)
    fmt.Println("done")
}
```

```diff
--- file1	2015-12-20 03:31:11.633716816 -0500
+++ file2	2015-12-20 03:31:46.233727391 -0500
@@ -1,2 +1,2 @@
-This is  a test file.
+This is the second test file
 We are calculating the diff
```

***

## BLACKFRIDAY EXTENSIONS

Hugo's Blackfriday renderer adds several extensions; the following should all be enabled by default.

### Tables

| ID  | Make      | Model   | Year |
| --- | --------- | ------- | ---- |
| 1   | Honda     | Accord  | 2009 |
| 2   | Toyota    | Camry   | 2012 |
| 3   | Hyundai   | Elantra | 2010 |
| 4   | Dodge     | Ram     | 2008 |
| 5   | Ford      | POS     | 1982 |

Colons can be used to align columns:

| Column should align left | Column should align center | Column should align right |
|:----------- |:-------------:| ------------:|
| align: left | align: center | align: right |
| align: left | align: center | align: right |
| align: left | align: center | align: right |

You can also use inline Markdown within a table:

| Inline     | Markdown  | In                | Table      |
| ---------- | --------- | ----------------- | ---------- |
| *italics*  | **bold**  | ~~strikethrough~~ | `code`     |

Oversized tables may break mobile layouts, which is why Ample provides the "table" shortcode:

{{% table %}}
| Column should align left | Column should align center | Column should align right |
|:----------- |:-------------:| ------------:|
| align: left | align: center | align: right |
| align: left | align: center | align: right |
| align: left | align: center | align: right |
{{% /table %}}

### Footnotes:

This is a footnote[^1], which should link to the bottom of the page.

   [^1]: this is the footnote text.


### Back slashes break lines.

Trailing backslashes \\
Will become `</br>` tags.

### Definition Lists

Inline definition lists are supported:

Cat
: Fluggy animal everyone likes

Internet
: Vector of transmission for pictures of cats
: The clacks... re-send GNU Terry Pratchett

Extra Añejo Tequila
: A new classification added in the summer of 2006, labeling any Tequila aged more than 3 years, an "Extra Añejo". Following the same rule as an "Añejo", the distillers must age the spirit in barrels or containers with a maximum capacity of 600 liters. With this extended amount of aging, the Tequila becomes much darker, more of a Mahogany color, and is so rich that it becomes difficult to distinguish it from other quality aged spirits. After the aging process, the alcohol content must be diluted by adding distilled water. These Extra Añejo’s are extremely smooth and complex.

Terms must be separated from the previous definition by a blank line.

### Task Lists

Github-style task (TODO) lists are supported, unless disabled:

- [ ] a task list item
- [ ] list syntax required
- [ ] incomplete
- [x] completed

### Emoji

If `enableEmoji` is True, you should see an inline :thumbsup:, which will bring :dollar: if you ever get the patent :registered: registered.

***

## SPECIALIZED HTML

The following are not supported by Markdown, but work fine as inline HTML.

### Blockquotes with citation

The blockquote element can be a citation which must be within a `footer` or `cite` element, and optionally with in-line changes such as annotations and abbreviations.

<blockquote>
  <p>My goal wasn't to make a ton of money. It was to build good computers. I only started the company when I realized I could be an engineer forever.</p>
  <cite>Steve Wozniak</cite>
</blockquote>

### Inline quotes

According to Mozilla's website, <q cite="https://www.mozilla.org/en-US/about/history/details/">Firefox 1.0 was released in 2004 and <q>became a big success</q>.</q>

## Other stuff — abbr, sub, sup, kbd, etc.

<abbr title="Graphics Interchange Format">GIF</abbr> is a bitmap image format.

H<sub>2</sub>O

C<sub>6</sub>H<sub>12</sub>O<sub>6</sub>

X<sup>n</sup> + Y<sup>n</sup> = Z<sup>n</sup>

Press <kbd>X</kbd> to win. Or press <kbd><kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>F</kbd></kbd> to show FPS counter.

<mark>As a unit of information in information theory, the bit has alternatively been called a shannon</mark>, named after Claude Shannon, the founder of field of information theory.

