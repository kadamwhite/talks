<!-- .slide: class="center" -->

# Data Visualization
### with the WordPress REST API

<br>

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)

???

Thank for intro / thank WCEU organizers; last talk, home stretch!

---
<!-- .slide: class="center" -->

# Data

???

We generally think of WordPress in terms of the things it lets us do -- in terms of publishing, posting, commenting. We think in terms of content. After all, it's a content management system!

We are not usually thinking in terms of data.

---
<!-- .slide: class="center" data-background="url('./images/wp_posts-columns.png')" data-background-position="top" data-background-size="cover" -->

# Data

???

But all that content is of course stored in a database.

And I'd bet that many of us use WordPress for far more than "just blogging," so that database contains a lot of interesting information. Maybe there are things we can learn about even our most "basic" writing by inspecting that content from a different angle.

---
<!-- .slide: class="center" -->

> **The Loop** is PHP code used by WordPress to display posts. Using The Loop, WordPress processes each post to be displayed on the current page, and formats it according to how it matches specified criteria within The Loop tags. Any HTML or PHP code in the Loop will be processed on each post.

<div class="center"><small>
[codex.wordpress.org/The_Loop](https://codex.wordpress.org/The_Loop)
</small></div>

???

The core of a WordPress theme is The Loop -- that PHP code that lets you iterate through your posts and display them on the page.

Thinking in terms of data lets us think about the loop a little differently.

---
<!-- .slide: class="center" -->

`SELECT wp_posts.* FROM wp_posts...`

<div class="center">&darr;&darr;&darr;</div>

`array( $post1, $post2, $post3 );`

<div class="center">&darr;&darr;&darr;</div>

`<div class="post post-1" />`<br>
`<div class="post post-2" />`<br>
`<div class="post post-3" />`

???

What's actually happening in the loop? We're using WordPress to move our data from a MySQL database into PHP, where we then map it into HTML. This transforms our posts from abstract information to something our readers can read and enjoy.

It's a direct mapping of data to visual representation.

---
<!-- .slide: class="center" -->

### Data-Driven Documents

_(or &ldquo;D3&rdquo;; we'll come back to this later!)_

???

When we think about it in these terms, most documents on the web can be thought of as "data-driven": they map some sort of data into some sort of visual representation.

This is usually content; text, words, images; but sometimes we want to communicate information more directly, or convey complex information that would be hard to describe in words or photographs.

---
<!-- .slide: class="center" -->

## Data Visualization

???

Data visualization is the practice of representing complex information visually.

Datavis is all around us: Charts, graphs, and interactive graphics bombard us on news websites, analytics dashboards, television programmes, smartphone apps, and advertisements.

We're so immersed in pictures of data that it can be easy to take them for granted, but every chart or graph you see was created by a human to tell a story.


---
<!-- .slide: class="full-height" data-background="url('./images/minard.png')" data-background-size="contain" data-background-repeat="no-repeat" data-background-position="center center" -->

<div class="attribution"><span>
Charles Joseph Minard, 1869 ([learn more](https://robots.thoughtbot.com/analyzing-minards-visualization-of-napoleons-1812-march))
</span></div>

???

Many different dimensions of information -- such as geographical position, temperature, and so on -- can be embedded into a single graphic.

The field has a long history. It is a particular honor to be giving this talk here in Paris, when many of the pioneers of visualization are themselves French.

(Can't take time to explain graphic, but it shows temperature, location, and travel over time as Napoleon's army invaded Russia in 1812-13) http://patrimoine.enpc.fr/document/ENPC01_Fol_10975?image=54#bibnum

---
<!-- .slide: class="full-height" data-background="url('./images/wpcom-stats-screen.png')" data-background-size="cover" data-background-position="top" -->

<div class="attribution"><span>
WordPress.com Analytics Dashboard, by Automattic
</span></div>

???

We learn to create and read graphs in school, and we reference them daily as we do our jobs. We measure site traffic and sales with one eye on analytics dashboards like those provided by Google or Jetpack.

---
<!-- .slide: class="full-height" data-background-video="./images/nytimes-2013-obama-budget-vis.mp4" data-background-size="contain" -->

<div class="attribution"><span>
_[Four Ways to Slice Obama’s 2013 Budget Proposal](http://www.nytimes.com/interactive/2012/02/13/us/politics/2013-budget-proposal-graphic.html)_, Shan Carter, New York Times, February 2012
</span></div>

???

Charts and maps add depth and perspective to articles beyond what can be conveyed in words or shown in pictures.

Interactive graphics like those produced by the New York Times and other newspapers and magazines let readers explore an issue themselves to understand nuances that might otherwise be missed.

---
<!-- .slide: class="full-height" data-background="url('./images/mister-rogers-cardigans.png')" data-background-size="cover" data-background-repeat="no-repeat" data-background-position="top" -->

<div class="attribution"><span>
The Awl, _[Every Color Of Cardigan Mister Rogers Wore From 1979–2001](https://theawl.com/every-color-of-cardigan-mister-rogers-wore-from-1979-2001-83c1faba2677)_
</span></div>

???

Visualizations can be used to illuminate small details in our everyday lives, for humor or nostalgia,

---
<!-- .slide: class="full-height" data-background-video="./images/bocoup-datavis-hms-lincs.mp4" -->

<div class="attribution"><span>
[LINCS Database Breast Cancer Browser](https://bocoup.com/work/cancer-browser)<br>
Harvard Medical School & Bocoup Data Visualization Team
</span></div>

???

Or in the sciences, where researchers in different groups can produce astronomical amounts of unconnected data, data visualization techniques can be used to build interactive portals like this Breast Cancer Browser: an online tool for exploring and visualizing both published and unpublished datasets to find connections between different studies in a single unified manner.

---
<!-- .slide: class="full-height" data-background-video="./images/bocoup-datavis-mlab.mp4" data-background-video-loop="true" -->

<div class="attribution"><span>
<em>[Measurement Lab - Visualizing the Health of the Internet](https://bocoup.com/work/measurement-lab).<br>
M-Lab & Bocoup Data Visualization Team
</span></div>

???

And this scale of data is of course not limited to science. We talk a lot about Big Data, but how can you reason about something you cannot see? A lot of the work our data visualization team at Bocoup does involves building custom interfaces for specific datasets, going beyond what you can do with analytics tools like Tableau.

---

## So, WordPress?

???

Today I want to share how we can bring the tools and techniques of data visualization to WordPress.

The sorts of news visuals we talked about earlier are often embedded into articles written in WordPress,

But we're going to focus on how we can visualize the information that's already present within our WordPress sites.

---
<!-- .slide: data-background="url('./images/wp_posts-columns.png')" data-background-position="top" data-background-size="cover" -->

???

Because, though we think of WordPress in terms of words, poetry, images, or _content_, that content is of course stored in a database.

And i'd bet that many of us use WordPress for far more than "just blogging," so that database contains a lot of interesting information. Maybe there are things we can learn about even our most "basic" writing by inspecting that content from a different angle.

---
<!-- .slide: class="center" -->

# Content is _Data_

???

Content is data, and data can be visualized.

---

(image of post frequency graphic from Jetpack Analytics -- need a site updated more than my blog is)
![GitHub Contribution Frequency Graph](./images/github-contributions-graph.png)

???

To see how we can do this ourselves, let's start with another chart you might have seen before: the posting freqency graphic used in Jetpack. it's a variation of the lower graphic, which you may recognize as GitHub's contribution frequency graph.

---
## Technologies

### D3.js (Data Driven Documents)
### React
### SVG (Scaleable Vector Graphics)
### Canvas
### WebGL (and libraries like REGL)

???

This is going to be light on code, but there are a lot of tools available for creating rich, interactive visualizations on the web. We'll be looking at only a few of them, with the goal of showing the overall process you can use to build a chart or map on the web. All demos have linked code samples.

---

## Getting The Data

- GET /wp-json/wp/v2/posts
- GET /wp-json/wp/v2/posts?page=2
- GET /wp-json/wp/v2/posts?page=3
- &hellip;forever?

<div class="fragment">
**_No!_** Make a custom endpoint :)

- GET `/wp-json/wceu/2017/posts`

</div>

???

Most web data visualization is created using JavaScript, so our first step is to get our data onto the client. Fortunately we have the WordPress REST API to help us.

We're going to get the past year of posts for our site, for all authors. For this example we're going to pull the fields we want from the existing REST API posts endpoint one page at a time, which means we'll be inefficiently transmitting a lot of unnecessary information.

If you are building something like this into your own plugin, I recommend creating a custom endpoint to reveal just the data you need.

(convert to use `rest-filter-response-fields` plugin?)

---

### Page through posts endpoint

(will be replaced by flow diagram)
```js

const now = new Date();
const msInOneYear = 1000 * 60 * 60 * 24 * 365;

function getUpdateAndIterate( request ) {
    request.get().then( ( posts ) => {
        if ( now - new Date( posts.date ) > msInOneYear ) {
            return;
        }
        updateGraphic( posts );
        if ( posts._paging && posts._paging.next ) {
            getAndUpdate( posts._paging.next );
        }
    });
}

getUpdateAndIterate( wp.posts().perPage( 20 ) );
```
<!-- .element class="stretch" -->

???

This isn't a code talk so I'm going to describe what we do rather than show you lines and lines of code, but all the examples we're looking at are up on github and linked from my slides.

We fetch our first page of results -- we'll get 20 posts at a time, which is a good balance between payload transfer size and number of steps.

Each time a page comes back, we'll pass the new data to an update function, then check to see if there's another page of results. If there is, and if we're still within the past year, we'll iterate on to fetch the next page.

---

### Parse the Data

```js
[
    { id: 1178, date: "2017-04-11T20:22:19" },
    { id: 1170, date: "2017-04-02T16:11:42" },
    { id: 1169, date: "2017-04-02T10:41:27" },
    // And so on
]
```
```js
[
    { date: "2017-04-11", count: 1 },
    { date: "2017-04-02", count: 2 },
    // And so on
]
```

???

Using this process we can build up an array of all the posts in the past year. We iterate through that list to create a new array, with only the counts of posts per date.

This is why we'd want to build a new endpoint to get this data -- we've now thrown away almost all of the data the posts endpoints returned to us! But you can use this approach for prototyping on a local install.

---

### Draw the Squares

```html
    <div />
    <div />
    <div />
    <div />

    <!-- ...& 361 more -->
```
Our graphic will be a grid of squares, so we know we'll need to render a square for each day. For this graphic we're just going to use divs, but we'll switch to SVG in the next example.

---
<!-- .slide: class="full-height center" data-background-video="./images/bocoup-datavis-canvas-performance.mp4" data-background-video-loop="true" data-background-position="top" data-background-size="contain" -->

<div class="attribution"><span>
Yannick Assogba, [Needles, Haystacks, and the Canvas API](https://bocoup.com/blog/2d-picking-in-canvas)
</span></div>


???

DOM and SVG rendering can only get us so far. The browser cannot render thousands of SVG nodes without a little stutter; for smooth animation with thousands of individual datapoints, you need to use the HTML Canvas element for rendering.

---
<!-- .slide: class="full-height center" data-background-video="./images/bocoup-datavis-canvas-animation-dark.mp4" data-background-video-loop="true" data-background-size="cover" -->

# Canvas

<div class="attribution"><span>
Peter Beshai, [Smoothly animate thousands of points with HTML5 Canvas and D3](https://bocoup.com/blog/smoothly-animate-thousands-of-points-with-html5-canvas-and-d3)
</span></div>

???

Canvas is a drawing surface inside the browser. It gives us a lower-level, high performance drawing API that can handle much more complex animations than SVG without breaking a sweat.

For complex charts like large network graphs, or to show thousands of points moving across maps, Canvas is the way to go.

However, things that SVG gives us "for free," like mouse events and selector hierarchy, aren't available -- we get this performance at the expense of simplicity, because actions like selecting a datapoint require more calculations and manual development.

---
<!-- .slide: class="full-height center" data-background-video="./images/pbesh-webgl-animation.mp4" data-background-video-loop="true" data-background-size="cover" -->

# WebGL

<div class="attribution"><span>
Peter Beshai, [Animate Points with WebGL and REGL](http://peterbeshai.com/beautifully-animate-points-with-webgl-and-regl.html)<br>
_see also_ Jim Vallandingham, [An Intro to regl for Data Visualization](http://vallandingham.me/regl_intro.html)<br>
_also see also_ [thebookofshaders.com](https://thebookofshaders.com/)
</span></div>

???

Shaders are complex -- This takes us even further away from the easy-to-read SVG code we saw earlier, but it's the fastest rendering you're going to see in the browser!

[Book of Shaders](https://thebookofshaders.com/) at thebookofshaders.com

Tools like REGL (pronounced "regal"), a REactive WebGL framework, make working with WebGL simpler; Three.js is another popular WebGL library, and I expect we'll continue to see more & more resources pop up to make it easier to get started.

---
<!-- .slide: class="full-height" data-background="url('./images/vega-lite-homepage.png')" data-background-size="cover" data-background-repeat="no-repeat"  data-background-position="top" -->

<div class="attribution"><span>
Vega & Vega-Lite, [vega.github.io/vega-lite](https://vega.github.io/vega-lite/)<br>
Arvind Satyanarayan, _[Reactive Building Blocks: Interactive Visualizations with Vega](https://www.youtube.com/watch?v=Y8Fp9z-9DWc)_, OpenVis Conf 2016
</span></div>

???

As we begin to wrap up, I want to emphasize that you don't always have to handle the rendering yourself.

Analysis tools like Tableau or Excel can frequently get you something useful. Writing your own data pipeline and WebGL renderer will only be the best option when you have something big and valuable to analyze.

In the middle, there are an increasing number of tools for
One of them, from a team I've had the pleasure to work with at the University of Washington in the US, is a vizualization grammar called Vega, and its simplified derivative Vega-Lite. These grammars let you build a tool that formats your data into a JSON representation of what a chart should look like -- vega will do the rest.

---
<!-- .slide: class="full-height" data-background="url('./images/vx-gallery.png')" data-background-size="cover" data-background-repeat="no-repeat"  data-background-position="top" -->

<div class="attribution"><span>
REACT + D3 = VX, [vx-demo.now.sh](https://vx-demo.now.sh/)
</span></div>

???

Or for more control, there's many different component libraries for React, Vue or Angular that give you lower-level primatives you can use to draw your charts.

---

### Resources

- [FlowingData](https://flowingdata.com/)
- [Dashing D3.js](https://www.dashingd3js.com/), tutorials & lessons
- [Bocoup DataVis Blog](https://bocoup.com/blog/category/datavis)
- Conferences: [OpenVis Conf](https://openvisconf.com/), [Eyeo Festival](http://eyeofestival.com/), [EuroVis](http://eurovis2017.virvig.es/), [Visualized](http://visualized.com/), [Data Visualization Summit](https://theinnovationenterprise.com/summits/data-visualization-summit-boston-2017), [Strata](https://conferences.oreilly.com/strata), _<span class="amp">&amp;</span> many, many more_

---

# Thank You
