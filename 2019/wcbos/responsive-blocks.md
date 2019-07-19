# Responsive Blocks
<!-- .element: class="montserrat" -->

<hr>

K. Adam White &bull; [@KAdamWhite](https://twitter.com/kadamwhite)


<img src="../../2018/wceu/images/hm-logo.png" style="margin-top: 0; height: 2em;" alt="Human Made Logo" />

???

(If intro'd, thank you)
(else,) I'm K Adam White -- you can call me KAdam. I'm a senior engineer and team lead at Human Made, an enterprise WordPress digital experience consultancy. I came up from New York this weekend to get away from the heat, and I'm really excited to share some fun responsive design techniques with you all this morning.

---

# Thank You, WordCamp Boston

???

Before we get into it, a round of applause for WordCamp Boston -- 10 years!

I lived in Somerville until last year, and I owe my career to the Boston WordPress community. I started attending the local meetup right after moving here, and it's an incredibly welcoming group. I gave my first talk on this same stage at WCBos 2011, and I never expected to still be here eight years later, speaking to you as a senior engineer and core committer -- it's a wonderful event and a fantastic community, and I'm extremely grateful to everybody in this room and everybody who makes this event happen.

So, I challenge you all. What do you have to share? Everybody in the room knows a topic well enough to present at a meetup or WordCamp. It can be an amazing opportunity to meet people and maybe even make something of a name for yoruself. There's no pressure to speak if you don't want to, but if you do, and don't know how to start, try applying to WordCamp next year. I look forward to learning from you all.

---

### _let's talk_
# Responsive Design

???

So what's this talk about? There's a little code, but my goal today is to give you tools you can use without having to write anything but HTML or CSS. At its core, this talk's about responsive design, and how we implement responsive designs.

We're all likely familiar with RD but let's think back to its beginnings, to Ethan Marcotte's pivotal article 

---

### 🎊

### _`@media( min-width: 40em ) {}`_

### 🎉

???

No web technology evolves in just one place, but if Boston has one major claim to internet fame I think it's how this city's programmers and designers popularized responsive design. From the high-profile launch of the new Boston Globe site, to the community resources and tools from Filament Group and others, and more recently the work by other locals such as Mat Marquis around responsive images, we began to advocate for the web we wanted to use.

Responsive design as we usually understand it is about adapting our experiences to the window or device we're using to browse. We can use the size and orientation of the viewport to present different layouts to our visitors, because what's usable on a widescreen desktop isn't as useful crammed onto a tiny phone screen. (Even if phones are huge now)

The media query is an amazing invention, and the way we've used it to move towards mobile-first responsive design has made the web a better, more usable and beautiful place.

---
<!-- .slide: class="full-height" data-background="images/latest-posts-block.png" data-background-size="cover" -->

???

but the media query doesn't solve everything. Our designs these days are component- or block-based; we create a site by arranging discrete units of content. If we take a list of recent posts, media queries let us style it to break out to a wider layout at larger screen sizes. This works great for a full-screen component, but what if we want this recent posts list to live in a sidebar, or within a columns block?

---
<!-- .slide: class="full-height" data-background="images/narrow-column.png" data-background-size="cover" -->

???

We need to style our blocks not just to accommodate the screen, but also their surrounding context on the page. If you're viewing a site on a HiDPI wide-screen monitor, a block in the sidebar may still be displaying at a width we'd normally associate with mobile.

We'd ideally want to drop the layout to single- or at least two-column,

---

### Content Hierarchy
### Visual Weight
### Typography
### Layout

<br>

<small>_Ethan Marcotte, [A Bit More on Container Queries](https://ethanmarcotte.com/wrote/a-bit-more-on-container-queries/)_, 2017</small>

???

And layout's only the start: depending on where a component occurs on your page, there's a whole host of design changes you might want to apply. Ethan Marcotte outlines a few of these in one of his excellent articles on this topic.

It's not impossible to work around this. Core blocks like this latest posts block give you controls to alter their layout, so if I knew this was going to be displaying in a sidebar I'd likely have chosen a different layout.

---

### Styling for Context
```css
    .my-block {
        /* mobile-first base styles */
    }

    @media ( min-width: 40em ) {
        .my-block {
            /* widescreen styles */
        }

        .wp-block-column .my-block {
            /* reinstate base styles */
        }
    }
```
<!-- .element: class="stretch" -->

???

For blocks that don't have so many controls, we can still style around this by including parent classes to alter the layout when we know it occurs within a certain context. When we release a plugin that registers blocks and widgets, we can ship it with styles to account for the core columns block, sidebars, and other known contexts. We have to manage these known core bloc scenarios individually, but it's doable.

But how do we account for the fact that an author could choose to use our block anywhere on a page, and we can't know where? We can support every known core context, but as soon as an author installs a new theme or puts our block within another custom container, all our assumptions could be out the window.

---

### _dreaming of_
## Element Queries

???

It's this complexity and uncertainty that lead web developers to propose what we call an _element query_. If you've heard the phrase container query, they refer to the same idea -- a container query is an element query on a container, used to style child elements.

---

```css
        .my-block {
            /* mobile- or "narrow-first" layout */
        }
        .my-block:media( min-width: 20em ) {
            /* wide layout (hypothetical syntax) */
        }
        .sidebar .my-block {
            /* contextual design changes */
        }
```

???

What if, the thought goes, we could tag our styles with a media rule that says, "only apply these styles if the element is this big?" Then we'd be able to handle all possible sizing contexts with a few elegant rules. We could focus our energy on writing styles for those specific cases where we want to alter the _feel_ or _impact_ of the content, rather than laboriously handling every possible layout scenario.

---

![Chris Coyier tweet](./images/chris-coyier-tweet.png)

???

There's two quotes that we're contractually obligated to include in any presentation on element queries, and one of them is Chris Coyier's assertion that most of the time we're writing a media query, we really want a container query.

We want to be able to write our components in a truly modular way, without constantly having to check against containers and contexts. In practice I think this number would be significantly above 50%.

---

#### “Tell us what you want! We’re listening. We want to know which features to prioritise based on real-world feedback from developers like you.”

#### “How about container quer—”

### “Not that.”

<br> 
<small>_Jeremy Keith, [Container queries](https://adactio.com/journal/12585)_, 2017</small>

???

These queries would solve a clear need. This proposal's been floating around for roughly half a decade now. Why aren't we all using this? The other required slide I have to include is this quote from Jeremy Keith about how it sometimes feels like browsers have been deliberately ignoring web developers.

---

## <span style="font-size: 0.6em;">💥</span> &infin; <span style="font-size: 0.6em;">💥</span>

```css
    .my-element:media(min-width: 500px) {
        width: 499px;
    }
```

<br>

<small>_Mat Marquis, [Container Queries: Once More Unto the Breach](https://alistapart.com/article/container-queries-once-more-unto-the-breach/), 2015_</small>

???

There's no conspiracy, and the browsers haven't betrayed us. It turns out that we don't have element queries yet because they're impossible.

For one, it's trivially easy to write a style rule that would trigger an infinite loop of style recomputation.

Even without infinite loops, having layout feed back into the computation of the style tree and CSS cascade would significantly impact rendering performance. However much this feature would help us, browsers don't really win points with users by making the web slower and more expensive to render.

---
<!-- .slide: class="full-height" data-background="images/css-containment.png" data-background-size="cover" -->

???

Chrome has implemented an experimental feature called CSS Containment which would let you instruct a browser that one part of a document's layout should not impact the rest, but that's not enough on its own.

---

### Container Queries
## Not A Thing

???

Even by re-casting the discussion to be about _container queries_ -- only styling elements based on the size of their parents -- we can't change the CSS equation sufficiently to allow this feature to exist.

---

### have you considered
## JavaScript?

???

So a CSS-only solution's out, for now. Maybe we can find a JavaScript solution, like we did with the picture element while responsive images were being designed.

---
<!-- .slide: class="full-height" data-background="images/eqcss.png" data-background-size="cover" -->

???

And indeed you will find several JavaScript prollyfills, ponyfills and bronyfills implementing a handful of syntax options for container and/or element queries.

---

## we will be ignoring these

???

I have not led you astray, and JavaScript is indeed to the rescue! But we won't be using any of these proposed container query syntaxes or libraries.

An excellent talk by Philip Walton at CSSConf last year convinced me that our focus on container query syntax is putting our pursuit of a specific solution ahead of the problem.

---

### remember the
## Original Problem

???

We're therefore going to take a step back and return to that original problem we wanted to solve. How do we style a component based not on the page, but on its container?

---

## _`.container-md {}`_?

???

In CSS we normally scope styles to a container using classes. How about we write JavaScript to listen for browser viewport changes, and apply classes to our containers to indicate their size?

Unfortunately this is slow, and won't catch layout changes that aren't triggered by viewport size events.

---

## _`new ResizeObserver();`_

???

The solution we're going to use is a new JavaScript interface called ResizeObserver. As the name suggests, ResizeObserver lets us efficiently react to element size changes.

---
<!-- .slide: class="full-height" data-background="images/philip-walton-at-cssconf.png" data-background-size="cover" -->

<small><em>Philip Walton, [Container Queries: The Past, Future, and How You Can Actually Even Use Them Today](https://www.youtube.com/watch?v=0wA4CMo9_EU), CSSConf EU 2018</em></small>
<!-- .element: class="whitebg" -->

???

I should preface by saying that the rest of this talk, and the plugin I've released to implement this solution, is based on an excellent presentation by Philip Walton from last year's CSSConf EU.

Philip is an engineer on Google's Chrome & Web Platform techniques, and has popularized a ResizeObserver-based approach to responsive components that I find to be the most compelling and practical solution we have to styling components based on their size on page.

---

<table>
    <thead>
        <tr>
            <th style="width: 4em;">Container Width</th>
            <th>Classes Applied</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>320px</td><td>`(none)`</td>
        </tr>
        <tr>
            <td>420px</td><td>`.container-sm`</td>
        </tr>
        <tr>
            <td>640px</td><td>`.container-sm.container-md`</td>
        </tr>
        <tr>
            <td>960px</td><td>`.container-sm.container-md.container-lg`</td>
        </tr>
        <tr>
            <td>1280px</td><td>`.container-sm.container-md.container-lg.container-xl`</td>
        </tr>
    </tbody>
</table>

???

So let's see how that solution works. Well, ResizeObserver lets us observe how large an element appears on the page. If we observe a container, we can use JavaScript to add classes to that container based on how big it is.

We'll do this in a way that mirrors how we use media queries, layering additional classes on as the component expands.

---

```css
    .latest-posts {
        /* single-column styles */
    }
    .latest-posts.container-sm:not(.container-md) {
        /* customizations specific to a wide single column */
    }
    .latest-posts.container-md {
        /* two-column styles */
    }
    .latest-posts.container-lg {
        /* three-column styles */
    }
    .latest-posts.container-xl {
        /* four-column styles?!? sky's the limit! */
    }
```
<!-- .element: class="stretch" -->

???

In our stylesheets we can then take advantage of these classes in the same way we would have used element or container query CSS rules: we can style based on the size of the container, not the page. Now if we write a rule that applies to medium-width containers, it will apply whether your block is displaying fullscreen on a phablet or in a narrow column on an ultra-widescreen display.

---

### `<div data-responsive-container>`

???

It wouldn't be performant to observe every element on the page, and if we did then our CSS would get pretty gnarly. We opt an element into this treatment by adding a data-attribute to it, specifically `data-responsive-container`.

---

#### `data-responsive-container='{"sm":600,"lg":1200}'`

#### `data-responsive-container='{"onecol":400,"twocol":800}'`

???

Neither components nor WordPress themes are one-size-fits-all, so if we don't want to use the default set of "breakpoints" on a given container, we can specify a set of container-specific overrides.

By assigning a JSON string to the `data-responsive-container` attribute, our JS code can read in component-specific styles and apply exactly the breakpoints and classes that best fit your block or widget.

---

# ![WordPress logo](../../2017/democratizing-software-wcbos/images/wordpress-logo.png) ?
<!-- .element: style="vertical-align: middle;" -->

???

But, OK. So we can make a good system for reacting to responsive breakpoints. But if I were you, I'd be asking, do I have to re-write the JS in every project? do I have to write the JS at all? what if we want to focus on the HTML & CSS, and the site design and content? For this to be a truly workable container styling system, we need a consistent way to apply it across projects.

I agree; and I'm excited to announce today a new plugin that provides this functionality for any WordPress site.

---
<!-- .slide: class="full-height" data-background="images/responsive-containers-plugin.png" data-background-size="cover" -->

???

This past week I released a plugin called Responsive Containers, which adds a JS file to your site which will look for elements with the `data-responsive-container` attribute and tag each container a preset list of size-based classes.

After twelve years using WordPress, six years contributing to the project, and dozens of custom plugins written for clients, this is actually the first plugin I've ever submitted to the plugin directory; our banner image could probably use some work but I'm really excited to share it with you!

---

```php
    function myplugin_render_block( $attributes ) {
        ob_start();
        
        echo '<div class="fancy-block" data-responsive-container>';
        
        // ...block markup
        
        return ob_get_clean();
    }
```
Declaring a responsive container in PHP

???

With this plugin installed and activated, we can add that data-attribute to our block or widget markup and begin taking immediate advantage of the sizing classes.

This applies whether we're writing our HTML from PHP,

---

```
    save() {
        return (
            <div
                className="fancy-block"
                data-responsive-container
            >
                { /* ...block markup */ }
            </div>
        );
    }
```
Declaring a responsive container in React

???

or if we're generating our HTML using React and JSX. Any element with `data-responsive-container` will get our default set of sizing classes.

---

```php
    function myplugin_render_block( $attributes ) {
        ob_start();
        echo sprintf(
            '<div class=fancy-block" data-responsive-container="%s">',
            // responsive_container_breakpoints() calls esc_attr internally.
            responsive_container_breakpoints( [
                'fancy-block--2-column' => 600,
                'fancy-block--3-column' => 900,
            ] )
        );
        // ...block markup
        return ob_get_clean();
    }
```
<!-- .element: class="stretch" -->
Custom container breakpoints in PHP

???

As described before, we can provide a JSON object as the value for our data attribute to use a custom set of container breakpoints for a specific element.

I've provided a `responsive_container_breakpoints` helper, which JSON-encodes & escapes a PHP array of classname-size pairs.

---

```
    save() {
        return (
            <div
                className="fancy-block"
                data-responsive-container={ JSON.stringify( {
                    'fancy-block--2-column': 600,
                    'fancy-block--3-column': 900,
                } ) }
            >
                { /* ...block markup */ }
            </div>
        );
    }
```
<!-- .element: class="stretch" -->
Custom container breakpoints in React

???

If we're writing a block in JavaScript, React will handle the escaping for us so we can just pass our object to JSON.stringify.

---
<!-- .slide: class="full-height" data-background="images/caniuse-resizeobserver.png" data-background-size="contain" -->

???

Hopefully I've got you interested in using this technique in your own projects, and hopefully you'll all find this plugin useful in your work.

But I suspect some of you are wondering about browser support and performance.

At present ResizeObserver is only available in Chrome and Opera. We do ship a polyfill as part of our JS bundle, so if you use this plugin 

---

Conceptual closing

---

Thank you