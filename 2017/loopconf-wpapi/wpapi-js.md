<br>

## Build Your Dreams
### with the
## WordPress REST API
#### and
## JavaScript

<br>

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite) &bull; [Bocoup](https://bocoup.com)

??? My name is K Adam White, I'm a senior engineer at Bocoup, a technology & design consultancy based over in Boston.

--

[![Bocoup logo](../../common/images/bocoup-vertical-676.png)](https://www.bocoup.com)

---

![WordPress Logo](../../2016/wp-as-data-csvconf/images/wp-logo-large.png)

??? I pitched this talk in the spring of 2016. "build your dreams" was campaign trail talk. Then the merge happened, so I needed a new topic!

We'll get to JavaScript, but I wanted to share my side of the history of how the REST API came to be merged, because I think it's a story we can learn from.

---

![WordPress Logo](../../2016/wp-as-data-csvconf/images/wp-logo-large.png)

??? In 2014, three years ago this week, we were working with a world class design agency to build am application for a fortune-500 financial company. We couldn't find a sufficiently mature Node CMS, but I'd been watching the API develop and I talked our team into trying it out as a POC.

---
<!-- .slide: data-background="url('../../2016/wp-node-feelingrestful/images/2014-project-architecture.svg')" data-state="semi-solid-bg" -->

### WP as _Component_
<!-- .element: class="whitebg" -->

??? It worked, and our clients' editorial team got the best of its battle-hardened interface, while we flowed their copy and images into the modern Node and SPA applications we were creating. No PHP templating!

Their writers and editor loved the flexibility of the WP Admin, and we spent much less time iterating on this architecture than we did on the rest of our integrations.

---

<!-- .slide: data-background="url('../../2016/wp-node-feelingrestful/images/2014-project-wp-data-flow.svg')" data-state="solid-bg" -->

??? So Bocoup's been using WordPress in our client projects for three years, specifically because of the REST API. We work on complex applications composed of many parts and services, and the REST API makes WordPress something we can use as a strategic component, not a monolithic platform.

Something we can use exclusively for its strengths, such as its maturity as a content editing tool. *We* here know it isn't perfect, but writers don't want to learn Markdown, and they shouldn't have to!

---
<!-- .slide: data-background="url('../../2016/wp-as-data-csvconf/images/csv-data-load.svg')" data-state="solid-bg" -->

??? The API's also helped us when we did take on projects built solidly on top of the WP platform: bootstrapping a site's data from hundreds of spreadsheets becomes the work of a single afternoon with a few lines of script code.

Getting that data back out into data dashboards is similarly straightforward.

---
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

This will provide direct improvements to our users, and also provide reference implementations for plugin developers and future core enhancements.

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

### A React Journaling Application
## In 10 Minutes

??? You got the React intro yesterday, so I'll just open with a brief overview of the "wpapi" NPM module that makes it easier to query the REST API.

---

### `npm install wpapi`

```js
var site = new WPAPI({
  endpoint: 'http://your-domain.com/wp-json'
});

// Get most recent 20 posts, as a Promise
site.posts().perPage( 20 )
  .then(function( posts ) { /* posts! */ });

// Get a page of comments submitted before March 31, 2016
site.comments().before( '2016-03-31' )
  .then(function( comments ) { /* discourse! */ });
```

??? wpapi is not required to use the REST API; you can use the Backbone client library, or just use jQuery or fetch to make direct requests. But we created a chaining syntax inspired by jQuery's to make it easy to request specific resources.

---

### `npm install wpapi`

```js
// Get all posts in the tags with ID 37 or 42
// wp-json/wp/v2/posts?tags[]=37&tags[]=42
site.posts().tags([37, 42]).then(function(posts) {
  console.log(posts);
});

// Get posts in the category with slugs "news" or "art"
Promise.all([
  site.categories().slug('news').get(),
  site.categories().slug('art').get(),
])
  .then(function(cats) {
    var ids = cats.map(function(cat) { return cat.id; });
    return site.posts().categories(ids);
  })
  .then(function(posts) {
    console.log(posts);
  });
```
<!-- .element class="stretch" -->

??? One of the frequently asked questions about the API is how to retrieve posts by their terms.

The API lets you query for posts in a specific tag or category by ID, or you can chain requests to look up posts by a category's slug or tag.

---

### `npm install wpapi`

```js
// Get third and fourth pages of media (media 40-59)
// rel="next" link is exposed as `._paging.next`
site.media().page( 3 ).then(function( page3 ) {
  return page3._paging.next
    .then(function( page4 ) {
      return page3.concat( page4 );
    });
})
  .then(function( media ) { /* Two Pages! */ });
```

??? Pagination is supported with a `_paging` property that exposes the previous and next pages of results for collections

---

### `npm install wpapi`

```js
// Create a post!

site.posts()
  .auth({
    nonce: 'injects nonce with wp_localize_script'
  })
  .create({
    title: 'Hello LOOPCONF!',
    content: 'This has been an excellent conference! ' +
             'let\'s keep it going for DAY 2'
  })
  .then(function( createdPost ) {
    console.log( 'Post saved with ID ' + createdPost.id );
  });
```

??? it supports creating, updating and deleting resources, as well, with authentication; we'll see this in action in a few slides.

---

# React Time!

[github.com/kadamwhite/wp-notebook](https://github.com/kadamwhite/wp-notebook)

??? wpapi provides a query builder interface to let you describe what you want to access through the API, and an HTTP layer to make the request.

It is not required in order to use the REST API, you can use the Backbone client or jQuery or anything you like; but I created it to make it easier to work with the API from node or client apps.

---
<!-- .slide: data-background="url('./images/journal-app-demo.gif')" data-state="solid-bg" -->

??? So let's build that react app!

---

### `register_post_type`

```php
add_action( 'init', function() {
  register_post_type( 'wpn_journal', array(
    // No admin UI or archives page
    'public'             => false,
    // But expose through REST
    'show_in_rest'       => true,
    'rest_base'          => 'journal-entries',
    'capability_type'    => 'post',
    'supports'           => array(
      // Declare the fields this type will have
      'title', 'editor', 'custom-fields'
    )
  ) );
});
```

??? Under the hood, our plugin starts with a custom post type to hold our data.

We will be working with content with a title, a main content object, and custom meta values.

---

### `register_rest_field`

```php
add_action( 'rest_api_init', function() {
  register_rest_field( 'wpn_journal', 'current_music', array(
    'get_callback' => function( $data ) {
      return get_post_meta( $data['id'], '_current_music', true );
    },
    'update_callback' => function( $value, $post ) {
      $value = sanitize_text_field( $value );
      update_post_meta( $post->ID, '_current_music', wp_slash( $value ) );
    },
    'schema' => array(
      'description' => __( 'The music you are listening to.', 'wpnotebook' ),
      'type'        => 'string'
    ),
  ) );
});
```
<!-- .element class="stretch" -->

??? then use register_rest_field to add a string meta value to our endpoint's response.

We could use `register_meta` here but currently there's no way to restrict meta added that way to a specific post type; we're working on that, but for now register_rest_field is our best bet for complex data modeling with the REST API.

---
<!-- .slide: data-background="url('./images/wp-notebook-page-template.png')" data-state="solid-bg" -->

??? Before we get to JavaScript we need a place to render the app, so we also create a custom page template to hold our journal UI, then create a page using that template.

---

### `index.jsx`

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './components/App';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

??? On the JS side, we create an index file that imports React and a to-be-created App component, which it will then render into a container on our page template.

---

### `App.jsx`

```js
import React, { Component } from 'react';

class App extends Component {
  constructor(props) {
    super(props);
    this.state = { entries: [] };
  }

  render() {
    return (
      <div>
        <h1>Hello LoopConf</h1>
      </div>
    );
  }
}
```
<!-- .element class="stretch" -->

??? We then create an app component. To start, it will show "Hello World"

---
<!-- .slide: data-background="url('./images/wp-notebook-hello-world.jpg')" data-state="solid-bg" -->

??? And that gets us this far. Now, let's connect to the API!

---

### `wp_localize_script`
```php
add_action( 'wp_enqueue_scripts', function() {
  wp_register_script( 'wpn_notebook_app', 'path/to/bundle.js' );

  if ( is_page_template( 'wpn_notebook.php' ) ) {
    // Localize our script to inject a NONCE
    wp_localize_script(
      'wpn_notebook_app',
      'WP_API_Settings',
      array(
        'root' => esc_url_raw( rest_url() ),
        'nonce' => wp_create_nonce( 'wp_rest' ),
      )
    );
    wp_enqueue_script( 'wpn_notebook_app' );
  }
});
```
<!-- .element class="stretch" -->

??? To connect to the API, we need to give our script file information about where the API is located and how to connect to it. To do that, we use `wp_localize_script`.

---

### `App.jsx`

```js
import WPAPI from 'wpapi';
import WP_API_Settings from 'WP_API_Settings';
const api = WPAPI.site( WP_API_Settings.root ).auth({
  nonce: WP_API_Settings.nonce
});
api.journalEntries = api
  .registerRoute( 'wp/v2', 'journal-entries/(?P<id>[\\d]+)', {
    params: [ 'status' ]
  });
```
??? Back in App.jsx, we pull in the WPAPI module and initialize an API instance with the settings injected from `wp_enqueue_script`. When the App component is constructed, we tell it to expect a list of journal entries.

See the github repo for how Webpack is configured to allow the settings object to be imported, it's flagged as what's called an "external" so that Webpack will grab it from the global scope.

---

### `App.jsx`
```js
class App extends Component {
  // ...

  componentDidMount() {
    this.updateData();
  }

  updateData() {
    api.journalEntries()
      .status( 'private' )
      .context( 'edit' )
      .then(entries => { this.setState({ entries }) });
  }

  // ...
}
```
<!-- .element class="stretch" -->

??? We give this app class an update data method, that requests journal entries. We request "status private" and "edit context" so that we get the full editable objects.

When the Component is first rendered (mounts), we tell it to request its data.

---

### `App.jsx`

```js
function formatDate(date) { /* magic date formatting */ }

class App extends Component {
  // ...
  render() {
    const { entries } = this.state;

    // iterate over divs & render post for each one
    return (<div>
      {entries.map(entry => (
        <div key={ `entry${entry.id}` }>
          <h2>{ entry.title.rendered }</h2>
          <p>{ formatDate(entry.date) }</p>
        </div>
      ))}
    </div>);
  }
}
```
<!-- .element class="stretch" -->

---
<!-- .slide: data-background="url('./images/basic-post-list.jpg')" data-state="solid-bg" -->

??? We now have some custom post objects rendering!

---

### `App.jsx`

```js
import EntryList from './components/EntryList';
import EntryComposer from './components/EntryComposer';

class App extends Component {
  // ...

  render() {
    const { entries } = this.state;

    return (<div>
      <EntryComposer onSubmit={this.savePost} />
      <EntryList entries={entries} />
    </div>);
  }
}
```
<!-- .element class="stretch" -->

??? Let's start introducing some component hierarchy. We'll make a new component EntryList to handle rendering that list, then make a new component, EntryComposer, which will render a form to add a new journal item.

---

### `EntryComposer.jsx`

```
class EntryComposer extends Component {
  render() {
    return (<form onSubmit={this.handleSubmit}>
      <input type="text" name="title"
        value={this.valueOf('title')}
        onChange={this.handleChange}
      />
      <textarea name="content"
        value={this.valueOf('content')}
        onChange={this.handleChange}></textarea>
      <input type="text" name="current_music"
        value={this.valueOf('current_music')}
        onChange={this.handleChange}
      />
      <button type="submit" className="btn">Save</button>
    </form>);
  }
}
```
<!-- .element class="stretch" -->

??? The EntryComposer component renders a basic HTML form,

---

### `EntryComposer.jsx`

```js
class EntryComposer extends PureComponent {
  // ...

  handleChange(event) {
    const { value, name } = event.target;
    this.setState({
      [name]: value
    });
  }

  handleSubmit(event) { /* Validate, then use onSubmit */ }

  valueOf(prop) { /* magic (not enough space) */ }

  render() {
    // ...
  }
}
```
<!-- .element class="stretch" -->

??? and defines methods to handle state changes within that form.

---

### `App.jsx`

```js
class App extends Component {
  constructor() {
    // ...
    this.savePost = this.savePost.bind(this);
  }

  savePost(post) {
    return this.api.journalEntries()
      .create({
        title: post.title,
        content: post.content,
        current_music: post.current_music,
        status: 'private'
      })
      // Refresh the data to get the update
      .then(result => { this.updateData(); });
  }
```
<!-- .element class="stretch" -->

??? And to make that form work, on submit, we'll fire a savePost method: it will take an object submitted by the child component and create a status:private journal entry using the API.

When the request is done, update is called again to refresh the list.

---

![How to draw a Doge, from a Vice article that 404's](images/how-to-draw-a-doge.png)

??? this probably feels a little bit like those "how to draw an owl" or "how to breakdance" tutorials; we skip over some steps.

---
<!-- .slide: data-background="url('./images/wp-notebook-git-repo.png')" data-state="solid-bg" class="center" -->

#### [<br>&nbsp;github.com/kadamwhite/wp-notebook&nbsp;<br>&nbsp;](https://github.com/kadamwhite/wp-notebook)
<!-- .element class="whitebg" -->


??? Unlike those examples, all the code for these is on github!

---
<!-- .slide: class="center" -->

### *The REST API is for*

## WordPress Core
## Plugin Developers
## Agencies

??? I'm almost out of time, so I wanted to leave you not with a spinning head full of react, but instead with a single simple thought.

The API serves many users. It papers over a lot of inconsistencies within WordPress; last night I inadvertently dubbed it the "jQuery of the WordPress Database."

jQuery filled, and still fills, a critical role in the web development community; and our REST API will, too. It's the first major facade over the internal roughness of WordPress data. It is rough itself, but we're improving it daily.

---
<!-- .slide: class="center" -->

### Every Technology Decision is
# Eventually
# Regrettable

<small>[*Make it Better Without Making it Over*](https://www.youtube.com/watch?v=-ZX8y56Tnx4), Rebecca Murphey at CascadiaFest 2016</small>

??? And if we do our job right, some day we will outgrow this incarnation of the API. Technologies come and go. That WordPress continues to be viable is nothing short of a miracle, in software terms;

we look back on the past and wince, but to quote one of my heroes, Rebecca Murphey, "Every technology decision is eventually regrettable."

I learned to code by making WordPress sites. But eventually my growth outpaced WordPress's. We should always be willing to go see what else is out there.

But that also means that within Wordpress, in a landscape of constant change, one audience and one goal stands above all others.

---
<!-- .slide: class="center" -->

# For Learners

??? The final and most important person the API is for is not somebody who spoke up to get it merged, or who even knows what it is yet. The REST API is for the future generation of WordPress developers.

If every tech decision is eventually regrettable, at any time the best we can hope for is that we are always learning, growing and teaching.

Today, a new generation of developers around the world is making WordPress sites, learning CSS, muddling their way through PHP, discovering the power of JavaScript; and now they can get exposure to REST APIs through WP in a way none of us could.

We came to WordPress and wanted it to do more. The people who have yet to join our community will push it still further.

This is why I will continue to be involved in the project. This is what excites me. I can't wait to hear what they say about the decisions we have made with another decade of hindsight.

---

## *Thank You*

<hr>

Slides: [**talks.kadamwhite.com/loopconf-wpapi**](http://talks.kadamwhite.com/loopconf-wpapi)

Me: [@kadamwhite](https://twitter.com/kadamwhite)

Us: [bocoup.com](https://bocoup.com)

<hr>

[npmjs.com/package/**wpapi**](https://npmjs.com/package/wpapi)

[A Day of REST Boston](https://adayofrest.hm/boston-2017), March 8 &ndash; 10

??? And with that, I thank you for your time.

---

### Fake headlines with [torch-rnn](https://github.com/jcjohnson/torch-rnn)

Actual WIRED Headlines:

**The Bizarre, Bony-Looking Future of Algorithmic Design**

**The Science in The Martian Isn't Perfect, But That's OK**

<br>Generated WIRED Headlines:

**Turning Great Will Drive Action Video**

**This Giant Surfic Battery Could Steal War, Break Instagram**

**How the Web?**

??? Extrapolating further, machine learning was a theme of our OpenVis Conf event last week, so over the weekend I experimented with spidering our own company blog through the API and using that data to train a recurrent neural network:

I could imagine a world in which our sites are capable of manufacturing vacuous filler content entirely on their own, maintaining our own voice in the process

or at least our sites can make up headlines for us as writing prompts, or for us to ensure we're maintaining our voice. The way this neural network works is that you train it on a set of text; WIRED uses the wp api on their site, so I collected two years of WIRED headlines like this, as output by the API&hellip;

and used those headlines to trained another RNN that can generate future headlines. Though it didn't fully learn English, and I don't know what a surfic battery is, I suspect WIRED would report on it. (Star Wars, FB)

There's a lot of data latent in a corpus like these headlines, one of my first experiments just generated a neural net that was a huge star wars fan because of the bulk of articles about that movie from the past few months. Getting our "content" in a machine readable format opens all this up.

---
<!-- .slide: class="center" -->

# Who Is This For?

??? So, who's this actually _for?_ I show you bespoke uses of WordPress as a data archive that are only possible for experienced developers, then share an API that clearly isn't user-facing either.

The goal here is to provide a suite of tools for developers to build amazing user-facing tools on top of or alongside WordPress.
