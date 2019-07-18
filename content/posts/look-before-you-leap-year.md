+++
title = "Look Before You Leap Year"
date = "2019-06-12"
tags = ["exercism", "kata", "learning"]
categories = ["articles"]
series = []
slug = ""
summary = "Leap years are stupid. Actually, leap years are absurd, and consequently extremely stupid. From the day some long-dead forbear of astronomers and astrologers peered up at both the Sun and Moon in the same sky, put two and two together, and realized that they were in the same place as the last time it was this bloody cold, we’ve been stuck with them, whether we realized it or not. In a sad quest to pretend that an ellipse is, nevertheless, a circle, we doomed ourselves to forever having to maybe offset our mental clocks when looking sufficiently far forward or back in time, lest history and reality drift dangerously out of sync."
+++

## Leap Years are Stupid

Actually, [leap years][leap_years] are _absurd_, and consequently _extremely_ stupid. From the day some long-dead forbear of astronomers[^1] and astrologers[^2] peered up at both the Sun and Moon in the same sky, put two and two together, and realized that they were in the same place as the last time it was _this bloody cold_[^3], we've been _stuck_ with them, whether we realized it or not. In a sad quest to pretend that an _ellipse_[^4] is, nevertheless, a _circle_, we doomed ourselves to forever having to _maybe_ offset our mental clocks when looking sufficiently far forward or back in time, lest _history_ and _reality_ drift dangerously out of sync.

  [leap_years]: https://en.wikipedia.org/wiki/Leap_year "Visit the Wikipedia entry for Leap Year"

  [^1]: Those who look up at the night sky and find it full of _stuff_.
  [^2]: Those who look up at the night sky and find it full of _nonsense_.
  [^3]: They've never _actually_ occupied the same absolute positions twice, of course, and never will, but neither angular momentum or orbital mechanics were yet available to our prototypical _yutz_.
  [^4]: Actually something closer to an ellipse being frantically sketched over and over on an imaginary two dimensional plane being pulled away from the artist in four dimensional spacetime.

In the modern West the leap year is usually attributed to Julius Caesar, who so successfully promoted the concept that it _only_ took the Romans fifty years after his death[^5] to reliably incorporate it into what history now tries to forget as the Julian calendar. Unfortunately Caesar and his scholars -- being pretty poor programmers -- had made a _wee_ bit of a rounding error, and so in 1582 Pope Gregory XIII was forced to "correct" the situation[^6] by shifting the average year from 365.25 to 365.2425 days. And so was born the Gregorian calendar we all know and use today[^7]. This approximation was _good enough_ for the Church, and so history has been positively _littered_ with February 29th every so often ever since.

  [^5]: Caesar's assassination, which famously happened on March 15th, 44 BCE, rather threw off the adoption of leap years. Things got a bit wonky until 8 CE and, since no one in this period could be relied on to write anything down consistently, we know exactly when he died, just not when _in our calendar_.
  [^6]: Gregory XIII may have been liturgically infallible, but the fact that we've since had to introduce _leap seconds_ tends to imply he wasn't mathematically infallible as well.
  [^7]: Unless you use the Hindu, Islamic, or Buddhist calendars, are Thai or Chinese, subscribe to the Juche ideology of North Korea, or measure everything in Unix time.

I feel _contempt_ for the leap year. So why am I writing about it?

### It's an Ideal Programming Exercise

It turns out that determining if a particular Gregorian calendar year[^8] is, or is not, a leap year is a problem with some _unusual_ properties that make it an _excellent_ test of a programmer's mastery of some of the most fundamental tools they have available to them. That, in turn, means that it's not only a very good challenge for the budding programmer, but it could -- and I'd argue _should_ -- also be used as an impressively diagnostic question to ask a candidate in a technical interview.

  [^8]: Specifically, for the _truly_ pedantic, the _proleptic_ Gregorian calendar with _astronomical year numbering_ and a year zero. Which is _fine_ for the purposes of an exercise. To accurately reflect leap years actually _observed_ by humans you'd need at minimum a quite convoluted lookup table before the 9th century CE, and probably a time machine.

