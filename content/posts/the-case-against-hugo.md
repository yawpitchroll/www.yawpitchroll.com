+++
title = "The Case Against Hugo"
date = "2019-05-26"
tags = ["hugo", "static site generator"]
categories = ["articles"]
series = []
slug = ""
draft = true
+++

## It's Quick Enough to Break Your Neck

As it says on the proverbial box, the [Hugo][hugo] static site generator is _fast_. Written in [Go][golang], Hugo promises _blistering_ speed that it certainly delivers, and I've got all the redness, pain, and burning discomfort needed to prove it.

  [hugo]: https://gohugo.io "The Hugo static site generator"
  [golang]: https://golang.org "Read about the Go programming language"

As I'm writing this -- in Markdown, using Vim -- all I have to do is save the file and the `hugo --server` process I've got running in the background will render to HTML and update my browser window by the time I can shift my eyes over to it. Hugo is _quick_, no question, and once you're up and running your site will do nothing but benefit from that speed, _especially_ when you've built up a significant catalogue of content.

### But...

<blockquote>
  <p>Prepare ship for Ludicrous Speed!</p>
  <cite>Colonel Sanders</cite>
</blockquote>

There's something to be said for the idea that _fast_ isn't necessarily _efficient_, and in the hands of the ill-prepared it's more often than not downright lethal. To get to the point where you could be reading this post I needed to do _vastly_ more than is implied by the [quickstart][quickstart] tutorial, and to do _that_ I had to learn vastly more than I'd originally been prepared for. For _months_ the only thing Hugo actually delivered to me at blistering speed was a blistering headache. To be fair that wasn't entirely Hugo's fault -- I made several false starts based on my aspirations more than my established needs -- but I let my desire for speed and some exciting marketing copy trip me up right out of the gate, so I spent most of those months on my face or worse.

  [quickstart]: https://gohugo.io/getting-started/quick-start/ "Read Hugo's Quick Start tutorial"

Frankly it's been an _agonizing_ journey. Pray you do not repeat it.

Read on, and perhaps you won't.

### A Bit of Background

I am a professional programmer, but I am **emphatically not** a professional _web_ programmer. Before deciding to build out [my personal site][home] as a home for my primarily technical musings I'd only ever blogged with WYSIWYG tools like Tumblr. For the last decade and then some I've written backend and process automation code for the Visual Effects industry, and while that is certainly a world orientated around visual aesthetics, in truth I've got the UX/UI design chops of your average wild-born gibbon. The last _serious_ experience I had with HTML/CSS predated the Marvel Cinematic Universe, and let's just say there have been some developments since then.

  [home]: https://www.yawpitchroll.com "Visit my homepage"

I wasn't naive, I knew there would a learning curve, I just wanted it to be slightly under the slope of picking up Dwarf Fortress.

And, after a fair amount of pre-Hugo research, I'd narrowed down exactly what I _thought_ I wanted, my Minimum Viable Website:

* A static site I could host on a free CDN-backed service like Github Pages or Netlify
* A responsive, mobile-first theme with syntax highlighting and readable typography
* Modern markup practices; JSON-LD Structured Data, OpenGraph, and semantic HTML5
* Reasonable privacy practices by default; at least a good-faith effort at GPDR compliance
* Easy social sharing to Facebook, LinkedIn, and Twitter, but _without_ unnecessary tracking
* Comments on posts, so I can hear from the readers I sincerely _hope_ will arrive
* Minimal ability to sign up for a mailing list; a lot of people left RSS after Google Reader died
* Very, very fast load time; I've been bitten by Tumblr, and Google's AMP pages _seemed_ ideal
* A decent nod to accessibility; I'm getting older and I've got friends that are visually impaired

Now, those nine criteria might seem like a lot -- and, in hindsight, maybe they were -- but really they can be boiled down to **deliverable**, **discoverable**, and **readable**, and since my visual needs are _pretty_ bare-bones they didn't seem like too much of an ask.

Of course I'd quicky learn that some had natural conflicts; AMP especially puts quite a bit of pressure on comments and mailing list signup, for instance, and social sharing and privacy don't exactly go hand in hand, but I had _hope_. More than that, I had Hugo.

