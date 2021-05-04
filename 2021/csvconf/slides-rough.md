### WordPress as Data
<!-- .element: class="montserrat" -->
## 5 Years In
<!-- .element: class="montserrat bold" -->

<hr>

K. Adam White &bull; [@KAdamWhite](https://twitter.com/kadamwhite)


<img src="/talks/2018/wceu/images/hm-logo.png" style="margin-top: 0; height: 2em;" alt="Human Made Logo" />

???

Thank you very much, and it's a pleasure to be able to join you all today!

I had the privilege to speak at csv,conf,v2 in 2016, and it's an honor to get to revisit that talk 5 years later.

---

### what is _WordPress_?
### what is a _REST API_?

???

To set the scene, WordPress is a free and open source CMS written in PHP, and by some counts powers about 40% of the navigable internet.

The WordPress REST API is a component within WordPress, which provides -- you guessed it -- a REST API to enable code to interact with WordPress content over HTTP.

---

Who am I, to tell you what to think? What hubris!

(Maybe put pictures of the people?)

???

To clarify roles a little bit, the development of the REST API was lead by Ryan McCue, Joe Hoyle, Rachel Baker, and Daniel Bachhuber, with code contributed by myself and a little shy of a hundred other developers.

The best way to describe my role in 2016 was as a project manager, helping to coordinate and prioritize feature development leading up to the final merge proposal in October. I then became a named lead and committer for the component from early 2017 until the start of the pandemic, when I stepped back from active participation.

The perspective in this talk are my own, though it has been informed by discussion with Ryan McCue and the current component lead Timothy Jacobs.

We'll come back to why these roles matter in a bit.

---
<!-- .slide: data-background-size="contain" data-background-image="/talks/2021/csvconf/images/wp-data-flow.png" data-background-color="white" -->

???

So, a quick recap: in 2016, I came to csv,conf to stump for the project. It was great! It would take your WordPress content, and bring it anywhere it needed to go!

It was fun for the whole family! We could build Next-gen editing interfaces, or load data into or out of WP for analysis and manipulation, or even machine learning.

We developed the API as a plugin and pitched it for WP 4.6, but it wasn't ready. So at the start of the 4.7 cycle, we sat down to figure out how to get this into core.

---

# Who was it for?

???
the merge almost didn't happen.

Because [WP lead dev] Helen Hou-Sandi asked us a question that should have been simple.
She asked us, Who is this for? Why does it belong in core?

---
<!-- .slide: data-background-position="center" data-background-size="cover" data-background="url('/talks/2021/csvconf/images/society_if.jpg')" -->

### Society if WP had a REST API
<!-- .element: class="whitebg" -->

???

We said, "everybody, obviously!" Look what you could do with it!
In retrospect, five years ago we were all going around to conferences like this and prosletyzing a utopian vision of how WP could be if we merely increased the size of the codebase by 2%.

---
<!-- .slide: data-background-position="center" data-background-size="contain" data-background-repeat="no-repeat" data-background="url('./images/return-of-the-jedi-empire.jpg')" -->

<p>Society if WP _didn't_ have a REST API</p>
<!-- .element: class="whitebg" -->

???

Though, both to honor the day -- may the fourth be with you -- and to be more transparent, maybe it's worth admitting that to our eyes, it was so self-evident that this was good that in our talks that year we were really saying that WordPress _without_ such API didn't bear thinking about,

---
<!-- .slide: data-background-position="center" data-background-size="contain" data-background-repeat="no-repeat" data-background="url('./images/return-of-the-jedi-celebration.png')" -->

???

and that if we'd just MERGE the darn thing, we could have a giant party and not worry about what happens after merge for three decades or so until The Force Awakens came out.

---
<!-- .slide: class="center" -->

# &ldquo;Everyone!&rdquo;

???

And of course, it wasn't, really -- The highest-profile WP API projects had been the ones where we built out custom endpoints, custom data types, custom interfaces; this would be the sort of work we do at HumanMade, Alley, 10up, etc. These are exciting projects, but the implementations are domain-specific, only relevant within the client's organization.

---

> If this doesn’t end up in core, we’ll start rolling our own API for stuff. Others will too. Interoperability won’t be there
> 
> <small>~ [@joostdevalk](https://wordpress.slack.com/archives/core-restapi/p1476306524006688), Oct 12, 2016</small>

???

The most convincing argument was from plugin developers, who advocated for the API quite heavily throughout 2016. The writing was on the wall about needing access to WP data in JS, and if WP core didn't provide an opinion about how to model core content, each plugin would have to roll their own. Without a central authority, we'd end up with a big mess.

---

## Conditional Merge

**_And [Success Metrics](https://make.wordpress.org/core/2016/10/19/wordpress-rest-api-success-metrics/)_**

- Plugin utilization
- Distributed theme utilization
- Custom development implementations
- Core development and feature projects

???

We hadn't demonstrated what benefit this would have that would justify putting it onto a quarter of the web.

In the end we did get the go-ahead to merge the API into core, but it was conditional. We've got to broaden our usage and demonstrate the power of the REST API at scale.

---

## 5 years later

???

So, jumping back to today: I'm here to ask, how did it all go?

What have we learned? and, what do we still need to do?

---

> 6 core features or patches than can utilize the API, as well as 1 feature project, within three major releases.

## `¯\_(ツ)_/¯`

???

To start, one admission: we squeaked by on a technicality with these metrics, because Matt Mullenweg froze major WP releases after 4.9,

---
<!-- .slide: data-background-position="top" data-background-size="cover" data-background-repeat="no-repeat" data-background="url('./images/gutenberg.png')" -->

???

and 5.0 introduced the revolutionary new React-based "Gutenberg" editor, which is _entirely_ dependent on the API.

---

## What Worked

- Plugin usage
- Custom work in agencies / enterprise teams
- Laid the foundation for Gutenberg

---

> ...to me, it means "I can talk to WordPress, too."

<small>*~ [Ashley Kolodziej](https://twitter.com/ashleykolodziej), Boston University, [LoopConf 2018](https://www.youtube.com/watch?v=lUslM1aXjpo)*</small>

---

- Intro
- What did happen?
  - Some adoption in major plugins
  - Lots of custom work within agencies
  - Lowered barrier to some challenges within broader community
  - foundation for gutenberg
    - could be seen as an argument for having waited, but explain that coming first was critical
- New features
  - Missing endpoints
    - esp. search
  - Data modeling
  - Better JSON schema compliance
  - New resources for Gutenberg
  - Authentication, finally
- Biggest mistakes
  - Docs
    - Especially around best practices
  - Capabilities
    - WP's data model is vast, and our "compatibility layer" API didn't account for that
  - Not prioritizing auth
  - Versioning
    - Biggest single miss
- Next?
  - Better auth scoping
  - Could become more schema-driven, some day?
  - Time zones ;)
- Burnout
  - mixed signals from Leadership
    - I don't think matt was a good steward
  - Could use more maintainers, but not alone in that
    - Shout-out to Timothy, jonny, alain, felix, george, etc
  - G is taking more ownership though
- What's next?
  - 

---

# Access Levels & Authentication Scoping

???

One key area where we found what we'd built to be insufficient was around permissions and access.

The REST API by default exposes content which is public on a WP site, and you can gain access to additional resources by authenticating your request against a user account.

---

![Roles & Caps](/talks/2021/csvconf/images/roles-caps.png)

[Roles and Capabilities, wordpress.org/support](https://wordpress.org/support/article/roles-and-capabilities/)
[A deep dive into the roles and capabilities API (talk)](https://wordpress.tv/2017/06/02/john-blackbourn-a-deep-dive-into-the-roles-and-capabilities-api/)

???

User accounts have certain roles, but roles are composed of a more primitive indicator called a capability. Capabilities can vary by content, and can be modified at runtime; you may have access to some types of data but not others, or even to some posts and not others.

We did not account for this in the API, so we had to massage the output of our built in endpoints to ensure they behaved appropriately with different levels of access.

We also needed to expose capabilities to frontend applications, which we've implemented using JSON Hyper Schema's `targetSchema` paradigm.

---

# Versioning

`/wp/v2` for life ☹

???

One of the most foundational mistakes we made was around versioning. On merge we declared this API to be Version 2, to distinguish it from the "v1" used in the REST API plugin prior to merge, but none of our internal functions or filters acknowledge this parameter.

Without versioning being a core architectural concept, we'd have to almost fully reinvent the API infrastructure to add a v3 of any resource, and doing so would be a complete compat break with existing code and plugins. It isn't going to happen.

---

# GraphQL?

???

I don't fault Matt for advocating for GraphQL. It's a powerful and flexible type of API, and there's a number of things we do in WordPress today that would be simplified if we used a graph data model.

But REST provides a simplicity GraphQL doesn't have, and is a much easier solution for your average web developer. I think these APIs could complement each other if WP ever added GQL, rather than replace one another.

Practically speaking, too much of Gutenberg is authored with REST awareness for a full change to be economical. 
I believe it will be here at least until and unless WP goes through a paradigmatic change in its codebase

---

---

---

## Access Common Data

## Model Custom Data

??? And not only do the classes in 4.7 provide access to native WordPress data types: those classes also make it much easier than before to model custom data.

---

## What has changed?

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

#### ` 'show_in_rest' => true,`

## Room for Improvement

> ...to me, it means "I can talk to WordPress, too."

<small>*~ Ashley Kolodziej, LoopConf 2018*</small>

---

# Join Us!

## chat.wordpress.org

### `#core-restapi`

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


<img src="/talks/2018/wceu/images/hm-logo.png" style="margin-top: 0; height: 2em;" alt="Human Made Logo" />

???

Thank you for having me, and enjoy the rest of csv,conf!