In every programming language that I've yet encountered there exists a short, simple, and performance-optimal solution for this problem. Indeed in most cases the optimum implementation is a single line long[^9], but most who attempt it will end up with something quite far from elegant on the first try. And, unlike most problems with such an ideal answer, if solved inelegantly it's also almost certainly solved inefficiently.

  [^9]: Your mileage may vary; in Perl it may even be less, but no one will know because of the braces. If you're writing in 8086 Assembly Language then, honestly, _why_ are you even reading this?

The beauty of the exercise is that the pathway to the ideal solution can easily be discovered just by employing the sort of straightforward reasoning that is the bread and butter of professional programming. It encourages you to _think_ through your solution by first _understanding_ what you're trying to solve.

#### Why does all this matter? 

<blockquote>
  <p>From the masochist to the sadist: "Hurt me."<br>From the sadist to the masochist: "No."</p>
  <cite>Clive Barker, for one</cite>
</blockquote>

Well maybe you've just joined [Exercism][exercism]. Or perhaps you're just looking for a good code kata. Or you've been assigned to a team working with calendars. Maybe you're simply a masochist. Or worse, perhaps your interviewer is a sadist.

  [exercism]: https://exercism.io "Visit Exercism"

One way or another, let's assume you've just been assigned the task of implementing a function `is_leap` that takes an _integer_ argument **year** and returns a _Boolean_ result.

### Luckily There's an Algorithm for That

<blockquote>
  <p>Every year that is exactly divisible by 4 is a leap year, except for years that are exactly divisible by 100, but these centurial years are leap years if they are exactly divisible by 400.</p>
  <cite>United States Naval Observatory</cite>
</blockquote>

Unusually for a programming problem the basic algorithm will most likely be presented to you up front, and you need merely implement it. The algorithm is very old, and has been stated in more or less precise ways over the centuries, so it helps to transcribe it into pseudocode:

```basic
IF the year is a multiple of 4 THEN
    IF the year is a multiple of 100 THEN
        IF the year is a multiple of 400 THEN
            RETURN True
        RETURN False
    RETURN True
RETURN False
```

Notice the chevron-like **>** shape that results from the multiple layers of nesting? It turns out that's fairly typical of a first-pass mental model of the algorithm, at least in a language where indentation is meaningful. It's not the most elegant form -- we'll get to that -- but it conveys some important properties about our algorithm:

1. **It's _simple_**. You have one argument, you perform (up to) three tests on it using a basic math operation, and it's the _same_ operation for all three tests. The most complicated thing you _need_ to know to solve it is _how_ your language performs the [modulo][modulo] operation. Once you've got that, comparison with zero, simple conditions, and how to return a Boolean-equivalent value in your language of choice you're _golden_. After five minutes of well-focused instruction a novice to _any_ high-level language should be able to bash out a general solution that mimics the above pseudocode.

  [modulo]: https://en.wikipedia.org/wiki/Modulo_operation "Wikipedia entry on the Modulo operation"

2. **It's _progressive_**. After each successive test you either know the answer or you know what to ask next. Most algorithms -- indeed most non-trivial problems -- aren't nearly so cut and dried. There is no need for complicated branching, or your language's version of `else_if`, you need merely proceed forward until the moment you are _certain_ you know the answer.

3. **It's _robust_**. There are no bugs, no weird or exceptional edge cases; every possible (integer) input maps directly to a single, unwavering output. Additionally there are no side effects, no state to mutate... you don't even need to carry forward the results of each modulo test. It's as _pure_ as a function can get, and so constrained that you can know from glancing at it if it will always return the correct answer.

### Know Thine Enemy and Thine Self

Understanding the algorithm is great, but understanding the problem it's addressing is _better_, and the insights gained above tell us nothing about the _domain_ we're working with. We've treated the various modulo tests as black boxes, but really they're specialized filters that apply to specific, progressively smaller, subsets of the overall domain of Gregorian years.

So what can we glean from looking a little more closely at those tests?