Now, I hadn't gone in full bore without reading up on the competition; I'm much more comfortable with Python than I am with Go, so I'd considered [Pelican][pelican], [Nikola][nikola], and [Hyde][hyde][^1], but at the end of the day none of those projects seemed very deep, and how often was I going to need -- or want -- to monkey around with the _generator's_ internals, anyway? Plus, at the end of the day, my itch for speed stems from too many years waiting on Python, so the siren song of fast lured me on.

  [pelican]: https://blog.getpelican.com/ "The Pelican static site generator"
  [nikola]: https://getnikola.com/ "The Nikola static site generator"
  [hyde]: https://hyde.github.io/ "The Hyde static site generator"

  [^1]: Hyde's own site looking different when served over http vs https didn't inspire confidence.

Of course I also checked out [Jekyll][jekyll], the Ruby-written, Github Pages first class member; an extremely solid alternative that's polished enough to be on its third major version, with a community large enough to demand some level of stability. But I'm not _at all_ familiar with Ruby, so lingering fear of having to get under the hood at least once, coupled with the -- by all accounts quite obvious -- speed differential tipped the balance towards Hugo. Besides, Jeykll _felt_ long in the tooth, with _loads_ of long unaddressed issues and themes showcases bloated by what certainly looked to me like a large amount of swine and only a few pearls. Even its own website seemed dated and rather dull.

  [jekyll]: https://jekyllrb.com/ "The Jekyll static site generator"

By contrast there was an obvious, churning buzz around Hugo among tech bloggers I admire, a solid amount of recent commit history, and some definitely cool sounding features like [Hugo Pipes][pipes]. As a neophyte to static, self-managed  blogging I really hoped for something that might save me from the confusing tide of tooling that seems to inundate the world of web development -- I'm staring balefully at you `npm`, `grunt`, `yarn`, `webpack`, `yack` and `pork`, the last two of which I'm not even _sure_ I just made up -- so Pipes looked like a big shiny win. And, glancing through the [theme browser][themes], there were a high proportion of options that looked good -- if not _ideal_ -- for the minimalist tech blog I was _obviously_ going to _finally_ have up and running **any day now**. Sure, I might need to figure out how to transplant some elements, Frankenstein-like, from one theme into another, but the templating syntax looked simple enough, there seemed to be a lot of [documentation][docs], and there were obviously active [forums][discourse] with lots of meat to chew through.

  [pipes]: https://gohugo.io/hugo-pipes/introduction "Check out Hugo Pipes"
  [themes]: https://themes.gohugo.io "Visit Hugo's themes showcase"
  [docs]: https://gohugo.io/documentation/ "Hugo's documentation"
  [discourse]: https://discourse.gohugo.io/ "Hugo's forums"

So, after some more comparison on drearier topics like CI deployment and hosting options, decision made, Hugo for the win! I'm a greenfield blogger, no big -- or for that matter _any_ -- back catalogue to worry about importing, all I've got to do is pick a theme, start writing my first post, and deploy!

What could go wrong?

#### It Doesn't Exactly Work Out of the Box

<blockquote>
  <p>You never get a second chance to make a first impression.</p>
  <cite>Head & Shoulders</cite>
</blockquote>

Maybe it was bad luck, maybe it was the winds of change, most likely it was an errant commit on the Ananke theme -- who knows? -- but on the fateful day I first did the [quickstart][quickstart] I rapidly and tenaciously made it all the way to item 5, breathlessly ran `hugo server -D` and then, aching with anticipation, opened a browser window and pointed it at the localhost address conventiently displayed to find absolutely _bupkiss_ being served. Nada. A blank screen with an empty source. Back in the terminal where I'd launched the command there were several warnings, but nothing that could obviously explain the error.[^2]

  [^2]: As of the day I'm writing this running through the quickstart instructions does in fact work, though with a great many deprecation warnings and you end up with a site that looks nothing like the theme demo page, even the gargoylish top splash image doesn't load. 

This was _disappointing_, but at the end of the day I had zero interest in Ananke, so I decided to try the rest of the quickstart with one of the more appropriate themes I'd chosen.

