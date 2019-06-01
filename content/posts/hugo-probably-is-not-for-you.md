+++
title = "Hugo Probably Isn't For You"
date = "2019-06-01"
tags = ["hugo", "web"]
categories = ["articles"]
series = []
slug = "Hugo Probably Is Not For You"
draft = true
+++

## Yes, It's Quick Enough to Break Your Neck

As it says on the proverbial box, the [Hugo][hugo] static site generator is _fast_. Written in [Go][golang], Hugo promises _blistering_ speed that it certainly delivers, and I've got all the redness, pain, and burning discomfort needed to prove it.

  [hugo]: https://gohugo.io "The Hugo static site generator"
  [golang]: https://golang.org "Read about the Go programming language"

As I'm writing this -- in Markdown, using Vim -- all I have to do is save the file and the `hugo --server` process I've left running in the background will render to HTML and update my browser window by the time I can shift my eyes over to it. Near instant feedback, even if I've made significant changes to multiple posts. Hugo is _quick_, no question, and _once you're up and running_ your site will do nothing but benefit from that speed, _especially_ when you've built up a significant catalogue of content.

### But...

<blockquote>
  <p>Prepare ship for Ludicrous Speed!</p>
  <cite>Colonel Sanders</cite>
</blockquote>

There's something to be said for the idea that _fast_ isn't necessarily _efficient_, and in the hands of the ill-prepared it's more often than not downright lethal. To get to the point where you could be reading this post I needed to do _vastly_ more than is implied by the [quickstart][quickstart] tutorial, and to even do _that_ I had to learn vastly more than I'd originally been prepared for. For _months_ the only thing Hugo actually delivered to me at blistering speed was a blistering headache. To be fair that wasn't entirely Hugo's fault -- I made several false starts based on my aspirations more than my established needs -- but I let my desire for speed and some exciting marketing copy trip me up right out of the gate. Which means I spent most of those months on my face, or often worse. All Hugo really did to help me during that time was _fail_ blisteringly fast; it _often_ did things that hindered me.

  [quickstart]: https://gohugo.io/getting-started/quick-start/ "Read Hugo's Quick Start tutorial"

Frankly it's been an _agonizing_ journey. Pray you do not repeat it. Read on, and perhaps you won't.

### A Bit of Background

I am an experienced programmer, but I am **emphatically not** a _web_ programmer. Before finally deciding to build out [my personal site][home] as a home for my technical musings I'd only ever blogged with WYSIWYG tools like Tumblr, and then only sporadically. Professionally I mainly write backend and process automation code for the Visual Effects industry, so it's charitable to say that I've developed the UX/UI design chops of your average wild-born gibbon. The last _serious_ experience I had with HTML/CSS predated the Marvel Cinematic Universe, and let's just say there have been some plot developments since then.

  [home]: https://www.yawpitchroll.com "Visit my homepage"

So I don't have a lot of experience in web development, but I'm also not seeking to gain that experience. I've also got no large back catalogue of existing content that I need to port over, so I'm basically a greenfield blogger who wants to get up and running relatively quickly. I just need to make a choice about _how_ I'm going to do that.

I wasn't naive about that choice; I knew that any choice I made would involve a learning curve, I just wanted it to be slightly under the slope of, say, picking up [Dwarf Fortress][curve], so I tried to approach the choice of tooling critically.

  [curve]: http://i.imgur.com/4AzYP.jpg "The Learning Curve of Popular Games"

#### Step 1: Establish Key Criteria

After a fair amount of offline research I'd eventually narrowed down exactly what I _thought_ I wanted out of my Minimum Viable Website:

* A static site I can host on the free tier of a CDN-backed service like Github Pages or Netlify
* A responsive, mobile-first theme with syntax highlighting and readable typography
* Modern markup practices; JSON-LD Structured Data, OpenGraph, and semantic HTML5
* Reasonable privacy practices; I live in the EU, so I must make a good-faith effort at GPDR compliance
* Easy social sharing to Facebook, LinkedIn, and Twitter, but _without_ unnecessary tracking
* Some form of commenting on posts, so I can hear from the readers I sincerely _hope_ will arrive
* Minimal ability to sign up for a mailing list; a lot of people left RSS after Google Reader died
* _Fast_ load time; I've been _badly_ bitten by Tumblr; Google's AMP pages _seemed_ ideal
* A decent nod to accessibility; I'm getting older and I've got friends that are visually impaired

