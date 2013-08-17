# Evolving your JavaScript with Backbone.js

WordCamp Providence, August 2013

K.Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)

Engineer at [Bocoup](http://bocoup.com/)


*At any time, hit "escape" to get an overview of all slides. This is a two-dimensional slide deck; Many slides have code examples available if you press "down."*



![Bob (Bocoup Logo)](images/bocoup-vertical-676.png)


![The Bocoup Family](images/bocoup-family.png)


![Open Source Web Technology](images/bocoup-tech-spread.png)


<small>(I've got stickers, if you're into that sort of thing)</small>



![Boston WordPress Logo](images/bostonwp.png)

[BostonWP](http://www.bostonwp.org) Co-Organizer



# I &hearts;<br/>PVD



## So. Who Are You Folks?



## WordPress & JavaScript

![wp heart](images/wp-hearts-js.png)



![JS Logo](images/js-logo.png)



![jQuery](images/jquery.png)



## @since 2.2.0

![Changeset 4816](images/changeset-4816.png)



2/3 of the scripts in script-loader.php<br />
define or depend on jQuery and its plugins

<small>(And many of the rest are legacy scripts like Prototype)</small>



# Why jQuery?



## Focus

Designed to [do specific things really well](http://jquery.com/#home-content):

* HTML document traversal
* Event handling
* Ajax interaction
* Animation



## Really good at this problem:

![Browser Logos](images/browser_logos-128.png)



# BUT



![Bowl of Spaghetti, from WikiMedia Commons](images/spaghetti.png)

jQuery files can get unwieldy



## jQuery does not enforce code
## structure in large applications




## WordPress is a large application



12.5% of the code shipped with WordPress is JS

![Language Statistics for WordPress, from Github](images/language-stats.png)

JS drives the most visible new user-facing features



## 3.3: Distraction-Free Writing
## 3.4: Theme Customizer
## 3.5: Media Manager
## 3.6: Revisions



> “I think [WordPress 3.5] actually signifies a shift from PHP land to JavaScript land for pretty much everything we’re going to do in the future”
>
> <small>~ WP 3.5 Lead Developer Andrew Nacin, [on WPCandy, Feb 4 2013](http://wpcandy.com/reports/a-shift-from-php-land-to-javascript-land/)</small>



## JS Needs within WordPress
## Have Changed



# Beyond jQuery



![Underscore.js logo](images/underscore.png)

![Backbone.js logo](images/backbone.png)



## Evolution, Not Revolution:

![Backbone uses jQuery](images/backbone-uses-jquery.png)



![The relationship between Backbone (for structure), Underscore (for utilities such as templating and functional programming constructs), and jQuery (for DOM manipulation and AJAX)](images/bb-underscore-jquery-trifecta.png)



## WordPress 3.5's Media re-write

> ...Backbone's models, collections, and views are pretty much exactly what we need to be able to make media work as awesome as we're aiming
>
> <small>~ nacin, [WordPress dev chat, 8/22/12](https://irclogs.wordpress.org/chanlog.php?channel=wordpress-dev&day=2012-08-22&sort=asc#m442360), re: [21390: Upload/Insert media revamp](http://core.trac.wordpress.org/ticket/21390)</small>



Backbone and Underscore<br />**are now shipped in Core**<br />for use within wp-admin


Better yet,

**Backbone.js 1.0**

ships with 3.6



## What is in core, may be enqueue'd



## So let's put these new libraries through their paces



![Underscore.js logo](images/underscore.png)



## What Is Underscore?

> Underscore is a **utility-belt library** for JavaScript that provides functional programming support without extending any of the built-in JavaScript objects.
>
> <small>*~ Adapted from [underscorejs.org](http://underscorejs.org)*</small>



> ... It's the tie to go along with jQuery's tux, and Backbone.js's suspenders.



## Collection Methods

Do things to groups of data



## Functional programming

Transform objects to make new ones

Manipulate functions to behave in new & useful ways



## General Utilities

Identity methods, Unique ID's & random numbers,

escaping strings, chaining...



![Screenshot of UnderscoreJS.org](images/underscore-website.png)

**More at [Underscorejs.org](http://underscorejs.org/#objects)**



## And then there's _.template



## Markup, the JavaScript Way

Write the template's markup in an easy-to-use, PHP-tag-like syntax, then compile it with `_.template` into something JavaScript interpreters can understand and optimize



```html
<div><%= mainContent %></div>
<a href="<%= link.url %>" title="<%- link.title %>">
  <%= link.text %>
</a>
```
*this* &uparrow; becomes *that* &downarrow;
```javascript
function(obj) {obj || (obj = {}); var __t, __p = '', __e = _.escape;
with (obj) { __p += '<div>' +((__t = ( mainContent )) == null ?
'' : __t) + '</div>\n<a href="' +((__t = ( link.url )) == null ?
'' : __t) + '" title="' +__e( link.title ) +'">\n  ' +
((__t = ( link.text )) == null ? '' : __t) +'\n</a>\n'; }
return __p};
```


Quick aside: If you render templates from PHP,

**use `<# #>` instead of `<% %>` to avoid conflicts**

with PHP's `asp_tags` (~5% of servers)



**MUCH** faster than building DOM nodes with jQuery

*(And easier to read, too!)*



![Underscore.js logo](images/underscore.png)

## That's one fine utility belt



## Underscore is the
## backbone of Backbone.js



# SO



![Backbone.js logo](images/backbone.png)



## What is Backbone?

> Backbone.js gives structure to web applications by providing **models** with key-value binding and custom events, **collections** [to group and manipulate those models], **views** with declarative event handling...
>
> <small>*~ Adapted from [backbonejs.org](http://backbonejs.org); emphasis added*</small>



## Separate Rendering from Logic

**Models** hold your data

**Views** render it on the page & handle user input



## Models

```javascript
var MyModelConstructor = Backbone.Model.extend({});

var modelInstance = new MyModelConstructor({
  prop1: 'some data',
  prop2: 'you want to store in a structured way'
});

console.log( modelInstance.get('prop1') ); // 'some data'
```



## Views

```javascript
var MyViewConstructor = Backbone.View.extend({
  el: '.my-view-container',
  render: function() {
    this.$el.html(
      this.model.get('prop1') + ' ' + this.model.get('prop2')
    );
    return this;
  }
});
var viewInstance = new MyViewConstructor({ model: modelInstance });
viewInstance.render();
// .my-view-container displays "some data that you want to
//                              store in a structured way"
```
Take that data, give it form



## That's a lot of boilerplate...

If you're used to "plain ol' JavaScript",
```javascript
var myData = {
  prop1: 'some data',
  prop2: 'you want to store in a *less* structured way'
};

$('.my-view-container').html( myData.prop1 + ' ' + myData.prop2 );
```
Backbone's *definitely* "more code"



# It's Worth It



## jQuery can't (as easily) do this:
```javascript
var MyViewConstructor = Backbone.View.extend({
  render: function() { /* ... */ },
  initialize: function() {
    // Re-render whenever the model changes!
    this.listenTo( this.model, 'change', this.render );
  }
});

// Other code...

modelInstance.set({
  'prop1': 'some NEW data'
});

// View now reads
// "some NEW data that you want to store in a structured way"
```
Your views can listen for changes in models,<br />
and automatically update themselves



## A little More Work Up Front
## ===
## Less Work Down the Road

The more structured your code is,

the easier it is to fix or modify



# Demo Time

We're going to take a small theme feature

and re-factor it to be awesome



## Homepage Image Gallery

![Image Gallery screenshot](images/gallery-demo-pvd.png)


[Gallery Code](https://github.com/kadamwhite/backbone-wordpress-demo/pull/7)



### Verdict:

![Screenshot showing page weight with naive PHP solution](images/page-weight-heavy.png)

### This feature Needs Improvement



# Step 1

Get the hidden Div's out of that DOM


![Screenshot showing reduced page weight](images/page-weight-light.png)


[Code for Step 1](https://github.com/kadamwhite/backbone-wordpress-demo/pull/8)



# Step 2

Get the rendering markup out of jQuery

and into a JavaScript template


[Step 2, Part 1: From jQuery to a Template](https://github.com/kadamwhite/backbone-wordpress-demo/pull/9)

[Step 2, Part 2: Pre-Compile the Template with Grunt](https://github.com/kadamwhite/backbone-wordpress-demo/pull/10)



# Step 3

Structure our featured image code with Backbone


[Code for Step 3](https://github.com/kadamwhite/backbone-wordpress-demo/pull/11)



# Step 4

Reorganize our .js files, for sanity and profit


[Code for Step 4](https://github.com/kadamwhite/backbone-wordpress-demo/pull/12)



# Step 5

Use Backbone for all the things!


[Code for Step 5](https://github.com/kadamwhite/backbone-wordpress-demo/pull/13)



The code for this demo is [available on Github](https://github.com/kadamwhite/backbone-wordpress-demo)

![Each step of the demo is broken down in a Pull Request, with appropriate comments](images/pr-demo-walkthrough.png)


### Demo Technology Colophon

![Grunt logo](images/grunt-logo.png)

with 10up's [grunt-wp-theme](https://github.com/10up/grunt-wp-theme) template



## Add Backbone to taste

Backbone is a useful way to structure JS code&mdash;

and you can use as little as you want



Or, you can go a bit crazy :)



## What Is Backbone?, Continued

> Backbone.js gives structure to web applications... and connects it all to your existing API over a **RESTful JSON interface**.



# Get Your Data
# from WP to JS



## WordPress as an API

WordPress serves your data

Backbone fetches that data, does stuff with it



# WordPress serves your data...



## JSON REST API

[wordpress.org/plugins/json-rest-api](http://wordpress.org/plugins/json-rest-api/)

-------

Google Summer of Code project by Ryan McCue

Works as a plugin, or as a core drop-in

Keep an eye on this one!



## JSON API plugin

[wordpress.org/plugins/json-api/](http://wordpress.org/plugins/json-api/)
```javascript
{
  "status": "ok",
  "count": 1,
  "count_total": 1,
  "pages": 1,
  "posts": [
    {
      "id": 1,
      "type": "post",
      "slug": "hello-world",
      "url": "http:\/\/localhost\/wordpress\/?p=1",
      "title": "Hello world!",
      "title_plain": "Hello world!",
      "content": "<p>Welcome to WordPress. This is your first post. Edit or delete it, then start blogging!<\/p>\n",
      "excerpt": "Welcome to WordPress. This is your first post. Edit or delete it, then start blogging!\n",
      "date": "2009-11-11 12:50:19",
      "modified": "2009-11-11 12:50:19",
      "categories": [],
      "tags": [],
      "author": {
        "id": 1,
        "slug": "admin",
        "name": "admin",
        "first_name": "",
        "last_name": "",
        "nickname": "",
        "url": "",
        "description": ""
      },
      "comments": [
        {
          "id": 1,
          "name": "Mr WordPress",
          "url": "http:\/\/wordpress.org\/",
          "date": "2009-11-11 12:50:19",
          "content": "<p>Hi, this is a comment.<br \/>To delete a comment, just log in and view the post's comments. There you will have the option to edit or delete them.<\/p>\n",
          "parent": 0
        }
      ],
      "comment_count": 1,
      "comment_status": "open"
    }
  ]
}
```



# ...Backbone fetches it



## .fetch()

```javascript
var Posts = Backbone.Collection.extend({
  model: Post, // constructor to use for items in this collection
  parse: function( response ) {
    return response.posts;
  }
});

var blogPosts = new Posts([], {
  url: '/api/get_recent_posts/'
});
```
Fetch posts from your blog (using the [JSON API](http://wordpress.org/plugins/json-api/) plugin)



## Demo: Theming
# Without the Loop

#### <br />*Mad Science for fun and profit*


```php
<article id="post-<%= get('id') %>" class="post-<%= get('id') %>
  type-<%= get('type') %> status-<%= get('status') %>
  <%= _.map( get('categories'),
    function( category ) {
      return 'category-' + category.slug;
    }
  ).join(' ') %>">
```



# In the Real World:



## Collections

![Screenshot of Collections theme demo site](images/collections-theme.png)

by [The Theme Foundry](http://thethemefoundry.com/wordpress/collections/)



## o2

![Header image of the geto2.com landing page](images/o2.png)

The successor to P2, by [Automattic](http://geto2.com/)<br />
<small>(not yet released)</small>



## Why stop at
## themes and plugins?



## Soundcloud &bull; Pandora &bull; AirBnB

## USA Today &bull; Khan Academy &bull; Rdio

## Newsblur &bull; Quarts &bull; Hulu &bull; Gawker

Backbone drives both website components<br />
and full-on web applications



You don't need to be *on* a webpage

to *use* data from that site



Access your blog using the WordPress.com REST API

![WordPress.com REST API documentation](images/wp-rest-api.png)



## Jetpack JSON API

![Jetpack JSON API announcement post](images/new-jetpack.png)

Use the WP.com API on self-hosted WordPress sites



## (provides a LOT more information)

```javascript
{
    "found": 2,
    "posts": [
        {
            "ID": 10,
            "author": {
                "ID": 275903,
                "email": false,
                "name": "K.Adam",
                "URL": "http:\/\/www.kadamwhite.com",
                "avatar_URL": "http:\/\/0.gravatar.com\/avatar\/6cd1cf6de05952505a165425efaf06b4?s=96&d=identicon&r=G",
                "profile_URL": "http:\/\/en.gravatar.com\/kadamwhite"
            },
            "date": "2012-08-27T20:06:06+00:00",
            "modified": "2012-08-27T20:06:06+00:00",
            "title": "The Cost of Privacy",
            "URL": "http:\/\/kadamwhite.wordpress.com\/2012\/08\/27\/the-cost-of-privacy\/",
            "short_URL": "http:\/\/wp.me\/p2GX8E-a",
            "content": "<p>Back in January, James Coglan wrote <a href=\"http:\/\/blog.jcoglan.com\/2012\/01\/19\/the-cost-of-privacy\/\">a great article about the drawbacks of private variables in JavaScript<\/a>. The hidden costs of encapsulating privately-scoped variables is explained with examples of some of the potential performance and maintenance drawbacks.<\/p>\n<blockquote><p>Encapsulation is something you get by deliberately designing interfaces and architectures, by communicating with your team\/users, and through documentation and tests. Trying to enforce it in code shows a level of paranoia that isn\u2019t necessary in most situations, and this code style has plenty of costs that grossly offset the minimal encapsulation benefit it provides.<\/p><\/blockquote>\n<p>(Link via <a href=\"http:\/\/rmurphey.com\/\">Rebecca Murphey<\/a>)<\/p>\n",
            "excerpt": "<p>Back in January, James Coglan wrote a great article about the drawbacks of private variables in JavaScript. The hidden costs of encapsulating privately-scoped variables is explained with examples of some of the potential performance and maintenance drawbacks. Encapsulation is something you get by deliberately designing interfaces and architectures, by communicating with your team\/users, and through [&hellip;]<\/p>\n",
            "slug": "the-cost-of-privacy",
            "status": "publish",
            "password": "",
            "parent": false,
            "type": "post",
            "comments_open": true,
            "pings_open": true,
            "comment_count": 0,
            "like_count": 0,
            "i_like": 0,
            "is_reblogged": 0,
            "is_following": 0,
            "featured_image": "",
            "format": "standard",
            "geo": false,
            "publicize_URLs": [

            ],
            "tags": {
                "Design Patterns": {
                    "name": "Design Patterns",
                    "slug": "design-patterns",
                    "description": "",
                    "post_count": 1,
                    "meta": {
                        "links": {
                            "self": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/tags\/slug:design-patterns",
                            "help": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/tags\/slug:design-patterns\/help",
                            "site": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780"
                        }
                    }
                },
                "Front-End Architecture": {
                    "name": "Front-End Architecture",
                    "slug": "front-end-architecture",
                    "description": "",
                    "post_count": 2,
                    "meta": {
                        "links": {
                            "self": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/tags\/slug:front-end-architecture",
                            "help": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/tags\/slug:front-end-architecture\/help",
                            "site": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780"
                        }
                    }
                },
                "JavaScript": {
                    "name": "JavaScript",
                    "slug": "javascript",
                    "description": "",
                    "post_count": 2,
                    "meta": {
                        "links": {
                            "self": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/tags\/slug:javascript",
                            "help": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/tags\/slug:javascript\/help",
                            "site": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780"
                        }
                    }
                },
                "Scope": {
                    "name": "Scope",
                    "slug": "scope",
                    "description": "",
                    "post_count": 1,
                    "meta": {
                        "links": {
                            "self": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/tags\/slug:scope",
                            "help": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/tags\/slug:scope\/help",
                            "site": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780"
                        }
                    }
                }
            },
            "categories": {
                "JavaScript": {
                    "name": "JavaScript",
                    "slug": "javascript",
                    "description": "",
                    "post_count": 2,
                    "parent": 0,
                    "meta": {
                        "links": {
                            "self": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/categories\/slug:javascript",
                            "help": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/categories\/slug:javascript\/help",
                            "site": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780"
                        }
                    }
                }
            },
            "attachments": {

            },
            "metadata": false,
            "meta": {
                "links": {
                    "self": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/posts\/10",
                    "help": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/posts\/10\/help",
                    "site": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780",
                    "replies": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/posts\/10\/replies\/",
                    "likes": "http:\/\/public-api.wordpress.com\/rest\/v1\/sites\/39789780\/posts\/10\/likes\/"
                }
            }
        }
    ]
}
```



## Demo:
# Blog Viewer


### We are going to build this with
# BUZZWORDS


## BOOTSTRAP

*and*

## STRANGELY ABSENT VOWELS

*and of course*

## BACKBONE



![PostListr app screenshot](images/post-listr.png)

[code](https://github.com/kadamwhite/wordbone-pressback/tree/master/PostListr#postlistr) & [live application](http://kadamwhite.github.io/wordbone-pressback/)



## Where do we go from here?



> #### There's More Than One Way To Do It 
> It's common for folks just getting started to treat the examples listed on this page as some sort of gospel truth. In fact, Backbone.js is intended to be fairly agnostic about many common patterns in client-side code.
>
> <small>~ [Backbonejs.org](http://backbonejs.org/#FAQ-tim-toady)</small>



## Backbone is the right
## choice for WordPress



![Nacin, indicating "I was right!" about choosing Backbone for media](images/i-was-right.jpg)

&ldquo;I was right!&rdquo;



### It's not going anywhere



### It's not scary



### It's easy to get started



# Experiment!



# Thank You

<br />

Slides: [talks.kadamwhite.com/wcpvd13](http://kadamwhite.github.io/talks/2013/backbone-wordpress)

Code: [github.com/kadamwhite/wordbone-pressback/](https://github.com/kadamwhite/wordbone-pressback/#readme)

Me: [@kadamwhite](http://twitter.com/kadamwhite) &bull; [kadamwhite.com](http://www.kadamwhite.com)

<br />

*Artwork by [Emily Garfield](http://www.emilygarfield.com) and [Judith Klausner](http://jgklausner.com/)*

<hr />

<small>Technology: [Reveal.js](http://lab.hakim.se/reveal-js/) &bull; [Grunt](http://gruntjs.com/) &bull; [Grunt-WP-Theme](https://github.com/10up/grunt-wp-theme)</small>

<small>*PS: I have Backbone, Grunt, JS, and Bocoup stickers!*</small>



## Resources & Further Reading

* Highly Recommended:
  * [Backbone.js Website](http://backbonejs.org/) and [annotated source code](http://backbonejs.org/docs/backbone.html)
  * [Backbone.js Deconstructed](http://tech.pro/tutorial/1367/part-1-backbonejs-deconstructed) on tech.pro
  * [Bocoup Training](http://training.bocoup.com/)
  * [Step by Step from jQuery to Backbone](https://github.com/kjbekkelund/writings/blob/master/published/understanding-backbone.md) on Github
* Also potentially Useful:
  * [WP Tuts+ tutorial on Backbone and WordPress](http://wp.tutsplus.com/tutorials/creative-coding/using-backbone-within-the-wordpress-admin-the-back-end/)
  * Function Programming/Currying: [Functional Programming in 5 Minutes](http://slid.es/gsklee/functional-programming-in-5-minutes)
* Completely un-vetted:
  * [Backbone.js Tips And Patterns](http://coding.smashingmagazine.com/2013/08/09/backbone-js-tips-patterns/)