... it didn't work. Neither did the next. And neither did the following three.

Hugo is an open source project; as of right now its highest release is 0.55. Unlike Jekyll it hasn't yet reached a 1.0 release, and thus has made no promises about backwards compatability. And that's fine. Each of the themes is similarly an open source effort, typically -- though not always -- with a single developer that is very possibly the sole invested consumer as well. And so things have broken, badly. Which maybe is to be expected, in a project so immature, but for each and every one of these themes the hosted _demo_ works fine. So what gives? Well it turns out it's because the hosted showcase uses the `exampleSite` directory embedded in each submitted theme, something not even mentioned in the quickstart, and _very_ often the templates in the theme depend on configuration that simply won't be present in your quickstart site.

Eventually, after _much_ reading of old forum posts and tripping through a lot of documentation well past it's best before date, I discovered the following _usually_ gives you a local theme demonstration that behaves roughly as the author intended:

```bash
mv config.toml config.toml.bak
cp -r themes/YOUR_THEME/exampleSite/* .
find . -maxdepth 1 -type f \( -name "config.toml" -or -name "config.yaml" -or -name "config.json" \) -print -quit | grep -q "." || cp config.toml.bak config.toml
cp themes/YOUR_THEME/archetypes/*.* ./archetypes/
```

The first line backs up the default `config.toml` file before the contents of the theme's `exampleSite` directory are copied into the root. We need to move `config.toml` because that file, if present, will take precedence over `config.yaml`, which will in turn take precedence over `config.json`. That's right, Hugo has had **three** configuration file formats over its short life, and all three remain viable options, though for some reason TOML has the edge. Since _any_ of them may have been present in the theme, we'll only move the backup back into place if _none_ of them were.

Similarly the final line  overwrites the `archetypes/default.md` file with any and all files in the theme's `archetypes` directory; this is because Hugo will _always_ assume that a `default.md` in the root `archetypes` directory should override _any_ archetype from the theme, no matter how specialized it may be.

As I said that will _usually_ give you a working example of the theme you've chosen, though for instance Ananke itself will need a further step:

```bash
sed -i 's/gohugo-theme-ananke/ananke/' config.toml
sed -i 's/^themesDir/#themesDir/' config.toml
```

Which are required because the quickstart instructions had you rename the theme itself as you made the submodule, and the **themesDir** was set apparently as a hack to make the theme easier to test.

These sorts of issues mostly derive from the various themes having been written at various stages in Hugo's _rapid_ evolution, and many of them have committed to old choices that no longer remain the best practice, or are now pending deprecation[^3]. One phylogentic tree of themes _requires_ content to be in `content/post` instead of `content/posts`, another will fall down if it's not the other way around.

  [^3]: Hence the warnings you'll see in the quickstart with Ananke, even with the fixes describe above.

These are, of course, relatively minor issues; take a dew days, pore over the forums and the documentation, make a few key configuration changes and possibly clear out a few of the cobwebs in a partial or two, and you're good, right?

#### Failure is a Recursing Theme

If I've learned anything recently it's that themes for static blogs tend to be fairly and surprisingly complex beasts. As a rule you should assume, going in, that whoever wrote the theme you've chosen only understood -- or at least only encountered -- a fraction of the potential issues. As just one example of an issue repeatedly encountered, a small and seemingly innocuous change to a configuration value can suddenly turn Hugo's impressive speed into an equally impressive amount of thumb twiddling, right up until the server times out and spits out a complaint about excess recursion. Unfortunately this is one of a family of errors that leaves you with no clear idea where the problem child might be, or even what file was being processed.