Now, those nine criteria might seem like a lot -- and, in hindsight, maybe they were -- but really they can be boiled down to **deliverable**, **discoverable**, and **readable**, and since my visual needs are _pretty_ bare-bones they didn't seem like too much of an ask.

Of course I'd quicky learn that some of these had natural, even insurmountable conflicts -- AMP would eventually be abandoned because it renders commenting and mailing list signup unfeasible, for instance, and social sharing and privacy don't exactly go hand in hand -- but I had _hope_.

#### Step 2: Assess the Field

Dynamic tools like Wordpress were obviously eliminated by my first criterion, so I set out to understand the options for static site generators, of which there are [many][generators]. Though I came across Hugo early in my research I _really_ didn't want to go in full bore on anything without reading up on the competition, so I set it aside for the moment.

  [generators]: https://myles.github.io/awesome-static-generators "See a list of Static Site Generators"

I tried to narrow the field by eliminating generators written in what were, to me, _exotic_ languages. As I'm extremely comfortable with Python -- far more so than I am, or ever intend to be, with Go -- I started by investigating [Pelican][pelican], [Nikola][nikola], and [Hyde][hyde][^1]. In each case it quickly became apparent that these weren't the right choice for me, as none seemed either very deep or in very wide use, and I wanted something with relatively broad adoption and a community to help me through the learning curve. No options in my number one language, then, but really how often was I going to need -- or want -- to monkey around with the generator's internals, anyway? If the tool _worked_ I shouldn't need to, I reasoned, though the ability to comprehend _how_ it worked would be nice. Plus, at the end of the day, my itch for speed stems in part from _many_ years waiting on Python, so the siren song of _fast_ lured me a little further out of my comfort zone.

  [pelican]: https://blog.getpelican.com/ "The Pelican static site generator"
  [nikola]: https://getnikola.com/ "The Nikola static site generator"
  [hyde]: https://hyde.github.io/ "The Hyde static site generator"

  [^1]: Hyde's own site looking different when served over http vs https didn't inspire confidence.

Of course I also checked out [Jekyll][jekyll], the Ruby-written, Github Pages first class member; an extremely solid alternative that's polished enough to be on its third major release, with a community large enough to demand some level of stability, and which certainly seemed friendly enough. But I'm not _at all_ interested in Ruby, so lingering fear of having to get under the hood at least once, coupled with the -- by all accounts quite obvious -- speed differential, tipped the balance towards Hugo. Besides, Jeykll _felt_ long in the tooth, with some long unaddressed issues and theme showcases bloated by what certainly looked to me like a large amount of swine and only a few pearls. Even its own website seemed dated and rather dull, which added to the perception that it wasn't keeping up with the times.

  [jekyll]: https://jekyllrb.com/ "The Jekyll static site generator"

#### Step 3: Embrace Confirmation Bias

By contrast there was an obvious, churning buzz around Hugo among tech bloggers I admire, a solid amount of recent commit history, and some definitely cool sounding features like [Hugo Pipes][pipes]. As a neophyte to static, self-managed blogging I really hoped for something that might save me from the confusing tide of tooling that seems to inundate the world of web development[^2], so Pipes looked like a big shiny win. 
  [pipes]: https://gohugo.io/hugo-pipes/introduction "Check out Hugo Pipes"

  [^2]: I'm staring balefully at you `npm`, `grunt`, `yarn`, `webpack`, `yack` and `pork`, the last two of which I'm not even _sure_ I just made up.

And, glancing through the [theme browser][themes], there were a high proportion of options that looked good -- if not _ideal_ -- for the minimalist tech blog I was _obviously_ going to _finally_ have up and running **any day now**. I quickly found themes that met _most_ of my functionality criteria, and others that seemed to implement some of what was missing. So I might need to figure out how to transplant some elements, Frankenstein-like, from one theme into another, but the templating syntax _looked_ simple enough, there seemed to be a lot of [documentation][docs], and there were obviously active [forums][discourse] with lots of meat to chew through.

  [themes]: https://themes.gohugo.io "Visit Hugo's themes showcase"
  [docs]: https://gohugo.io/documentation/ "Hugo's documentation"
  [discourse]: https://discourse.gohugo.io/ "Hugo's forums"

So, after some more comparison on drearier topics like CI deployment and hosting options, the decision was made. Hugo had been an early contender, and now it was Hugo for the win! I was confident; I'm a greenfield blogger, no big -- or for that matter _any_ -- back catalogue to worry about importing... all I've got to do is pick a theme, start writing my first post, and deploy! I'll be up in days! Maybe even _hours_!

