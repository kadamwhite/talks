<!-- .slide: class="center" -->

# Better<br>Webpack<br>Builds

<br>

<p>K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite) &bull; [Human Made](http://humanmade.com/)</p>
<!-- .element: class="italic" -->

???

Thank you organizers, welcome.

---
<!-- .slide: class="full-height" data-background-video="./video/webpack-home-screen-2.mp4" data-background-video-loop="true" -->

???

Why are we still talking about build tools? Really ought to be a solved problem.

Almost the entire front-end dev community supports Webpack in some fashion.

Webpack isn't part of our UI; it isn't a user-facing feature. It's a means to an end, not the end itself. This should be a boring, rote subject

But where there's friction, there's room for understanding.

Talk intended to demystify a little of what webpack is and does, and to share ways we can better utilize the tools it gives us in our WP projects.


---
<!-- .slide: class="full-height" data-background="url('./images/grunt.png')" data-background-position="center" data-background-size="cover" -->

???

TK: history of bundlers

---
<!-- .slide: class="full-height" data-background="url('./images/dorkq.png')" data-background-position="center" data-background-size="cover" data-transition="none" -->

???

(visual gag)

---
<!-- .slide: class="full-height" data-background="url('./images/browserify.png')" data-background-position="center" data-background-size="cover" -->

---
<!-- .slide: class="full-height light-bg" data-background="url('./images/browserify-transforms.png')" data-background-position="center" data-background-size="cover" -->

### _Browserify Transforms_
<!-- .element: class="whiteoutline" -->

---

### _Browserify Transforms_

`require` more than just code!

_`hello.combyne`:_
```
hello, {{ who }}!
```
_`app.js`:_
```
var template = require( './hello.combyne' );
console.log( template.render({ who: 'world' }) );
```

---

### _Browserify Transforms_

Configured via `package.json`
```
"browserify": {
    "transform": [
        "coffeeify",
        ["browserify-ngannotate", {
            "ext": ".coffee", "bar": true
        }]
    ]
}
```

---

### _Browserify Transforms_

or the command line&hellip;

```
browserify -t coffeeify \
           -t [ browserify-ngannotate --ext .coffee --bar ] \
           index.coffee > index.js
```

---
<!-- .slide: class="full-height" data-background-video="./video/webpack-home-screen-2.mp4" data-background-video-loop="true" -->

???

This brings us back to that webpack home screen. Look at the dependency tree; assets, scripts, styles, images. More than any bundler before it, Webpack is aware of the entire structure of your application: not just code but styles, even images.

---

TK: loader & plugin overview

---
<!-- .slide: class="full-height light-bg" data-background="url('./images/core-ticket-40894.png')" data-background-position="center" data-background-size="cover" -->

???

It's a powerful tool. And since Webpack natively understands modern ES6 imports, it's a better choice for WordPress going forward -- both for core, and for our own themes, plugins and JavaScript front-ends. It works with Vue and React equally, and Webpack supports every major templating system, CSS preprocessor and other common application component I could think to look for.

So again, if it's such an obvious choice, why are we sitting here at WCUS talking about it? Surely we could all just read the docs and 

---
<!-- .slide: class="full-height" data-background="url('./images/webpack-into-wp.png')" data-background-position="center" data-background-size="cover" -->

???

But the truth of the matter is that some of the best parts of Webpack, hot reloading in particular, are hard to get working with WordPress. And that's the main thing I want to talk about today.

We're going to take a fairly standard webpack config, and adapt it so that the dev server works seamlessly alongside WordPress.

---

```
npx create-react-app cra-wcus-demo
```
???
We'll start by using `create-react-app` to install a sample theme

(the npx command lets you execute a package's command-line utility without installing it globally; it will pull down the latest release temporarily just to run the command. This is convenient for boilerplate or scaffolding tools like create-react-app that you won't have to run too often.)

---
  

```md
[master][kadam@wcus:/vm/content/themes/cra-wcus-demo]
[12:35:53] $ npm run eject

> cra-wcus-demo@0.1.0 eject /vm/content/themes/cra-wcus-demo
> react-scripts eject

? Are you sure you want to eject?
This action is permanent. (y/N) _
```

???

Next, in our installed project directory we will run `eject` to write all the configuration to disk, letting us edit our project boilerplate. 

---

_`style.css`_

```css
/*
Theme Name: WCUS Webpack Demo
Description: A barebones example of using Create React App
             in a WordPress theme.
Version: 1.0.0
Text Domain: crademo
*/
/* This CSS file is a stub used to allow theme activation,
and should not be edited directly. */

```

???

We'll add an empty `style.css` in that folder so WP considers it a theme,

---

_`index.php`_
```
<!doctype html>
<html <?php language_attributes(); ?>>
<head>
    <meta charset="<?php bloginfo( 'charset' ); ?>">
    <?php wp_head(); ?>
</head>
<body <?php body_class(); ?>>
    <!-- React App root element: -->
    <div id="root" class="site-content"></div>
</div>
<?php wp_footer(); ?>
</body>
</html>
```
<!-- .element class="stretch" -->

???
And we'll add an absolute bair-bones `index.php` so that the theme can render.
For now the index will just contain a `<div id="root"></div>` in which to render our React app. Routing and proper server rendering of a React app is another talk. Or conference.

---
<!-- .slide: class="full-height" data-background="url('./images/installed-theme.png')" data-background-position="top left" data-background-size="cover" -->

???

Looks great! Totally a useful, functional theme.

With our boilerplate set up, let's figue out how to get our app running.

---
<!-- .slide: class="full-height" data-background-video="./video/npm-run-build.mp4" -->

???

Let's cut the dev server out of things to start and just look at the compiled bundle. `npm run build` takes the application and bakes it into a static set of JS and CSS files.

---
<!-- .slide: class="full-height" data-background="url('./images/tree-build.png')" data-background-position="top left" data-background-size="cover" -->

???

We get some expected things, like a main JS and CSS bundle, and sourcemaps, as well as a service worker and its manifest file. But we also get an asset manifest.

---

_`build/asset-manifest.json`_
```json
{
  "main.css": "static/css/main.c17080f1.css",
  "main.css.map": "static/css/main.c17080f1.css.map",
  "main.js": "static/js/main.fd0901f1.js",
  "main.js.map": "static/js/main.fd0901f1.js.map",
  "static/media/logo.svg": "static/media/logo.5d5d9eef.svg"
}
```

???

This asset manifest describes all of the assets emitted by Webpack. This is awesome, because PHP can read and parse JSON files! Instead of hard-coding a path for our script enqueues, we'll look for the asset-manifest in our build folder and load that.

---

_`config/webpack.config.prod.js`_
```js
    // Generate a manifest file which contains a mapping
    // of all asset filenames to their corresponding output
    // file so that tools can pick it up without having to
    // parse `index.html`.
    new ManifestPlugin({
      fileName: 'asset-manifest.json',
    }),
```

???

The manifest is generated by an instance of the ManifestPlugin, specified in the production webpack config. The plugins in that file are also responsible for minification, setting React into production mode, 

---

1. Read & parse JSON file
```php
    $manifest_path = get_stylesheet_directory()             
        . '/build/asset-manifest.json';

    $asset_list = array_values(
        json_decode(
            file_get_contents( $manifest_path ),
            true
        )
    );
```
2. Iterate through list; enqueue any JS and CSS you find!

???

We read & parse the JSON to get a list of the files to enqueue,
then check each one to see if it ends in JS or CSS, and enqueue appropriately.

Now our theme will load, and the script will render! But we could have done that by renaming the files and writing our own enqueue script call.

For the fun part, let's move on to the dev server.

---
<!-- .slide: class="center" -->

## `npm start`

???

If you run `npm start` when using CRA it starts a webpack dev server on an open port, so your application is accessible at e.g. `localhost:3000`.

No files are written to disk; everything is served from memory. This means fast rebuilds, but nothing we can get to from PHP. Thinking back to that asset list, it said in the config that it's designed to let external code get access to the script assets without parsing index.html, but PHP can't even see index.html in this case without making an HTTP request. that'd be too inefficient.

---

```diff
    diff --git config/webpack.config.dev.js config/webpack.config.dev.js
    index 409182a..19467e7 100644
    --- config/webpack.config.dev.js
    +++ config/webpack.config.dev.js
    @@ -211,15 +211,10 @@ module.exports = {
       ],
     },
     plugins: [
    -    // Makes some environment variables available in index.html.
    -    new InterpolateHtmlPlugin(env.raw),
    -    // Generates an `index.html` file with the <script> injected.
    -    new HtmlWebpackPlugin({
    -      inject: true,
    -      template: paths.appHtml,
    +    // Write an assets-manifest.json to disk with dev server paths.
    +    new ManifestPlugin({
    +      basePath: config.output.publicPath,
    +      fileName: 'asset-manifest.json',
    +      writeToFileEmit: true,
       }),
       // Add module names to factory functions so they appear in browser profiler.
       new webpack.NamedModulesPlugin(),
```
<!-- .element: class="stretch" -->

???

Since WordPress is going to handle rendering the HTML shell, we can replace the HTMLWebpackPlugin instance with a new ManifestPlugin