My encounters with these recursion issues weren't extremely common, but frustrating enough that I tried to figure out what was going on; they _seem_ to be related to the usage of the [Scratch][scratch] area, a sort of variously site / page / template localized "scratchpad" that the Hugo team bolted on to overcome an apparent deficiency in the Go template language.[^4]. The Scratch facility seems to have been added to attend to a narrow problem, but it was apparently adopted enthusiastically -- and perhaps too widely and, at times, inappropriately -- by theme authors. Unfortunately they've done that off of sparse documentation on what is an obviously powerful, but seemingly dangerous, feature, and more importantly a feature you, the theme _consumer_ can't know is in use without knowing your theme's various templates both _deeply_ and _intimately_.

  [scratch]: https://gohugo.io/functions/scratch/ "Read about Hugo's .Scratch"

  [^4]: Variables could be assigned in templates with the `:=` assignment operator, but not updated. This appears to have been quietly fixed at some point (there is now a `=` update operator), reducing the need for the Scratch, at least _within_ a single template's scope.

<blockquote>
  <p>This isn't life in the fast lane, it's life in the oncoming traffic.</p>
  <cite>Terry Pratchett</cite>
</blockquote>

Debugging these sort of issue is _hard_. And, beyond Scratch, the Go templating language is _impressively_ flexible and powerful, allowing you to embed significantly more complex logic into templates than I've seen in other such template DSLs, but this brings with it a consequent increase in the complexity and number of possible errors. Since there's -- as of yet -- no meaningful or obvious way to test a template, you can imagine that the reliability of the various themes in the showcase is _extremely_ variable.

The end result is that the promise of getting up and running fast with a theme is a fairly hollow one; even if you don't end up rewriting every line of your chosen theme -- and, as you'll see below, there's a good chance you will _want_ to -- you're going to spend a signfiicant amount of time looking and installing and testing, and ultimately you'll be required to understand what is happening internally to a degree that simply doesn't appear to be true with other more mature, stable, and well documented projects.

Here's the thing though... that may be a feature, not a bug, and though I may not sound like it right now, I'm an optimist.

#### The Problem of Laws & Sausages

None of the above is to say that there aren't themes out there that work, and work well. I got nowhere near testing them all, and it's entirely possible I just chose poorly, and your mileage may vary. If your need is is a single page landing site or a product launch page there are slick looking, seemingly professional offerings that may work out of the box, but those simply didn't fill my needs. Further, many of the themes in the showcase were filtered out for purely aesthetic reasons, while others were eliminated because of my early desire for an [AMP][amp]-compatible theme.

  [amp]: https://amp.dev/ "Learn about Accelerated Mobile Pages"

That last point plays into what came next surprisingly heavily, and it may seem like a specialist concern, but I assure you it isn't. My interest in AMP wasn't born out of a desire to get to the top of Google's featured posts -- what techie blog could do that? -- but it was about _speed_, which after all is what drove me into the arms of Hugo.

I want my work read, and Google -- and my own experience as a reader -- have made a compelling case that the quicker a page loads the more chance it has of getting read far enough to garner attention. Now a static site should, in theory, load pretty quick, but firing up the Firefox Web Developer Tools that I was only just beginning to understand I found that the few themes I'd narrowed down to were positively dripping with dependencies on heavy-weight, externally hosted CSS and Javascript, and it was significantly effecting load and render times. More then that it wasn't going to be compatible with AMP, which puts a filse size restriction on CSS and only allows a small, curated set of JS widgets. I needed to filter out any theme that relied on any of this for basic looks and functionality, and a surprising number of the remaining options -- which had already been chosen for their stark, text-first minimalism  -- were tossing themselves out of the boat.

These were, of course, my own constraints, arrived at independently, and I can't and don't fault Hugo or the theme authors for not meeting them. But they're also not unreasonable or particularly unusual constraints, and what I'd just spent the better part of a month doing was whittling time away by first struggling to get a candidate minimally working with some closer-to-real-world content, followed by diving in and trying to identify areas of concern.

I'll leave why I ended up setting AMP aside for another time, but by that time it had driven me to start looking under the hood of the themes I found even more than the issues I've already described. I started to actually _read_ all the templates, more than just skim them looking for specific lines mentioned in occasional errors.

What I found was that I often _couldn't_ understand them. The expressive power of Hugo's templates and partials means that it's often like trying to unscramble an omelette or re-muscle a sausage. Everything no doubt makes sense to someone intimately familiar with it, but to the uninitiated, at least in the short run, it's just a muddle, with no real recurring structural patterns. The language itself is simple enough, 

#### When You Want it Done Wrong