What could go wrong?

### It Doesn't Exactly Work Out of the Box

<blockquote>
  <p>You never get a second chance to make a first impression.</p>
  <cite>Head & Shoulders</cite>
</blockquote>

Maybe it was bad luck, maybe it was the winds of change, most likely it was an errant commit on the Ananke theme -- who knows? -- but on the fateful day I first did the [quickstart][quickstart] I rapidly and tenaciously made it all the way to the moment of truth, breathlessly ran `hugo server -D` and then, aching with anticipation, opened a browser window and pointed it at the localhost address conventiently displayed in the terminal. Where I found absolutely _bupkiss_ being served. Nada. A blank screen with an empty source file. Back in the terminal where I'd launched the command there were several warnings, but nothing that could obviously explain the error.[^3]

  [^3]: As of the day I'm writing this running through the quickstart instructions does in fact work, though with a great many deprecation warnings. You'll end up with a site that looks nothing like the theme demo page, though; even the gargoylish top splash image doesn't load. 

This was _disappointing_. But at the end of the day I had zero interest in using Ananke, so I decided to try the rest of the quickstart with one of the more me-appropriate themes I'd already bookmarked.

... it didn't work. Neither did the next.

Neither did the following _three_.

#### The Agony of Teething

Hugo is an open source project; as of right now its most recent [release][releases] is 0.55. Unlike Jekyll it hasn't yet reached a 1.0 release, and thus has made no promises about backwards compatability. And that's _fine_. Each of the themes is similarly an open source effort, typically -- though not always -- with a single developer who is very possibly the sole invested consumer as well. And so things have broken, _badly_. Which maybe is to be expected, in a project this immature.

But for each and every one of these themes the "official" hosted demo of the theme appears to work fine, which gives a Hugo-newbie like me the impression that there are _many_ more out-of-the-box functional themes than there actually are.

  [releases]: https://github.com/gohugoio/hugo/releases "See Hugo Releases on Github"

So what gives? Well it turns out it's because the hosted showcase uses the `exampleSite` directory embedded in each submitted theme, something not even mentioned in the quickstart, and _very_ often the templates in the theme depend on configuration that simply won't be present in your quickstart site.

Eventually, after _much_ reading of old forum posts and tripping through a lot of documentation well past its best before date, I discovered the following _usually_ gives you a local theme demonstration that behaves roughly as the author intended:

```bash
mv config.toml config.toml.bak
cp -r themes/YOUR_THEME/exampleSite/* .
find . -maxdepth 1 -type f \( -name "config.toml" -or -name "config.yaml" -or -name "config.json" \) -print -quit | grep -q "." || cp config.toml.bak config.toml
cp themes/YOUR_THEME/archetypes/*.* ./archetypes/
```

The first line backs up the default `config.toml` file before the contents of the theme's `exampleSite` directory are copied into the root. We need to move `config.toml` because that file, if present, will take precedence over `config.yaml`, which will in turn take precedence over `config.json`. That's right, Hugo has had **three** configuration file formats over its short life, and all three remain viable options, though for some reason TOML has the edge. Since _any_ of them may have been present in the theme, we'll only move the backup back into place if _none_ of them were.

Similarly the final line overwrites the `archetypes/default.md` file with any and all files in the theme's `archetypes` directory; this is because currently Hugo will _always_ assume that a `default.md` in the root `archetypes` directory should override _any_ archetype from the theme, no matter how specialized it may be. The end result is that the `hugo new posts/my-first-post.md` command mentioned in the quickstart won't include theme-critical elements in the post's [front matter][front_matter], quite often leading to errors or missing content.

  [front_matter]: https://gohugo.io/content-management/front-matter "Learn about Post Front Matter"

And as I said the above fixes will only _usually_ give you a working example of the theme you've chosen. The Ananke theme itself, for instance, will need further steps:

```bash
sed -i 's/gohugo-theme-ananke/ananke/' config.toml
sed -i 's/^themesDir/#themesDir/' config.toml
```

These are required because the quickstart instructions had you rename the theme directory as you made the submodule, and the **themesDir** configuration key was set apparently as a hack to make the theme easier to test.

These sorts of issues mostly derive from the various themes having been written at various stages in Hugo's _rapid_ evolution, and many of them have committed to old choices that no longer remain the best practice, or are now pending deprecation[^4]. One phylogentic tree of themes _requires_ content to be in `content/post` instead of `content/posts`, another will fall down if it's not the other way around.

  [^4]: Hence the warnings you'll see in the quickstart with Ananke, even with the fixes describe above.

