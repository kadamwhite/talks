# WordPress in  
# Weird Places,
*or*

&ldquo;How to Content Manage a Node App with PHP&rdquo;
<br><br>
K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite) &bull; [@Bocoup](http://bocoup.com)



![Bob (Bocoup Logo)](../../2013/backbone-wordpress/images/bocoup-vertical-676.png)



<!-- .slide: data-background="images/sf-clouds.jpg" -->
### Unorthodox Solution,
## Common Problem

Note: This talk is about a solution to a problem, but the problem is not new. In January my team started building an application for a new business unit for a fortune-50 company. As it was a new business unit, it was a fresh build: there would be no integration with the parent company's existing systems. How do you pick your technology for a green-field project?



![Node.js logo](images/node-logo.png)

![Postgresql Logo](images/postgresql-logo.png)

Note: We chose node and Postgres, because we have experience with them and know Node to be a flexible tool



## What is the best Node.js CMS?

Note: A site needs a good CMS. But what are our options in Node?




![Mario Kart 64 item selection spinner](images/mario-kart-item-spinner.gif)

Note: We evaluated a lot of existing choices, looking for something that would provide the editing interface, usability, and data structures we needed



![WordPress logo](images/wordpress-logo-simplified-rgb.png)

Note: We ended up choosing WordPress



How?
# WP-API Project



## CMS as API

[github.com/WP-API/WP-API](https://github.com/WP-API/WP-API)

Note: The API is changing the way we think about WordPress. It makes it *easy* (unlike XMLRPC) to use WP data in other places



# WordPress
### as Monolith?

Note: WP has been a single unit: You build on top of it with plugins and themes. You can change things internally by plugging in, but generally you'll be using most or all of the parts, such as templating and routing.



# WordPress
### as Components

Note: There are many individual components within WordPress that you may or may not need



# WordPress
### as *Data Store* and *Editing Interface*
Note: we can pick-and-choose what we use



# Node

### provides the *Routing* and *Templating*

Note: We can use Express and Handlebars (or any templating option) on the Node side



## Something's Missing:

route &rarr; **data** &rarr; template



# Data Access

<br> 
`npm install --save wordpress-rest-api`

<br>

<small>[wordpress-rest-api](https://github.com/kadamwhite/wordpress-rest-api) on Github</small>

Note: We wrote and released an NPM package that consumes the API. There are other NPM packages for XMLRPC, and the .com API.



## Query Builder for the WP-API:
```javascript
    var WPClient = require( 'wordpress-rest-api' );
    var wp = new WPClient({ endpoint: 'http://mysite.com/wp-json' });

    wp.posts().then(function( posts ) {
        console.log( posts );
    });

    wp.posts()
      .type( 'my_cpt' )
      .tag( 'wordcamp' )
      .then(function( posts ) { /* ... */ });
```



## Putting It Together:
```javascript
    router.get( '/posts/:slug', function( req, res, next ) {
      // Search for the post with this slug
      var post = wp.posts().name( req.params.slug );

      post.then(function( posts ) {
        if ( ! posts.length ) {
          return next(); // 404
        }

        var context = _.first( posts );
        res.render( 'single', context );
      });
    });
```
Note: IDs have no meaning outside of WP: slugs are more meaningful.



## Rendering

*Not that different from `<?php the_title(); ?>`*
<code><pre>
    <h1>{{{post.title}}}</h1>
    <p class="light secondary byline no-margin">
      <span class="pencil-icon"></span>
      by <a href="/library/author/{{post.author.username}}">
        {{post.author.name}}
      </a> on {{formatArticleDate post.date}}
    </p>
</pre></code>
<small>*[Handlebars](http://handlebarsjs.com/), or [Combyne](https://github.com/tbranyen/combyne), or [Nunjucks](http://mozilla.github.io/nunjucks)...*</small>



### Sample Implementation:
## &ldquo;ExpressPress&rdquo;

[github.com/kadamwhite/expresspress](https://github.com/kadamwhite/expresspress)



<!-- .slide: data-background="images/sf-clouds.jpg" -->
# What Worked



## External Content

Note: Clear separation between our application and the WP data source helped us structure our code better. Content coming from a JSON pipe was actually cleaner than integrating/building on top of an existing CMS would be.



## The Best UI

Note: we avoided having to reinvent a content editing interface, and our clients got an easy-to-use and robust article management tool. With plugins, can add editorial workflows, etc: all the usual editing benefits



## Media Management

Note: WP provides a great way to upload and manage media, integrated right into the editing interface: and this is going to get better. We actually use WordPress for managing non-article images too, since it's straightforward.



## &ldquo;Private&rdquo;

Note: I mean this as opposed to public-facing: Image URLs are the only way you'd know our CMS server exists, as a site visitor. If we uploaded them to S3, WP would be entirely invisible to the outside world. You could even have WP running within a local network.



<!-- .slide: data-background="images/sf-clouds.jpg" -->
# Rough Edges



## PHP !== JS

Note: We have a PHP CMS, an Ember.js internal tool, an express public app, and another external API in Ruby on Rails, all in one project: good luck hiring for that.



### It Would Have Been Worse

with a different CMS

Note: training new developers would have been additional overhead. WP is widely known, and stable, unlike younger Node CMS options. Also, managed WP hosts saved us a lot of devops time. S3, etc would improve even more



## External Point of Failure

Note: A CMS as an API introduces another point of failure: WP is one more thing to load-balance and failover; but this is mitigated by the stability of the platform 



### Cache That Content

(and   use a managed host)

Note: an intelligent caching layer saves some of the burden on the CMS, and it could be even more robust: imagine caching everything in one go, then using a plugin in WP that calls out to your application whenever content changes, to invalidate the cached versions. The duplication of content in two DBs pales in comparison to the simplicity of using WP as a self-contained admin console.



## API Growing Pains

*0.9 is a pretty lonely number, too...*

Note: We began our build before 1.0: we had to track the project as it evolves. On the plus side, we found several issues!



## Authentication & Pagination

Works, but unsatisfying

Note: Basic Auth is too simplistic, and OAuth is complex. We worked around this by filtering existing data and making custom endpoints to serve "private" content, but that only worked because we were read-only from WP. Where things get interesting is when you read-write. Pagination, on the other hand, is just not available for some types of queries: e.g. WP_User_Query doesn't permit pagination, and the way in which it is exposed needs some love



## That &ldquo;Best UI&rdquo;...

!["View Post" link: one of many](images/view-post-link.png)

Note: WP's UI is comprehensive, but tightly integrated. Just start counting the number of UI elements that assume you're using WordPress-native routes and templating... there are *many*. We had to work around a lot with a custom plugin. Lots of work to be done to make the interface more flexible to this kind of "abuse."



## Structured Content

We need better tools in core

*(for now, we used Pods)*

Note: The WP and Node codebases had to be highly synchronized: migrating back to older versions without in-code field definitions is very difficult. Can't wait for that Custom Meta UI project!



<!-- .slide: data-background="images/sf-clouds.jpg" -->
## Was It Worth It?



<!-- .slide: data-background="images/sf-clouds.jpg" -->
# Yes



## What We Gained

Stability, clean separation, usability



## Rough Edges Were Manageable

Note: between the content service module within our app, the node module itself, and a plugin on the WordPress side, we were able to do everythign we wanted to do. Even if it took lots of UI hacks to make the editor experience reasonable!



# Looking Forward

Note: When this hits core, we will get 2 things:



### Plugin interfaces can evolve

to live within *or* alongside WP

Note: Plugins will range from the traditional model, all the way to a single-page app served in an iframe within the admin that uses the API for all of its data, or even an external service that uses the plugin to customize its communication with your WP install. Custom interfaces for every need are possible.



## WordPress can evolve




### What if

*the dashboard was built on top of the API?*

Note: WP's interface itself can, and may, and possibly should, be reinvisioned as a single page application built on top of this kind of API.



### What if

*it was one of* many *core applications?*

Note: but why stop there? Rather than one monolithic dashboard, we could have a host of interlocking modular applications that make up an ecosystem that is WordPress, with the API as Common Interface



### until then,



# Let's see what
# we can build!

Note: The project is a success, and works as a proof-of-concept: For some use cases, WP is an excellent solution for node. And whether or not the future plays out the way we see it, the API makes WP a relevant contender in tons of different environments, and we're excited to see what everybody else does in their own languages and environments of choice.



<!-- .slide: data-background="images/sf-clouds.jpg" -->
## Thank You!

&nbsp;

Slides: [talks.kadamwhite.com/wcsf](http://kadamwhite.github.io/talks/2014/wcsf-node-wp)

Demo: [github.com/kadamwhite/expresspress](https://github.com/kadamwhite/expresspress)

API Client: [npmjs.org/package/wordpress-rest-api](https://www.npmjs.org/package/wordpress-rest-api)

---------

Me: [kadamwhite.com](http://kadamwhite.com) &bull; [@kadamwhite](http://twitter.com/kadamwhite)

Us: [Bocoup.com](http://bocoup.com) &bull; [@bocoup](http://twitter.com/bocoup)
