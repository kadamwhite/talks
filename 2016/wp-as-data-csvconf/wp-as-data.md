<!-- .slide: class="lurking-bob" -->

# WordPress
# As Data

<br>

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite) &bull; [Bocoup](https://bocoup.com)

??? My name is K Adam White, I'm a lead engineer at Bocoup, a tech & design consultancy based over in Boston.

Excited for the rest of this event b/c we do design/datavis, but here today to share some of the work that's been going on recently to make it easier to work with WordPress data.

---

![WordPress Logo](./images/wp-logo-large.png)

??? WP is the most widespread web content management system in the world, at last count powering about 26% of the top ten million sites (w3techs.com).

Not bad for 13 year old software!

What started as a fork of b2/cafelog intended for "personal publishing" is now used by magazines, writers, academic institutions, photographers, enterprise companies, poets, tech bloggers...

---
<!-- .slide: data-background="url('./images/wp_posts-columns.png')" data-state="solid-bg" -->

??? Most people think of WP in those terms; in terms of publishing, writing, _content_. But of course content is stored in a database for a reason, content _is_ data

That makes WP one of the most widespread storage mechanisms for data in the world, especially deliberately authored personal data meant for public consumption ("content")

---
<!-- .slide: data-background="url('./images/new-post-editor.jpg')" data-state="semi-solid-bg" class="center" -->

<h2 class="whitebg">&ldquo;Posts&rdquo;&hellip;</h2>

??? Its personal publishing origins make the "post" the default unit of granular data in WordPress, but a host of tools are available to define your own "post types" and provide more complex data structures

---

![screenshot of post types defined on dentedreality.com.au](images/beau-wp-import-types.png)

<small>[dentedreality.com.au](http://dentedreality.com.au/)</small>

??? Because WP is permissively licensed, frequently deployed upon a user's own server, and not prescriptive of what type of data it is used to store, WordPress has come to be used as an arbitrary personal data store

My friend Beau Lebens from Automattic, the parent company of WordPress.com, uses it to back up anything he publishes to other platforms and social networks; this is not a common use-case necessarily but it is not unique

---

## Change This Slide

> WordPress's code is badly designed and written in a language that I no longer believe serves the best interests of the Internet in general

> PHP is&hellip; a collection of hacks more than a language

<small>~ [grumpy ycombinator comments](https://news.ycombinator.com/item?id=9548674)</small>

??? WP's success means it must be doing something right&mdash;but of course WP does not have a reputation for excellent developer ergonomics.

It still takes a lot of effort to get data into or out of WP, which has fueled a lot of recent work around improving WP's built-in APIs

---
<!-- .slide: data-background="url('./images/xmlrpc-codex.png')" class="center" -->

<div class="whitebg">
  <h2><small>In The Beginning</small><br>
  There Was XML-RPC</h2>
</div>

??? The primary "WordPress API" currently available is the XML-RPC API, which is how the WordPress mobile app can talk to your site. But this is not a fun API to work with.

I've heard that about 40% of the code in the mobile app goes JUST to encoding/decoding XML, that's not good overhead

---
<!-- .slide: data-background="url('./images/wpdotcom-api-docs.png')" class="center" -->

<div class="whitebg">
  <h2>WordPress.com API</h2>

  [developer.wordpress.com/docs/api](https://developer.wordpress.com/docs/api/)
</div>

??? WordPress.com started providing a REST API a few years back, and you can use it with an independent WP site by installing the Jetpack plugin; but this depends on leveraging Automattic's wordpress.com infrastructure, and isn't "built in"

(WP.com and WP the software are related by separate)

---
<!-- .slide: class="center" -->

![WordPress REST API Project Logo](./images/wp-api-logo.jpg)
[v2.wp-api.org](http://v2.wp-api.org/)

??? So most recently, I've been involved with a project to build a canonical, modern, JSON-based HTTP REST API to WordPress, a project started by an Australian developer named Ryan McCue in 2013 through Google Summer of Code.

---

## &hellip;So?

Why yet another API?

??? The reason this is exciting is that this plugin is being built with the intent of merging this API into WordPress core, which would give WP users unprecedented access to their content

---

`yoursite.com/wp-json/wp/v2`
```
{
  "namespace": "wp/v2",
  "routes": {
    "/wp/v2": {},
    "/wp/v2/posts": {},
    "/wp/v2/posts/(?P<id>[\\d]+)": {},
    "/wp/v2/posts/(?P<parent>[\\d]+)/revisions": {},
    "/wp/v2/posts/(?P<parent>[\\d]+)/revisions/(?P<id>[\\d]+)": {},
    "/wp/v2/pages": {},
    "/wp/v2/pages/(?P<id>[\\d]+)": {},
    "/wp/v2/pages/(?P<parent>[\\d]+)/revisions": {},
    "/wp/v2/pages/(?P<parent>[\\d]+)/revisions/(?P<id>[\\d]+)": {},
    "/wp/v2/media": {},
    "/wp/v2/media/(?P<id>[\\d]+)": {},
    "/wp/v2/types": {},
    "/wp/v2/types/(?P<type>[\\w-]+)": {},
    "/wp/v2/statuses": {},
    "/wp/v2/statuses/(?P<status>[\\w-]+)": {},
    "/wp/v2/taxonomies": {},
    "/wp/v2/taxonomies/(?P<taxonomy>[\\w-]+)": {},
    "/wp/v2/categories": {},
    "/wp/v2/categories/(?P<id>[\\d]+)": {},
    "/wp/v2/tags": {},
    "/wp/v2/tags/(?P<id>[\\d]+)": {},
    "/wp/v2/users": {},
    "/wp/v2/users/(?P<id>[\\d]+)": {},
    "/wp/v2/users/me": {},
    "/wp/v2/comments": {},
    "/wp/v2/comments/(?P<id>[\\d]+)": {}
  },
  "_links": {}
}
```
<!-- .element: class="stretch" -->

??? This is the endpoint list you get when you hit the root endpoint for the plugin's built-in resources, which represent the core WordPress types and taxonomies.

---
<!-- .slide: data-background="url('./images/blog-post.jpg')" class="center" -->

`/wp-json/wp/v2/posts/2452` <!-- .element: class="whitebg" -->
```
{
  "id": 2452,
  "date": "2016-02-22T12:18:31",
  "date_gmt": "2016-02-22T12:18:31",
  "guid": {
    "rendered": "https://bocoup.com/?p=2452"
  },
  "modified": "2016-02-22T18:02:18",
  "modified_gmt": "2016-02-22T18:02:18",
  "slug": "say-hello-world-with-johnny-five-on-tessel-2",
  "type": "post",
  "link": "http://website.loc/weblog/say-hello-world-with-johnny-five-on-tessel-2",
  "title": {
    "rendered": "Say &#8220;Hello World&#8221; with Johnny-Five on Tessel 2"
  },
  "content": {
    "rendered": "<p>Back in April I wrote about Bocoup&#8217;s excitement..."
  },
  "excerpt": {
    "rendered": "Back in April I wrote about Bocoup&#8217;s excitement..."
  },
  "author": 5,
  "featured_media": 0,
  "comment_status": "open",
  "ping_status": "closed",
  "sticky": false,
  "format": "standard",
  "categories": [ 407, 243 ],
  "tags": [ 60, 456 ],
  "_links": {
    "self": [{
      "href": "http://website.loc/wp-json/wp/v2/posts/2452"
    }],
    "collection": [{
      "href": "http://website.loc/wp-json/wp/v2/posts"
    }],
    "about": [{
      "href": "http://website.loc/wp-json/wp/v2/types/post"
    }],
    "author": [{
      "embeddable": true,
      "href": "http://website.loc/wp-json/wp/v2/users/5"
    }],
    "replies": [{
      "embeddable": true,
      "href": "http://website.loc/wp-json/wp/v2/comments?post=2452"
    }],
    "version-history": [{
      "href": "http://website.loc/wp-json/wp/v2/posts/2452/revisions"
    }],
    "https://api.w.org/attachment": [{
      "href": "http://website.loc/wp-json/wp/v2/media?parent=2452"
    }],
    "https://api.w.org/term": [{
      "taxonomy": "category",
      "embeddable": true,
      "href": "http://website.loc/wp-json/wp/v2/categories?post=2452"
    }, {
      "taxonomy": "post_tag",
      "embeddable": true,
      "href": "http://website.loc/wp-json/wp/v2/tags?post=2452"
    }]
  }
}
```
<!-- .element class="stretch" -->

---
<!-- .slide: class="center" -->

Code using the [`wordpress-rest-api` package](https://www.npmjs.com/package/wordpress-rest-api) on NPM:
```
var WP = require('wordpress-rest-api');
var site = new WP({ endpoint: 'your-site.com/wp-json' });

site.posts().get().then(function(posts) {
  posts.forEach(function(post) {
    console.log(post.content.rendered);
  });
});
```

??? In the course of our consulting work I wrote a Node client for this API which works on the server or in browser; PHP, Go, Ruby, Angular.js and Backbone.js client libraries also exist

---
<!-- .slide: class="center" -->

Query Interface
```
/wp-json/wp/v2/posts?filter[author_name]=kadam
    &filter[tag]=art+digital-art
    &filter[year]=2014
    &search=Chelsea
```

```js
var query = site.posts()
    .author( 'kadam' )
    .tags([ 'art', 'digital-art' ])
    .year( 2014 )
    .search( 'Chelsea' );
```

??? If you don't know the ID of the post you want, you can query for it -- most of these clients provide an interface to simplify the process of building out the query and filter parameters

Our JS client uses a chaining syntax.

---

**Create**
```javascript
var prom = wp.posts().auth( credentials ).post({
    title: 'New Post 2501',
    content: 'Some Content'
}).then(function( createdPost ) {
    console.log( 'post created with ID ' + createdPost.id );
});
```
**Update**
```javascript
return wp.posts().auth( credentials ).id( id ).put({
    title: 'Updated Title'
});
```
**Delete**
```javascript
wp.posts().auth( credentials ).id( id ).delete();
```

??? While authentication handling is still one of the roughest edges of this plugin -- OAuth 2.0 is out for many sites since it requires SSL, while WP itself does not -- once you are authenticated you can of course create, update and delete resources as well.

---
<!-- .slide: class="center" -->

## Extending the API

[Add Custom Routes](http://v2.wp-api.org/extending/adding/) to expose new resources

(or new views of existing information),

or [define custom content types](http://v2.wp-api.org/extending/custom-content-types/) that can be accessed via the API.

??? And those resources don't have to be limited to the default WordPress types.

WordPress is still a PHP application, of course, so there's a little bit of legwork to do to create endpoints for your own custom resources -- but it's mostly boilerplate. I've linked to it here rather than going through it in depth.

---
<!-- .slide: class="center" -->

## Who Benefits?

??? I show you bespoke uses of WordPress as a data archive that are only possible for experienced developers, then share an API, the very name of which indicates this isn't a tool for the end user either.

But users can and will benefit from what developers do with this API.

---
<!-- .slide: data-background="url('../wp-node-feelingrestful/images/calypso-site-screenshot.png')" class="center" -->

<div class="whitebg">

<h2>Next-Gen Editing Interfaces</h2>

</div>

??? Last year Automattic launched the new WordPress.com admin UI, "Calypso," one example of the new interfaces that can be built once a standard API is in place.

The .com team have asserted that if and when this plugin rolls into core, the WordPress.com API will be merged, reducing fragmentation across the ecosystem.

---
<!-- .slide: data-background="url('../wp-node-feelingrestful/images/2014-project-wp-data-flow.svg')" data-state="solid-bg" -->

??? At Bocoup I've used WordPress as the editing interface UI for non-PHP applications

Our clients' editorial team got the best of its battle-hardened editorial UI, while we flowed their copy and images into Node and Ember applications.

Their writers and editor loved the flexibility of the WP Admin, and we spent much less time iterating on this architecture than we did on the rest of our integrations!

---
<!-- .slide: data-background="url('./images/csv-data-load.svg')" data-state="solid-bg" -->

## Bulk Data Load

??? Bulk Data Load also gets a lot easier: we've used the WP API as a way to bulk load data into WP. On a recent project it let us take a bucket of CSV files and get all that data into our system in an afternoon; content import used to be a fairly fraught process!

That data was visualized on dashboards running on that site: win for their team, same system. Could do the same with Analytics, text vis.

---

## Machine Learning&hellip;?

Generated from [Bocoup blog copy](https://bocoup.com/weblog) using [torch-rnn](https://github.com/jcjohnson/torch-rnn):
<blockquote class="full-width">
  <p>GitHub is pretty scripts used to make more, free when we now we can also up, we present. We can active connections, but that's the engineering test, code like hardware: CodePen. The hardware of callback!</p>
  <p>There is an incredibly exciting command.</p>
</blockquote>

??? I am super new to this specifically but machine learning was a theme of our OpenVis Conf event last week, so over the weekend I experimented with spidering our own company blog through the API and using that data to train a recurrent neural network:

I could imagine a world in which our sites are capable of manufacturing vacuous filler content entirely on their own, maintaining our own voice in the process; or at least a world in which our sites can make up headlines for us as writing prompts!

---
<!-- .slide: data-background="url('../wp-node-feelingrestful/images/2014-project-architecture.svg')" data-state="semi-solid-bg" -->

### WP as _Component_
<!-- .element: class="whitebg" -->

??? With a robust, modern API WP doesn't need to be a monolithic platform, it doesn't need to be the core of our project -- it can be a component, something we use for its strengths when we need to.

It can supplement or replace other data stores, or it can be an intermediary that passes its data off to another system.

---

### Remaining Hurdles:

## Authentication, Discovery

??? There's still some rough edges; I mentioned authentication, but we also have no global discovery mechanism the way we do with wordpress.com (where the API is synonymous with the directory of sites).

We can detect if a given site is providing this API, but we cannot necessarily search through all API-enabled sites, since they're so distributed. Not really a weakness, just the state of affairs.

---

## WP API Roadmap

- [v2.0 Plugin to be Released Soon](https://make.wordpress.org/core/2016/04/04/wp-rest-api-2-0-beta-13-roadmap/)
- Plugin will be proposed for core merge in late 2016

??? The API team is talking through these questions and releasing beta versions of the API v2 plugin, which should get a stable release soon.

Our current plan is to propose that this plugin be merged into core in late 2016.

Some argument from Automattic, who are focused on the "new UI" use-case, that it won't merge until full feature parity: I hope it'll go in sooner b/c you can do a LOT with it today.

---

## We need your help!

What do you need for this to be useful to _you?_

Kick tires, file bugs.

??? So for us to get this thing off the ground, we need testers and implementers more than anything. Every new site I've used the API on has turned up bugs in the API itself or in my client library; we need more people kicking these tires before we're comfortable unleashing it on a quarter of the internet!

---

# Types
## of API Project

*(home stretch)*

??? The API suits itself to two very different type of project, and we need more examples of both.

---

### API Projects can be

## Custom & Specific,

??? The first type is the bespoke system, like the work we do at Bocoup that is highly tailored for an individual client.

---

### or API Projects can be

## Generic & Broad

??? Something like Calypso goes the opposite direction, and served a broad variety of sites by utilizing solely the built-in API functionality.

Generic clients have broad applicability, but fewer capabilities; specific clients have very narrow applicability, and limitless capabilities.

---

### Broad Applications

(may) benefit users the most.

??? Projects written against this out-of-the-box API are where we have the most opportunity to impact how WordPress users see their content and understand the data they are generating.

There was a lot of FUD about RSS when it was first released: people have access to my content without my permission! Ah! We may go through the same phase with this API, but I turn to the csv,conf community for help understanding how we can communicate the benefits to our users without making them blind to the continued need for them to be diligent about licensing and protecting their content accordingly.

---

## *Thank You*

<hr>

Slides: [**talks.kadamwhite.com/wp-as-data**](http://talks.kadamwhite.com/wp-as-data)

Me: [@kadamwhite](https://twitter.com/kadamwhite)

Us: [bocoup.com](https://bocoup.com)

<hr>

API Project Home: [github.com/WP-API/WP-API](https://github.com/WP-API/WP-API)

[npmjs.com/package/**wordpress-rest-api**](https://npmjs.com/package/wordpress-rest-api)

