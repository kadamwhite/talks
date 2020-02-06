## The Past & Future of the
<!-- .element: class="montserrat" -->
# WordPress REST API
<!-- .element: class="montserrat" -->

<hr>

K. Adam White &bull; [@KAdamWhite](https://twitter.com/kadamwhite)


<img src="../../2018/wceu/images/hm-logo.png" style="margin-top: 0; height: 2em;" alt="Human Made Logo" />

---

> ...to me, it means "I can talk to WordPress, too."

<small>*~ Ashley Kolodziej, LoopConf 2018*</small>

---

# REST
### _Representational State Transfer_

---

### HTML
### PHP
### MySQL

???

Traditional Site

---

### _DATA_
### PHP
### MySQL

???

Traditional Site

---

## REST transfers object representations

## XML-RPC calls methods

---

## XML _vs_ JSON

---

## REST

is an architectural style, not a standard

---

## REST Principles

- Client-Server
- Stateless
- Cacheable
- Layered
- Hypermedia as the engine of application state (HATEOAS)

---

# `json-api`

2009

---
<!-- .slide: data-background="url('images/jetpack-api.png')" -->

https://developer.wordpress.com/2012/10/26/using-the-rest-api-with-wordpress-org-self-hosted-sites-via-jetpack/

---

<!-- .slide: data-background="url('images/dotcom-api-its-alive.png')" -->

https://developer.wordpress.com/2012/04/05/rest-api/

---

<!-- .slide: data-background="url('images/dotcom-api-v1-1.png')" -->

https://developer.wordpress.com/2015/01/06/rest-api-v1-1/

---

# Since Merge

---

# Burnout

---

# Focus

---

The REST API as a common utility and shared resource

A community effort

---

https://make.wordpress.org/core/2017/08/23/rest-api-roadmap/

ROADMAP

---

https://make.wordpress.org/core/2017/01/04/focus-tech-and-design-leads/

FOCUS ANNOUNCEMENT

---

https://make.wordpress.org/core/2016/10/19/wordpress-rest-api-success-metrics/

API SUCCESS METRICS

---

https://make.wordpress.org/core/2016/10/13/merge-proposal-discussion-rest-api-content-endpoints/

---

https://make.wordpress.org/core/2016/10/08/rest-api-merge-proposal-part-2-content-api/

---

# &hellip;GraphQL?

---

# Data Modeling

---

`register_rest_field()`

---

# Performance

Ongoing!

---

## Gutenberg Support

- New endpoints
- New functionality
- Challenges to old assumptions

---

## Persistent
# Misunderstandings

---

## The REST API is a set of endpoints

It is also the infrastructure needed to create new, custom endpoints

---

## "The REST API makes all my site data public"

The API only exposes data which is public on an average WordPress site.

---

## ` 'show_in_rest' => true,`

---
<!-- .slide: data-background="url('../../2016/wp-node-feelingrestful/images/2014-project-architecture.svg')" data-state="semi-solid-bg" -->

### WP as _Component_
<!-- .element: class="whitebg" -->

---

<!-- .slide: data-background="url('../../2016/wp-node-feelingrestful/images/2014-project-wp-data-flow.svg')" data-state="solid-bg" -->

???

So Bocoup's been using WordPress in our client projects for three years, specifically because of the REST API. We work on complex applications composed of many parts and services, and the REST API makes WordPress something we can use as a strategic component, not a monolithic platform.

Something we can use exclusively for its strengths, such as its maturity as a content editing tool. *We* here know it isn't perfect, but writers don't want to learn Markdown, and they shouldn't have to!
<!-- .slide: class="center" -->

# <em><span style="font-size: 2em">4.7</span></em>

??? And that's where we were at the end of the summer last year. Bocoup, and many other companies, were building complex, highly-customized applications and websites using the REST API. There was a lot of interest, but the content endpoints that make it broadly useful weren't yet part of core.

We pitched the API for 4.6, but it wasn't ready. So at the start of the 4.7 cycle, we sat down to figure out how to get this into core.

---
<!-- .slide: class="center" -->

<div style="text-align: left;">
<h3>&#x2611; Meta Handling</h3>
<h3>&#x2611; Password-Protected Posts</h3>
<h3>&#x2611; Site Settings endpoint</h3>
<h3>&#x2611; Improved consistency &amp; examples</h3>
</div>

??? We had a hit-list of technical issues: meta handling, password-protected posts.

By October, we had an API that was technically ready; hundreds of contributors, support from Helen & Aaron. We'd come up with solutions to almost all our known technical challenges. And then, the merge almost didn't happen.

Because Helen asked us a question that should have been simple.

---
<!-- .slide: class="center" -->

# Who Is This For?

??? She asked us, Who is this for? Why does it belong in core?

We answered, "for everybody!"

---
<!-- .slide: class="center" -->

# &ldquo;Everyone!&rdquo;

??? And of course, it wasn't, really -- The highest-profile WP API projects had been the ones where we built out custom endpoints, custom data types, custom interfaces; this would be the sort of work we do at Bocoup, HumanMade, The Alley, 10up, etc. These are exciting projects, but the implementations are domain-specific, only relevant within the client's organization.

---
<!-- .slide: class="center" -->

# <large>80 / 20</large>

<br>

## WordPress 4.7:
### *&ldquo;Now With 2% More code!!&rdquo;*

??? We hadn't demonstrated what benefit this would have that would justify putting it onto a quarter of the web. How do you write release notes for an API?

Software : APIs :: Sculpture : Stuff

"now with 2% more code!"

While I appreciate what Ryan said yesterday about dev UX, we can's compromise our philosophy, and WP is a product that exists for the people that use it.

(upgrade now)

---

## Conditional Merge

**_And [Success Metrics](https://make.wordpress.org/core/2016/10/19/wordpress-rest-api-success-metrics/)_**

- Metric #1: Plugin utilization
- Metric #2: Distributed theme utilization
- Metric #3: Custom development implementations
- Metric #4: Core development and feature projects

??? In the end we did get the go-ahead to merge the API into core, but it was conditional. We've got to broaden our usage and demonstrate the power of the REST API at scale.

---

### The REST API is for
# WordPress Core

<small>[Focus Leads for 4.8](https://make.wordpress.org/core/2017/01/04/focus-tech-and-design-leads/)</small>

??? And so, if you saw the State of the Word, the API is a focus area for 4.8 to improve usage of the API inside WP-Admin, eventually replacing Admin Ajax in most or all places.

We are starting by migrating existing functionality in places where the current behavior is inconsistent, such as bulk actions.

This will provide direct improvements to our users, and reference implementations for plugin developers and future core enhancements.

It will also highlight what the API can't do, right now; and we'll be expanding support for menus, improving date handling, adding batching, etc

---

### The REST API is for
# Plugin Developers

??? As well as support plugin developers.

I am not a plugin developer myself, so I hadn't fully appreciated the benefits a shared set of content endpoints could bring; more and more plugins provide endpoints for their own data, but WordPress is a publishing platform, and having access to the editorial content of a site in a consistent way is tremendous for plugin development.

Another focus for our team this year is remote API authentication, such as improving OAuth support and releasing better tools to simplify the process.

This will drive both the sorts of custom work we've seen already, and continue to improve the ability of plugins to tie in to external services and offerings.

---

> If this doesn’t end up in core, we’ll start rolling our own API for stuff. Others will too. Interoperability won’t be there [...] this is much more like all of us using the same table space in MySQL.
> 
> <small>~ [@joostdevalk](https://wordpress.slack.com/archives/core-restapi/p1476306524006688)</small>

??? We don't have plugin dependency management yet, and that is not a burden an average user should be expected to bear. If core does not provide an opinion about how to model core types, plugins would have to roll their own, and we'd end up with a big mess.

---

## Access Common Data

## Model Custom Data

??? And not only do the classes in 4.7 provide access to native WordPress data types: those classes also make it much easier than before to model custom data.

This has been a narrative-heavy talk, want some code?

---

## Start

---

## Move endpoint maintenance into their components

---

## Ensure new editor endpoints are not _too_ specific to Gutenberg

---

The API team doesn't have the bandwidth to develop new endpoints

We also lack comprehensive documentation around best practices, so there is no guidance for teams which create their own

---

# Join Us!

## `#core-restapi`

---

Successes & Failures in Component Leadership

???

I have failed

Timothy is succeeding

---

# Thank You

## `#core-restapi`

<hr>

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)


<img src="../../2018/wceu/images/hm-logo.png" style="margin-top: 0; height: 2em;" alt="Human Made Logo" />

???

Thank you for having me, and enjoy the rest of WordCamp Asia!