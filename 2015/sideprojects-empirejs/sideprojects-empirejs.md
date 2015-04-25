# Side Projects
## Front &amp; Center

<br>

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)

Slides: [talks.kadamwhite.com/sideprojects-empirejs](http://talks.kadamwhite.com/sideprojects-empirejs)

---

## What is a Side Project?

??? Most of us probably have some idea of what SPs are: they're pretty pervasive in our field. But let's be specific:

---

> any self-contained project that's not your main deliverable

??? So, a moment for definition: for our purposes, a SP is any self-contained project that is not part of your main, deliverable codebases or role

---
<!-- .slide: data-background="url('images/projects/aredridel-html5.png')" -->
[Aria Stewart, HTML5 parser](http://github.com/aredridel/html5) <!-- .element: class="caption" -->

??? I asked around on twitter for what sorts of projects we're working on within this community, and I got everything from a JS HTML parser..

---
<!-- .slide: data-background="url('images/projects/jjj-shower.jpg')" -->
<span>[John James Jacoby](http://jaco.by/), Bathroom Shower (WIP)</span> <!-- .element: class="caption" -->

??? to a home shower remodeling project. For this conversation that we're not limited to the web, or to code.

---

*et tu?*

??? let's get a show of hands if you have some sort of side project of your own: Should be most of you. Many of the speakers at this event are talking about their own side projects.

---

## Why

## When

## How

??? We're going to focus today on the benefits that side projects bring us, as individuals and organizations; how we can integrate regular creative exploration into our work; and how we can take some basic steps to give ourselves the best chance of success in our projects.

---

# Why?

??? Why is it that we all have these projects kicking around? What are we trying to do when we start a side project?

---
## Fame & Fortune

??? I think I speak for most of us when I say that I'm in it mainly for the fame. After all, some of the most prevalent pieces of software in the world began as side projects!

---

> My logging software hasn’t been updated for months &hellip; What to do?
> 
> b2/cafelog is GPL, which means that I could use the existing codebase to create a fork &hellip;

<small>*~ Matt Mullenweg, [The Blogging Software Dilemma](http://ma.tt/2003/01/the-blogging-software-dilemma/), 2003*</small>

??? but of course WP, for example, started out very simply: the maintainer of Matt Mullenweg's existing tool got busy, and he wanted to keep using it.

---
<!-- .slide: data-background="url('images/wp-runs-23-pct-of-web.png')" -->

??? That WP now has over 60% of the overall CMS market share (per [w3techs.com](http://w3techs.com/)) is a testament to open source licensing and a dedicated community.

---

> it would be nice to have the flexibility of MovableType, the parsing of TextPattern, the hackability of b2, and the ease of setup of Blogger.
> ## Someday, right?

<small>*~ Matt Mullenweg, [The Blogging Software Dilemma](http://ma.tt/2003/01/the-blogging-software-dilemma/), 2003 (emphasis added)*</small>

??? You can plan for that, but it's rarely where the idea starts. Most things start small.
---

# Side Projects are *fun!*

??? So why do we *really* work on SPs? There's a reason we call them "passion projects": we take time to work on side projects because we enjoy them. I've heard it called "scratching an itch," I've heard it described as "blowing off steam": we take on work we find interesting, that differs in some way from what we do normally.

---
<!-- .slide: data-background="url('images/projects/melchoyce-redradar.png')" -->

<span>Mel Choyce, [rdrdr WordPress Themes](https://themes.redradar.net)</span> <!-- .element: class="caption" -->

??? Mel Choyce, a UX designer at Automattic, makes WP themes with Kelly Dwan in her spare time and releases them as RedRadar.

---
<!-- .slide: data-background="url('images/projects/melchoyce-umbra-preview-post.png')" -->

> I get to work on what I want to work on, with no external restrictions or limitations. It's a time to let my creativity run wild and do what I want to do.
<small>*~ [Mel Choyce](https://twitter.com/melchoyce)*</small>

??? and sees it as an opportunity to exercise creativity without constraint. This is something I heard a lot when soliciting opinions for this talk.

---

## `+= 'new skills'`

??? I think enjoyment is the most important reason, but a lot of us naturally start SPs to learn new skills. I head this described as "me += skill" in one blog...

---
<!-- .slide: data-background="url('images/projects/jennschiffer-make8bitart.png')" -->

<span>Jenn Schiffer, [make8bitart.com](http://make8bitart.com)</span> <!-- .element: class="caption" -->

??? My colleague (and speaker at last year's EmpireJS) Jenn Schiffer, for example, made the awesome make8bitart.com in order to learn JS and Canvas

---

> Side projects are a good motivator to learn something new outside of your everyday job. [They] can help you delve into other realms of development.
<small>*~ [Jenn Schiffer](https://twitter.com/jennschiffer)*</small>

---

## Solidifying Skills

??? A complement to learning new skills is to reinforce the ones you have; to practice. This is a major reason I take on side projects, personally:

---
<!-- .slide: data-background="url('images/projects/kaw-mbtawesome.png')" -->

<span>K Adam White, [mbtawesome.com](http://mbtawesome.com)</span> <!-- .element: class="caption" -->

??? My Boston subway tracking application MBTAwesome let me learn some new tools, but it also gave me a chance to reevaluate the ones I'd used before

---

Start with one set of tools,

<br>

### Express
### Backbone
### *Nunjucks*
### *Browserify*

??? A benefit to projects that use a combination of old and new skills is that you can continue incrementally switching out technology as you explore different solutions to a problem

---

and decide which to keep for next time

<br>

### Express
### *Ampersand*
### *Combyne*
### Browserify

??? For MBTAwesome, for example, I learned I enjoyed using Browserify to build my application, and that's lead me to consider Ampersand for my next project.

---

## Practice Makes Perfect?

??? The more you solve the same problem, the more practiced you are at working through it&mdash;you build muscle memory, and maybe you develop a boilerplate, or a set of configurations to re-use later.

---

## Practice reveals
# pain points

??? As you repeat a task, you often find yourself encountering the same challenges over and over and over again

---

## `hundreds of jQuery plugins`
# `+`
### `repetitive gruntwork to release/maintain them all`
# `= ?`

??? that can lead to a new, completely separate project designed to solve those problems: side projects as problem-solving sandbox

---
<!-- .slide: data-background="url('images/projects/benalman-gruntjs.png')" -->

<span>Ben Alman & the Grunt Team, [Grunt](http://gruntjs.com)</span> <!-- .element: class="caption" -->

??? I always wondered how libraries like Grunt were created, and it's a very straightforward type of problem solving.

---

```
                  _____
               _.'_____`._
             .'.-'  12 `-.`.
            /,' 11      1 `.\
           // 10      /   2 \\               How
          ;;         /       ::                Do
          || 9  ----O      3 ||                  You
          ::                 ;;                    Make
           \\ 8           4 //                       Time?
            \`. 7       5 ,'/
             '.`-.__6__.-'.'
              ((-._____.-))
              _))       ((_
             '--'SSt    '--'
```
<small>*clock from [ascii.co.uk](http://ascii.co.uk/art/clock)*</small>

??? To say something's straightforward, though, doesn't mean it's easy: projects take time, sometimes a lot of it

---

## &ldquo;When do you work?&rdquo;

> Mostly weekends. Especially Sunday afternoon &ndash; night.

<small>*~ Mariko Kosaka*</small>

> It started in a Saturday night at home.

<small>*~ Leonardo Balter*</small>

> Nights and weekends.

<small>*~ Too many to mention by name*</small>

??? In the responses to my survey the most common phrase was "nights and weekends," and if you look around Github I suspect you'll see a lot of late-night or Sunday-afternoon commits.

---

> Mostly nights, mostly the time I had intended to use to build the application that [prompted my side project] in the first place. I still have not finished that application now...

<small>*~ Calvin Spealman*</small>

> It was pretty much the only thing I did for a long, long time.

<small>*~ Ben Alman*</small>

??? But there's only so many nights and weekends to go around, especially if you have other things you want to use those nights and weekends to do

---

> If you do it like I did it, you pretty much lose your social life. I recommend a slightly more balanced approach&hellip;

<small>*~ Ben Alman*</small>

>  I rarely had the time for [make8bitart]. Even today I struggle to find the time to work on it.

<small>*~ Jenn Schiffer*</small>

> It will never be &ldquo;done&rdquo;.

<small>*~ Greg Smith*</small>

??? A quick survey of my colleagues reveals some major concerns about the time needed, and the costs of that time

---

# Bring Your Projects to Work Day

??? For reasons we'll get to later, I think making time for side projects is a critical part of our professional growth&mdash;and part of that growth can happen *within* our jobs, not alongside it

---

## &ldquo;X%&rdquo; Time
## Hackathons <!-- .element: class="fragment" -->
## Project Nights <!-- .element: class="fragment" -->
## Game James <!-- .element: class="fragment" -->

??? There's actually a host of ways that this idea's already been embraced by companies around the world

---

## &ldquo;20% Time&rdquo;

> Google didn’t invent the idea of giving employees time to experiment with their own ideas, nor will it have the final word on how best to bestow such time.

<small>*~ Wired.com, ["20% Time Will Never Die", 8/21/13](http://www.wired.com/2013/08/20-percent-time-will-never-die/)*</small>

??? Google became famous for allowing engineers a percentage of their time to explore passion projects and new ideas, leading to products like Gmail. This is not a new idea,

---

## &ldquo;Bootlegging&rdquo;

> Research in which motivated individuals secretly organize the innovation process

<small>*~ Wikipedia, ["Bootlegging (Business)"](http://en.wikipedia.org/wiki/Bootlegging_%28business%29)*</small>

??? and it's not a Silicon Valley idea: it goes back decades, and was dubbed "bootlegging" in the late 60's (see Knight, K., 1967, *A Descriptive Model of the Intra-Firm Innovation Process*)

---
<!-- .slide: data-background="url('images/henrikpalm-redo-for-test.jpg')" -->

> **The 15 percent rule works** &hellip; the best-known success story is scientist Art Fry's **creation of Post-its** while trying to create bookmarks that would stay put in the church choir's hymnals.

<small>*~ Wired Magazine, ["The 15% Solution", 1/23/1998](http://archive.wired.com/techbiz/media/news/1998/01/9858) (emphasis added)*</small>
<small><small>*[Photo by Henrik Palm](https://www.flickr.com/photos/henrikpalm/5565633783), used under a [CC Attribution 2.0 Generic](https://creativecommons.org/licenses/by/2.0/) license*</small></small>

??? the post-its we use for our Scrum boards actually came out of 3M's unofficial "permitted bootlegging" policy, which evolved eventually to "15 percent time" (see http://en.wikipedia.org/wiki/Post-it_note)

---

## Hackathons

??? Hackathons take that idea, time-box it, and make it a group activity. What you lose in autonomy, the thinking goes, you gain in collaboration.

---

## Hackathons

<br>

### *Community*
### *Teamwork* <!-- .element class="fragment" -->
### *Competition* <!-- .element class="fragment" -->

??? These become as much (or more) about teambuilding and community as they do about passion projects -- but they can be an easier sell than bootlegging, or a nice complement to independent exploration

---

## Project Nights

<br>

### *Hardware,*
### *Art, Design*
### *You Name It*

??? hack days are implicitly at the organization level; Project Nights are a little different, in that (in my experience) they're employee-organized. One point-of-sale software company had a hack day to build vacancy indicators for their restrooms, giving software engineers and non-technical employees a chance to try soldering and to learn about the hardware side of their business&mdash;but the event organization was all ad-hoc. We've had art nights at Bocoup, just to blow off steam; they're different in their focus, but the same type of event.

---

# *Our Approach*

??? I think the way we balance these options at Bocoup is pretty effective, so I want to share how it works:

---

# Open Source Time

??? Every employee gets a percentage of our time to maintain, contribute to and explore open-source web technology (or culture).

This can be anything from building and releasing a general-purpose library, to writing a twitter bot while exploring how Node.js works.

We're a consulting company, so if we're on a project we may use that time to build part of their application in a reusable, modular way that we can then work with the client to open-source.

---

## Open Source Time

> I’ve always taken this kind of time in all the jobs I could&mdash;even when it wasn’t officially offered. When you do officially offer it, then I don’t have to feel guilty!

<small>*~ Jim Vallandingham*</small>

??? Supporting the web as an open platform is part of our mission, of course, but this time also codifies what we know would be happening anyway, to avoid making us feel guilty or conflicted in our explorations

---

# Perch Time

??? This is our equivalent of bootlegging and hackathons, in a way: in downtime between projects, my coworkers collaborate on building and maintaining the tools we use to keep Bocoup running. These projects are managed through a Tech Ops organization, and run like any other engineering project.

---

# Bocoupfest

??? Bocoupfest, on the other hand, is our company week: anything goes. We've built nodebots, we've learned to make spray-paint stencils; my coworker Carl lead a group to make a game for the Pebble watch last month. This is when we can "blow off steam".

---

# Projects
## *Within Projects*

??? We're so engrained in this highly parallel, asynchronous project mentality that we use it in our consulting work, too:

---

```
+-----------+--------------------------------------+-----------+
| Research  |  Implementation                      | Delivery  |
+-----------+--------------------------------------+-----------+

```

??? this past year I was leading a project to build a complex web app for a client, and we had a free-wheeling research phase at the start to prove out the tools we wanted to use.

---

```
+-----------+--------------------------------------+-----------+
| Research  |  Implementation                      | Delivery  |
+-----------+--------------------------------------+-----------+
               ^ new research task

```

??? When a new requirement came up after that phase, however, we wanted to find a way to find a solution without disrupting our existing work

---

```
+-----------+--------------------------------------+-----------+
| Research  |  Implementation                      | Delivery  |
+-----------+--------------------------------------+-----------+
              v                    ^
              +--------------------+
              | "Side Project" POC |
              +--------------------+
```

??? By spinning that proof of concept, a WordPress-backed node application, out into a "side project" alongside our main repository, we kept the research from impacting our project, then rolled it all back in when we were done.

---
<!-- .slide: data-background="url('images/projects/kaw-wp-rest-api.png')" -->

<div class="highlight">
*Released* [wordpress-rest-api](https://www.npmjs.com/package/wordpress-rest-api) (npm package)

*and* [expresspress](https://github.com/kadamwhite/expresspress) (demo project)
</div>
??? and since the work was already extracted from the main repository, it made it easy to release the fruit of our labor as an open source package, too: we can ride this feedback cycle from project to project, getting better all the time.
---

# You \*are\* what you make time for

<small>*~ [@femmebot, Sep 4 2014](https://twitter.com/femmebot/status/507613717232508928)*</small>

??? These systems are important to us, because how we spend our time defines what type of company we are. Phoebe E (@femmebot) said it well in this tweet:

---
<!-- .slide: data-background="url('images/projects/femmebot-25x52.png')" -->

<span>[@femmebot](https://twitter.com/femmebot), [25x52](http://25x52.com/)</span> <!-- .element: class="caption" -->

??? We can also learn a lot from her own side project effort, 25x52, an initiative to launch 25 projects in a year.

---
<!-- .slide: data-background="url('images/projects/femmebot-typography-1.jpg')" -->

<span>[@femmebot](https://twitter.com/femmebot), [Google Fonts Typography](http://femmebot.github.io/google-type/)</span> <!-- .element: class="caption" -->

??? She describes 25x52 as a personal initiative, starting in August of last year, and the length of the project was a deliberate choice:

---
<!-- .slide: data-background="url('images/projects/femmebot-typography-2.jpg')" -->

> I wanted to set a timeline that was **long enough to compel a behavior change** &hellip; I needed to establish a long-term **habit** of launching projects.
> 
> <small>*~ [25x52 About Page](http://femmebot.github.io/about/) (emphasis added)*</small>

??? The About page for the project contains two main takeaways, for us: **repetition builds habits**, and **milestones are important.** To quote her site again, "Shipping Products is Better than Getting Tasks Done".

---

# Regularity
## and
# Repetition

??? Let's look at repetition, and regularity.

---

## Write Code Every Day

<br>

> 1. I must write code every day.
> 2. It must be useful code.
> 3. All code must be written before midnight.
> 4. The code must be Open Source and up on Github.

<small>*~ John Resig, [Write Code Every Day, April 2014](http://ejohn.org/blog/write-code-every-day/)*</small>

??? John Resig wrote an article on this topic that really stuck with me, entitled "write code every day". He outlined a few rules for himself to keep things on track, but the title speaks for itself

---
<br>

<br>

## Go Into Your Studio
# Every Day
#### *even if it's just to wash your brushes.*

<small>*~ Jay Stuckey, artist*</small>

??? My art professor in college outlined a similar rule he uses for himself: go into the studio every day. Even if all you do is wash your brushes, it builds a habit, and a practice.

---

# Deadlines

??? Personal projects can drag on, since we're the only ones who can tell ourselves that it's "done." Imposing deadlines on yourself helps: when will you have this presentable, when will you release it, or when will you move on?

---
<!-- .slide: data-background="url('images/projects/marikokosaka-knittingmachine.jpg')" -->

<br>

> Submitting to conferences and meetups shaped &ldquo;just some doodling code&rdquo; to &ldquo;a project&rdquo;.
> 
> <small>*~ [Mariko Kosaka](https://twitter.com/kosamari)*</small>

??? Mariko Kosaka, who spoke earlier today, shared that the deadlines she takes on by presenting her work publicly help her form up her work into something that can be "finished". Our MC Adam Sontag had the same experience when he build a Web Audio Speech demo for a QueensJS talk, "carving out just enough time" to get it presentable.

---

## Managing Project Scope

```js
function() {
  var projectScope;

  function () {
    function() {
      function() {
        function() { 'what am I even working on?'; }
      }
    }
  }
}
```

??? What does it mean to "ship"? We may not release anything -- I think of it as coming to a logical stopping point. Small increments are just as important on side projects as they are in other contexts: without a well-scoped goal, a project gets frustrating
---
<!-- .slide: data-background="url('images/projects/ericandrewlewis-cool-text-converter.png')" -->

<br>

> I purposefully made **minimum viable products** along the way, so I would get quick wins and not get burnt out.
>
> <small>*~ [Eric Andrew Lewis](https://twitter.com/ericandrewlewis) (emphasis added)*</small>

??? Eric Lewis, a developer at the Times here in NY, built a "cool text converter" to do unicode glyph substitution on text strings, treating each new dialect he added as a new "release."

---

## Managing Project Scope
```js
function() {
  var projectScope;

  function () {
    projectScope.feature1 = done;
  }
  function () {
    projectScope.feature2 = done;
  }
  function (cb) {
    setTimeout(function() {
      projectScope.feature3 = cb();
    }, whenever_you_get_around_to_it );
  }
}
```

??? Especially if you're working with open source time or only working on code periodically, set well-scoped, achievable goals and the progress will be more reliable and satisfying.

---

## Work *Regularly*
## Work *Incrementally*
## Work *Towards a Deadline*

---

> These passion projects are essential outlets &hellip; and are **absolutely necessary** for staying happy, feeling trusted, and remaining free to experiment &hellip;
> 
> <small>*~ [John James Jacoby](https://twitter.com/jjj)*</small>

??? As we established with the show of hands, I don't need to convince you of this. But if you need the language to help convince colleagues or management, here's some options:

---

## Freedom Up,
# Turnover Down

??? Employees who have the freedom to explore, and get support for that exploration, don't

---

## Another kind of
# &ldquo;Professional Development&rdquo;

??? Many companies are fine sending us to conferences for days at a time, and paying for airfare and lodging&mdash;regular open source time is arguably less impactful to a project, and can be even more valuable

---

<br>

## Take the time. Always.
## Even if no one ever sees
## your work.

<small>*~ [Andrew Norcross](https://twitter.com/norcross)*</small>

??? But we know how to make the time, and I think we should.

---
<!-- .slide: data-background="url('images/emilygarfield-sketchbook-pages.jpg')" -->

<br>

<div class="highlight">

## Side Projects are not your
## portfolio, but they *can be*
# <small>a</small> sketchbook

</div>
<br>

<small>*Sketchbook pages by [Emily Garfield](http://www.emilygarfield.com)*</small>

??? To extend the art studio metaphore, it's almost self-evident that an artist, for example, keeps a sketchbook. It's part of their art practice. We work in a creative field, and it's bizarre to me that we don't make more time within our jobs to sketch, to practice, and to grow.

---

# *Thank You!*

