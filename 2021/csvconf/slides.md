<!-- .slide: class="align-left" -->
### WordPress as Data
## 5 Years In
<!-- .element: class="weight-normal" style="font-size:3em" -->

<hr>

K. Adam White &bull; [@KAdamWhite](https://twitter.com/kadamwhite)

<img src="/talks/2021/csvconf/images/hm-logo-white.svg" style="height: 1.5em;" alt="Human Made Logo" />

---
<!-- .slide: data-background-image="/talks/2021/csvconf/images/altis-dxp-com.png" data-background-position="top" -->

---
<!-- .slide: data-background-image="/talks/2021/csvconf/images/gh-contrib-graph.png" data-background-position="top" -->

---

## Hi, I'm KAdam!
<!-- .element: class="italic" -->

 &nbsp; | &nbsp;
 ------------ | ------------
**2014–2016** | WP-API plugin contributor/advocate
**2016** ✨ | csv,conf,v2 speaker 👋
**Late 2016** | PM for merge effort
**2017–2019** | REST API lead maintainer

&nbsp;

Current lead maintainer is [@TimothyBJacobs](https://twitter.com/timothybjacobs?lang=en)

---

#### what have we learned
## since 2016

--

### <span class="weight-normal">what is</span> _WordPress?_
### <span class="weight-normal">what is a</span> _REST API?_

---
Lesson 1

<hr class="short">

# know why
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-top" data-background-size="cover" data-background-image="/talks/2021/csvconf/images/society_if.jpg" -->

### Society if WP had a REST API
<!-- .element: class="meme" -->

???

We said, "everybody, obviously!" Look what you could do with it!
In retrospect, five years ago we were all going around to conferences like this and prosletyzing a utopian vision of how WP could be if we merely increased the size of the codebase by 2%.

---
<!-- .slide: class="align-top" data-background-color="black" data-background-size="contain" data-background-repeat="no-repeat" data-background-image="/talks/2021/csvconf/images/return-of-the-jedi-empire.jpg" -->

### Society if it _doesn't_ get one
<!-- .element: class="meme bottom" -->

???

Though, both to honor the day -- may the fourth be with you -- and to be more transparent, maybe it's worth admitting that to our eyes, it was so self-evident that this was good that in our talks that year we were really saying that WordPress _without_ such API didn't bear thinking about,

---
<!-- .slide: data-background-color="black" data-background-size="contain" data-background-repeat="no-repeat" data-background-image="/talks/2021/csvconf/images/return-of-the-jedi-celebration.png" -->

---

> If this doesn’t end up in core, we’ll start rolling our own API for stuff. Others will too. Interoperability won’t be there&hellip;
> 
> <small>~ [@joostdevalk](https://wordpress.slack.com/archives/core-restapi/p1476306524006688), Oct 12, 2016</small>

???

The most convincing argument was from plugin developers, who advocated for the API quite heavily throughout 2016. The writing was on the wall about needing data access from JS, and if WP core didn't provide an opinion about how to model core content, each plugin would have to roll their own. Without a central authority, we'd end up with a big mess.

---

### Conditional Merge

**_and [metrics for success](https://make.wordpress.org/core/2016/10/19/wordpress-rest-api-success-metrics/)_**

- Plugin utilization
- Distributed theme utilization
- Custom development implementations
- Core development and feature projects

???

We hadn't demonstrated what benefit this would have that would justify putting it onto a quarter of the web.

In the end we did get the go-ahead to merge the API into core, but it was conditional. We've got to broaden our usage and demonstrate the power of the REST API at scale.

---

### One feature project within
<!-- .element: class="italic" -->
## three major releases
<!-- .element: class="italic" -->

???

To start, one admission: we squeaked by on a technicality with these metrics, because Matt Mullenweg froze major WP releases after 4.9,

---

# Gutenberg
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-top" data-background-position="top" data-background-size="cover" data-background-image="/talks/2021/csvconf/images/gutenberg.png" -->

---

A core REST API gives plugin developers

# interoperability
<!-- .element: class="italic" -->

---

An API contract is a

# standard
<!-- .element: class="italic" -->

???

This isn't a surprise to many here, I'm sure, but what we were doing was proposing a data standard for use across WordPress. Standards enable collaboration and interaction, as well as data portability

---
Lesson 2

<hr class="short">

# authentication
<!-- .element: class="italic" -->

---

## _Core:_ Cookie &amp; Nonce
<!-- .element: class="italic" -->

### _Plugins:_ Basic Auth, Application Passwords, JWT, OAuth 1.0a, OAuth 2, Central Broker...
<!-- .element: class="italic" -->

---

# _no_ docs
<!-- .element: class="italic" -->

# _no_ examples
<!-- .element: class="italic" -->

---

> That's not good enough, we need something _**perfect**_
>
> ~ me, _**way**_ too often

---

## WordPress 5.6 "Simone"
<!-- .element: class="italic" -->

Application Passwords added

### December 2020

---
Lesson 3

<hr class="short">

# capabilities
<!-- .element: class="italic" -->

---

## who can _access_ the data?
<!-- .element: class="italic" -->
## who can _modify_ it?
<!-- .element: class="italic" -->

---
Lesson 4

<hr class="short">

# versioning
<!-- .element: class="italic" -->

---
The Final Lesson

<hr class="short">

# burnout
<!-- .element: class="italic" -->

---

## heroic underdogs
<!-- .element: class="italic" -->
## considered harmful

---

### was it worth it?

---

> ...to me, [the API] means "I can talk to WordPress, too."

<small>*~ [Ashley Kolodziej](https://twitter.com/ashleykolodziej), Boston University, [LoopConf 2018](https://www.youtube.com/watch?v=lUslM1aXjpo)*</small>

---
<!-- .slide: class="align-top align-right" -->

### <br>thanks-for-having-me.csv

Slides: [talks.kadamwhite.com/2021/csvconf](https://kadamwhite.github.io/talks/2021/csvconf)

# Questions?
<!-- .element: class="italic" -->