These are, though, the relatively minor issues; take a dew days, pore over the forums and the documentation, make a few key configuration changes, possibly clear out a few of the cobwebs in a partial or two, and you're good, right?

#### Failure is a Recursing Theme

<blockquote>
  <p>This isn't life in the fast lane, it's life in the oncoming traffic.</p>
  <cite>Terry Pratchett</cite>
</blockquote>

If I've learned anything on this saga it's that themes for static blogs tend to be fairly and surprisingly complex beasts, and that human beings can make them _far_ more complex than that. As a rule you should assume, going in, that whoever wrote the theme you've chosen only understood -- or at least only encountered -- a fraction of the potential issues. As just one example of an issue repeatedly encountered, a small and seemingly innocuous change to a configuration value can suddenly turn Hugo's vaunted speed into an equally impressive amount of thumb twiddling, as you wait for the server to time out and spit out a complaint about excess recursion. Unfortunately this is one of a family of errors that leaves you with no clear idea where the problem child might be, or even what file was being processed.

My encounters with these recursion issues weren't extremely common, but frustrating enough that I tried to figure out what was going on; they _seem_ to be related to the usage of the [Scratch][scratch] area, a sort of variously site / page / template localized "scratchpad" that the Hugo team bolted on to overcome an apparent deficiency in the Go template language.[^5]. The Scratch facility seems to have been added to attend to a narrow problem, but it was apparently adopted enthusiastically -- and perhaps too widely and, at times, inappropriately -- by theme authors. Unfortunately they've done that off of sparse documentation on what is an obviously powerful, but seemingly dangerous, feature, and more importantly a feature you, the theme _consumer_, can't know is in use without knowing your theme's various templates both _deeply_ and _intimately_.

  [scratch]: https://gohugo.io/functions/scratch/ "Read about Hugo's .Scratch"

  [^5]: Variables could be assigned in templates with the `:=` assignment operator, but not updated. This appears to have been quietly fixed at some point (there is now a `=` update operator), reducing or possibly eliminating the need for the Scratch space, at least _within_ a single template's scope.

Debugging these sort of issue is _hard_, and if you're not a reasonably seasoned developer you won't have a hope of doing so. And, beyond Scratch, the Go templating language is _impressively_ flexible and powerful, allowing you to embed significantly more complex logic into templates than I've seen in other such template DSLs. But this brings with it a consequent and potentially explosive increase in the complexity and number of possible errors. Since there's -- as of yet -- no meaningful or obvious way to test a template, you can imagine that the reliability of the various themes in the showcase is _extremely_ variable.

### Lessons Hard Won

None of the above is to say that there aren't themes out there that work, and work well, out of the box, just that I never found them. However I also got nowhere near testing them all, and it's entirely possible that I just chose un-wisely, so your mileage may vary. And of course your needs may simply not overlap with mine; if you need a single page landing site or a product launch page there are slick looking, seemingly professional offerings that may work perfectly with only the most minimal configuration.

But if you _are_ like me, with relatively low experience in web programming and a strong desire to start producing content quickly, and with as much out-of-the-box support as conceivably possible, then be forewarned that the _implicit_ promise of getting up and running fast with Hugo is quite a hollow one.

If you're not interested in -- or capable of -- monkeying around with theme internals, then Hugo is almost certainly **not** the right choice for you, at least not yet. If you _are_ interested and capable, then realize that even if you don't end up rewriting every line of your chosen theme -- and there's a _very_ good chance you will _want_ to -- then you're _definitely_ going to invest a significant amount of time browsing, installing, shake-down testing, and rejecting themes in the showcase. And ultimately you're going to find that you will be _required_ to understand what is happening internally to a degree that simply isn't immediately true with other more mature, stable, and well documented projects in this space.

And if you don't intend to be _especially_ prolific -- or if you haven't already got a _substantial_ back catalogue of posts -- then there's a very substantial chance that the dividends paid by Hugo's _extremely_ impressive rendering speed simply won't ever repay that investment, much less bring you real returns on it.

That said if you _do_ have the temerity to start from scratch -- as I eventually ended up doing with my own theme -- then pat yourself on the back when those frustrating months of effort are done, because that first post -- this one -- feels _good_, even if it took a very long time to see it finally rendered.
