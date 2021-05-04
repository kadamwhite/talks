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
<!-- .slide: class="align-left" -->
## Hi, I&rsquo;m KAdam!
<!-- .element: class="italic" -->

 &nbsp; | &nbsp;
 ------------ | ------------
**2014–2016** | WP-API plugin contributor/advocate
**2016** ✨ | csv,conf,v2 speaker 👋
**Late 2016** | Coordinated merge effort
**2017–2019** | REST API lead maintainer

&nbsp;

Current lead maintainer<br> is[@TimothyBJacobs](https://twitter.com/timothybjacobs?lang=en)

---
<!-- .slide: class="align-left" -->

#### what has changed
## since 2016?

???

- Surprisingly little in some ways
- iterative improvement
- endpoints, search
- filtering & perf
- But most of all,

---
<!-- .slide: class="align-left" -->

# Gutenberg
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-top" data-background-position="top" data-background-size="cover" data-background-image="/talks/2021/csvconf/images/gutenberg.png" -->

---
<!-- .slide: class="align-left" -->

#### what have we _learned_
## since 2016?

???

About the API, or about data

---
<!-- .slide: class="align-left" -->
When proposing a change,

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

Though, both to honor the day -- may the fourth be with you -- and to be more transparent, maybe it&rsquo;s worth admitting that to our eyes, it was so self-evident that this was good that in our talks that year we were really saying that WordPress _without_ such API didn't bear thinking about,

---
<!-- .slide: data-background-color="black" data-background-size="contain" data-background-repeat="no-repeat" data-background-image="/talks/2021/csvconf/images/return-of-the-jedi-celebration.png" -->

---
<!-- .slide: class="align-left" -->

## &ldquo;who is this for?&rdquo;
<!-- .element: class="italic" -->

--

> If this doesn’t end up in core, we’ll start rolling our own API for stuff. Others will too. Interoperability won’t be there&hellip;
>
> <small>~ [@joostdevalk](https://wordpress.slack.com/archives/core-restapi/p1476306524006688), Oct 12, 2016</small>

---
<!-- .slide: class="align-top" -->

&nbsp;
# interoperability
<!-- .element: class="italic" -->

A strong foundation for plugin interaction

???

The most convincing argument was from plugin developers, who advocated for the API quite heavily throughout 2016. The writing was on the wall about needing data access from JS, and if WP core didn't provide an opinion about how to model core content, each plugin would have to roll their own. Without a central authority, we'd end up with a big mess.

---
<!-- .slide: class="align-left" -->
### Conditional Merge

**_and [metrics for success](https://make.wordpress.org/core/2016/10/19/wordpress-rest-api-success-metrics/)_**

- Plugin utilization
- Distributed theme utilization
- Custom development implementations
- Core development and feature projects

???

We hadn't demonstrated what benefit this would have that would justify putting it onto a quarter of the web.

In the end we did get the go-ahead to merge the API into core, but it was conditional. We've got to broaden our usage and demonstrate the power of the REST API at scale.

--

### One feature project within
<!-- .element: class="italic" -->
## three major releases
<!-- .element: class="italic" -->

(thanks for the save, Gutenberg 😁)

???

- got by on a technicality with G

---
<!-- .slide: class="align-left" -->
## should we have waited?
<!-- .element: class="italic" -->

???

This raised the Q

---
<!-- .slide: class="align-left" -->
An API contract is a

# standard
<!-- .element: class="italic" -->

???

This isn't a surprise to many here, I'm sure, but what we were doing was proposing a data standard for use across WordPress. Standards enable collaboration and interaction, as well as data portability

Broader use than if we'd waited for G

---
<!-- .slide: class="align-left" -->
Does your data API plan for

# versioning
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-left" -->
how granular are users&rsquo;

# capabilities
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-left" -->

## who can _access_ the data?
<!-- .element: class="italic" -->
## who can _modify_ it?
<!-- .element: class="italic" -->

???

In WP this can be modified at runtime with the map_meta_cap and user_can filters

--
<!-- .slide: class="align-left" -->
adapted Hyper Schema&rsquo;s `targetSchema`
```json
{
  "rel": "https://api.w.org/action-publish",
  "title": "The current user can publish this post.",
  "href": "https://www.kadamwhite.com/wp-json/wp/v2/posts/{id}",
  "targetSchema": {
    "type": "object",
    "properties": {
      "status": {
        "type": "string",
        "enum": [ "publish", "future" ]
      }
    }
  }
},
```

---
<!-- .slide: class="align-left" -->
adapted Hyper Schema&rsquo;s `targetSchema`,<br>exposed as `apiResource._links`
![_links property on a WP object](/talks/2021/csvconf/images/_links.png)

---
<!-- .slide: class="align-left" -->

## Data&rsquo;s only as<br>good as what you<br>can do with it

???

- Inaccessible data is useless, as is untrustable data
- Can't leave access as an afterthought

---
<!-- .slide: class="align-left" -->
We dragged our heels on providing options for

# authentication
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-left" -->
At time of merge&hellip;

## _Core:_ Cookie &amp; Nonce
<!-- .element: class="italic" -->

### _Plugins:_ Basic Auth, Application Passwords, JWT, OAuth 1.0a, OAuth 2, Central Broker...
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-left" -->
## _insufficient_ docs
<!-- .element: class="italic" -->

## _no_ examples
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-left" -->
This one&rsquo;s on me, as the component lead:

## I let &ldquo;perfect&rdquo; be<br>the enemy of &ldquo;good&rdquo;
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-left" -->
## WordPress 5.6 "Simone"
<!-- .element: class="italic" -->

Application Passwords added

### December 2020

---
<!-- .slide: class="align-left" -->
One Final Lesson

# burnout
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-left" -->

## heroic underdogs
<!-- .element: class="italic" -->
## considered harmful

???

- Could use more maintainers, but not alone in that
  - Shout-out to Timothy, jonny, alain, felix, george, etc
- words matter
- mixed signals from Leadership
  - I don't think matt was a good steward

---
<!-- .slide: class="align-left" -->

## signals from project leadership carry weight
<!-- .element: class="italic" -->

--

## Goals:

- Components own their own endpoints
- API team serves as documentation & standards body

---
<!-- .slide: class="align-left" -->

## Empower contributors
<!-- .element: class="italic" -->
## Recognize burnout
<!-- .element: class="italic" -->
## Bigger than us
<!-- .element: class="italic" -->

---
<!-- .slide: class="align-left" -->

# worth it?
<!-- .element: class="italic" -->

---

<!-- .slide: class="align-left" -->
## Curb Cut Effect

> ...to me, [the REST API] means &ldquo;I can talk to WordPress, too.&rdquo;

<small>*~ [Ashley Kolodziej](https://twitter.com/ashleykolodziej), Boston University, [LoopConf 2018](https://www.youtube.com/watch?v=lUslM1aXjpo)*</small>

---
<!-- .slide: class="align-top align-left" -->

## summary
<!-- .element: class="italic" -->

- Know why the data standard matters
- Plan for versioning from Day 1
- Understand the nuances of permissions & access
- Provide a documented authentication solution
- It&rsquo;s never &ldquo;us _vs_ them&rdquo;:<br>FOSS is a community effort
- Curb cutting effect

---
<!-- .slide: class="align-top align-left" -->

### <br>thanks-for-having-me.csv

- Slides: [kadamwhite.github.io/talks/2021/csvconf](https://kadamwhite.github.io/talks/2021/csvconf)
- API Handbook: [developer.wordpress.org/rest-api](https://developer.wordpress.org/rest-api)
- Us: [humanmade.com](https://humanmade.com)

&nbsp;

# Questions?
<!-- .element: class="italic" -->
