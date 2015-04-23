# Side Projects
## Front &amp; Center

<br>

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)

Slides: [talks.kadamwhite.com/side-projects-empirejs](talks.kadamwhite.com/side-projects-empirejs)

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

??? You can plan for that, but you can't make it happen -- and it's rarely where the idea starts. Most things start small.
---

## `+= 'new skills'`

??? So why do we *really* work on SPs? The most common reason is naturally to learn new skills. I head this described as "me +=" in one blog...

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

and decide which ones to keep for next time

<br>

### Express
### *Ampersand*
### *Combyne*
### Browserify

??? For MBTAwesome, for example, I learned I enjoyed using Browserify to build my application, and that's lead me to consider Ampersand for my next project.

---

## Practice Makes Perfect?

??? The more you solve the same problem, the more practiced you are at working through it&mdash;you build muscle memory.

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

# *Thank You!*