1. **The answer is _usually_ no**: From the very first test we know that 3 out of every 4 years _won't_ be a leap year. By looking at the rest we can see that an additional 3 out of every 4 _centuries_ won't be either... returning False by default will correctly answer >75% of all possible questions without any additional effort.
2. **They _rapidly_ cull the herd**: Just 1 in every 4 years is even a _potential_ leap year, just 1 year in every 100 is a century, and just 1 year in 400 is a century that's also a leap year... we learn a _lot_ fast about our year.
3. **They have a _natural_ order**: Each test is a special case of the previous one, and from the above we know that each applies to a progressively smaller number of cases. Sure, if we test division by 400 first we solve the problem very quickly in an _extremely_ small number of cases, but if it _doesn't_ give us the answer it also doesn't give us any useful knowledge about the question being asked. Proceed in the natural order, however, and each step refines the last.

Taking the first of these to heart we can rewrite our pseudocode so that we need only ever consider the paths to a True answer:

```basic
IF the year is a multiple of 4 THEN
    IF the year is NOT a multiple of 100 THEN
        RETURN True
    IF the year is a multiple of 400 THEN
        RETURN True
RETURN False
```

But this is interesting. Glancing at the above we can now see that there are _exactly_ two criteria that result in a year being a leap year, and that those criteria are exclusive. So for any given year the answer is True if _either_ of the following is True:

1. the year is a multiple of 4, but not of 100
2. the year is a multiple of 4, 100, and 400

### The Path of the Righteous

From either of the above the path to the ideal form can pretty neatly unroll in front of you. Especially if we introduce some abstraction and call our three tests **a**, **b**, and **c**.

For instance, if we progressively introduce _Boolean logic_ operations to our pseudocode:

```basic
IF a THEN
    IF NOT b OR c THEN
        RETURN True
RETURN False
```

... becomes...

```basic
IF a AND (IF NOT b OR c) THEN
    RETURN True
RETURN False
```

... which, in a language that allows you to return an expressions becomes:

```basic
RETURN a AND (NOT b OR c)
```

Oooh, that's pretty concise.

### Or We Could Go The Other Way

And if we'd started from the criteria we derived alone?

```basic
IF a AND NOT b THEN
    RETURN True
IF a AND b AND c THEN
    RETURN True
RETURN False
```

... can be combined with another Boolean logic operator as:

```basic
IF (a AND NOT b) OR (a AND b AND c) THEN
    RETURN True
RETURN False
```

... which allows us to extract the common operation:

```basic
IF a AND ((NOT b) OR (b AND c)) THEN
    RETURN True
RETURN False
```

... but there's no reason to perform the same Boolean test twice, so:

```basic
IF a AND (NOT b OR c) THEN
    RETURN True
RETURN False
```

... and since we're returning expressions brings us right back to:

```basic
RETURN a AND (NOT b OR c)
```

### All Roads Lead Here

And here lies the ultimate, optimal form. In a language that has _short-circuiting_ Boolean operations this is also the most performant form, because neither side of the `or` will be evaluated for the vast majority of cases. Thankfully most languages either do short-circuit Boolean operations, or they tend to provide an alternate short-circuiting operator like `and_also` and `or_else`, so if you're not sure yours does you'll need to do a bit of research.

Speaking of research, you _might_ be tempted to remove those parentheses, which certainly does look nicer. But therein lies the final lesson `is_leap` can teach you; your ability to elide those parentheses depends _entirely_ on the [evaluation strategy][evaluation] and [operator precedence][precedence] rules for your language. If your language evaluates left to right and binds `or` at the same or lower precedence as `and`, then no, you cannot remove those _significant_ parentheses. At least not without paying the price of checking division by 400 for a year that doesn't even divide by 4.

  [evaluation]: https://en.wikipedia.org/wiki/Evaluation_strategy "An overview of the topic of Evaluation Strategies"
  [precedence]: https://en.wikipedia.org/wiki/Order_of_operations "A brief explanation of Operator Precedence"

Which, like leap years, would be _stupid_.
