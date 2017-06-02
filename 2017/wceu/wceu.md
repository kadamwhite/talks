<!-- .slide: class="center" -->

# Data Visualization
### with the WordPress REST API

<br>

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite) &bull; [Bocoup](https://bocoup.com)

???

Thank for intro / thank WCEU organizers; last talk, home stretch!

---
<!-- .slide: class="center" -->

# Data Visualization

???

Data Visualization, or "datavis," is all around us. Charts, graphs, & interactive graphics bombard us on news websites, analytics dashboards, television programmes, smartphone apps, and advertisements.

We're so immersed in pictures of data that it can be easy to take them for granted, but every chart or graph you see was created by a human to tell a story.


---
<!-- .slide: class="full-height" data-background="url('./images/minard.png')" data-background-size="contain" data-background-repeat="no-repeat" data-background-position="center center" -->

<div class="attribution"><span>
Charles Joseph Minard, 1869 ([learn more](https://robots.thoughtbot.com/analyzing-minards-visualization-of-napoleons-1812-march))
</span></div>

???

The field has a long history. It is a particular honor to be giving this talk here in Paris, when so many of the pioneers of visualization are themselves French.

(Can't take time to explain graphic, but it shows temperature, location, and travel over time as Napoleon's army invaded Russia in 1812-13) http://patrimoine.enpc.fr/document/ENPC01_Fol_10975?image=54#bibnum

---
<!-- .slide: data-background="url('./images/wpcom-stats-screen.png')" data-background-size="cover" data-background-position="top" -->

<div class="attribution"><span>
WordPress.com Analytics Dashboard, by Automattic
</span></div>

???

We learn to create and read graphs in school, and we reference them daily as we do our jobs. We measure site traffic and sales with one eye on analytics dashboards like those provided by Google or Jetpack.

---
<!-- .slide: class="full-height" data-background-video="./images/bocoup-datavis-syria-settling.mp4" -->

<div class="attribution"><span>
_[This is the life of a Syrian refugee](https://bocoup.com/blog/globalpost-syria-conflict)_, Paul Wood, [GlobalPost, 24 September 2015](https://www.pri.org/stories/2015-09-24/daily-hustle-survive-life-syrian-refugee).<br>
Maps and Graphics by the Bocoup Data Visualization Team.
</span></div>

???

Charts and maps add depth and perspective to articles beyond what can be conveyed in words or shown in pictures.

Interactive graphics like those produced by the New York Times and other newspapers and magazines let readers explore an issue themselves to understand nuances that might otherwise be missed.

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
<!-- .slide: data-background="url('../../2016/wp-as-data-csvconf/images/wp_posts-columns.png')" data-state="solid-bg" -->

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

(screenshot or text sample of REST API posts endpoint request)

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
<!-- .slide: class="full-height" data-background="url('./images/minard.png')" data-background-size="contain" data-background-repeat="no-repeat" data-background-position="center center" -->

### Resources

- [Bocoup Data Visualization](https://bocoup.com/services/datavis), examples of our work
- [Dashing D3.js](https://www.dashingd3js.com/), tutorials & lessons