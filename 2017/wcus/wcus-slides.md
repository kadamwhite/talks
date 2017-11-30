<!-- .slide: class="center" -->

# Better<br>Webpack<br>Builds

<br>

<p>K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite) &bull; [Human Made](http://humanmade.com/)</p>
<!-- .element: class="italic" -->

???

Thank you organizers, welcome. I have some stiff competition in this block and I appreciate that you joined me for this session.

---
<!-- .slide: class="full-height" data-background-video="./video/webpack-home-screen-2.mp4" data-background-video-loop="true" -->

???

Why are we still talking about build tools? Really ought to be a solved problem.

Almost the entire front-end dev community supports Webpack in some fashion.

Webpack isn't part of our UI; it isn't a user-facing feature. It's a means to an end, not the end itself. This should be a boring, rote subject.

But that belies the friction that Webpack causes. It takes time to understand a powerful tool, especially if it changes the way we think about our code.

This talk is therefore intended to demystify a what webpack is and does, and to share ways we can better leverage it in our WP projects.

---
<!-- .slide: class="full-height" data-background="url('./images/grunt.png')" data-background-position="center" data-background-size="cover" -->

???

We've been through this before, with Grunt. Task runners and build tools promise to make our workflows easier, but then we get bogged down in configuration and spend more time

I had the privilege of working for a number of years with Ben Alman, Grunt's creator, and this was especially pronounced for him: he made the tool to help him do the gruntwork associated with maintaining all of his jQuery plugins, but in the end he didn't have time to maintain those plugins anymore because Grunt itself took up all his time.

We can't let our build tools get the better of us.

---
<!-- .slide: class="full-height" data-background="url('./images/browserify.png')" data-background-position="center" data-background-size="cover" -->

???

Webpack of course doesn't replace a task runner like Grunt (although many of the things we can do with Grunt can be done more efficiently and holistically with Webpack).

Webpack is a module bundler, so it instead replaces a tool like Browserify.

---
<!-- .slide: class="center" -->

### _`browserify entry.js -o output.js`_

### _`webpack entry.js output.js`_

???

The base interface for Webpack even looks very similar to Browserify's; We have an _entry_, and it gets bundled into an _output_. And in fact the similarities don't end there.

---
<!-- .slide: class="full-height light-bg" data-background="url('./images/browserify-transforms.png')" data-background-position="center" data-background-size="cover" -->

### _Browserify Transforms_
<!-- .element: class="whiteoutline" -->

???

Browserify gained a lot of traction not just for having a simpler module system than Require.JS, but also because of its transform system.

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

???

Browserify transforms let us require non-JavaScript code directly; they could be used to do things like process template partials into render methods, eliminating a parallel template precompilation step.

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

???

And in fact the chaining and extension-dependent configuration of Browserify anticipates Webpack's configuration in some ways, as well. But transforms often feel like an add-on in Browserify, and maintaining complex toolchains usually required additional tools like Gulp, and custom build pipelines that quickly become difficult to manage.

---
<!-- .slide: class="full-height" data-background-video="./video/webpack-home-screen-2.mp4" data-background-video-loop="true" -->

???

This brings us back to that webpack home screen. Look at the dependency tree; assets, scripts, styles, images. More than any bundler before it, Webpack is holistically aware of the entire structure of your application: not just code but styles, even images.

Out of the box it understands more about JavaScript than older tools like Browserify, providing native support for ES6 modules. But where that out-of-the-box experience falls short, Webpack loaders take over. Browserify transforms felt like an afterthought at times, Webpack's Loaders are core concepts alongside the file entry and output.

---
<!-- .slide: class="center" -->

> Loaders enable webpack to process more than just JavaScript files (webpack itself only understands JavaScript). They give you the ability to leverage webpack's bundling capabilities for all kinds of files by converting them to valid modules that webpack can process.

_https://webpack.js.org/concepts/_

???

It took me a while to get my head around this, so let's clarify: when we load something with Webpack what we're doing is _not_ converting everything into javascript, per se. We're not making images, svg, or css into JavaScript. What we're doing is wrapping those assets with a JavaScript shell so that Webpack can properly output them, and that shell exposes useful information along the way.

Loaders are what lets Webpack process modern JS files with Babel, precompile templates, or convert preprocessor styles into CSS.

---

_Loading CSS_
```
module.exports = {
    module: {
        rules: [
            {
                test: /\.scss$/,
                use: [
                    require.resolve('style-loader'),
                    {
                        loader: require.resolve('css-loader'),
                        options: { /* ... */ },
                    },
                    {
                        loader: require.resolve('postcss-loader'),
                        options: { /* ... */ },
                    },
                    require.resolve('sass-loader'),
                ],
            },
            // ...
```
<!-- .element: class="small stretch" -->

???

If you use Webpack to compile SCSS, we're asking Webpack to make a series of transformations; and each loader is designed to be very specific, so you'll have a loader definition that looks like this:

This uses Node to read and compile a SASS file, then runs that content through PostCSS loader to do further transformations like autoprefixing. The CSS loader interprets `import` and `url` statements, to make sure Webpack knows about all relevant files. Finally, the style loader takes the string content of that transformation process and injects the CSS string into your document.

---

```
module: { rules: [{
    oneOf: [{
        test: [/\.bmp$/, /\.gif$/, /\.jpe?g$/, /\.png$/],
        loader: require.resolve('url-loader'),
        options: {
            limit: 10000,
            name: 'static/media/[name].[hash:8].[ext]',
        },
    }, {
        // Ensure that any files required from JS or CSS
        // get output into the build media directory
        exclude: [/\.js$/, /\.html$/, /\.json$/],
        loader: require.resolve('file-loader'),
        options: {
            name: 'static/media/[name].[hash:8].[ext]',
        },
    },
}]}
```
<!-- .element: class="stretch" -->

???

And when the CSS loader is reading those `import` statements, Webpack will resolve them with loaders, as well. Image files will be tested to see if they are small enough to inline, and if they are Webpack will bake that base64 url-encoded image into the rendered styles. Otherwise, and for all non-image assets as well, the `url-loader` and accompanying `file-loader` ensuring that any assets your styles depend upon get properly output into the build, and that your CSS and JS files point to the correct hashed filenames.

For the amount of power that we get from image inlining, asset cachebusting and build integrity, these loaders are not a lot of configuration for the benefits they gives us.

---

```
module.exports = {
    module: {
        rules: [
                {
                    test: /\.styl$/,
                    use: [
                        'style-loader',
                        {
                            loader: 'css-loader',
                            options: {
                                modules: true,
                                localIdentName: '[path][name]--[local]--[hash:base64:5]',
                            },
                        },
                        'postcss-loader', // See postcss.config.js for options
                        'stylus-loader',
                    ],
                },
            }
        ]
    }
}
```
<!-- .element: class="small stretch" -->

???

Writing the style tags from JS means a couple things. We have an actual dependency chain to the images we use in our CSS, so further enhancements like inlining small files as base64 become trivial. We can also get access to information about our CSS files from within our JS source code.

If you use css-loader's module options, you can specify rules for how Webpack will transform class names. But if Webpack's changing your class names so they are module-specific, how do you know what classes to use?

---

```
import styles from './Modal.styl';
import OverviewAnimation from '../shared/img/overview.gif';

const FAQModal = ({ onCloseFAQ }) => (
    <Modal
      onConfirm={onCloseFAQ}
      confirmText="Continue"
    >
        <div className={styles.center}>
            {/* ... */}
        </div>
    </Modal>
);
```
<!-- .element: class="stretch" -->

???

When we import a stylesheet from our JS, Webpack sends it down that chain so that the styles will eventually end up on the page. But in the process it can also give our JS information about those styles; in this case the loader returns a JS object with mappings of our authored classnames to their generated equivalents, so that we can use the dynamic values in our bundled application.

---

> `raw-loader`: A loader for webpack that lets you import files as a string.

```
module.exports = function(content) {
    return 'module.exports = ' + JSON.stringify(content);
};
```

???

Loaders are extremely powerful, but they don't have to be complex; 

The `raw-loader` for example reads any file in as a string, without transformation; what that means is basically that it reads in the file's data and stringifies it, returning the source code of a new module that passes that string value along to the next loader.

---

[Loader API Documentation, webpack.js.org/api/loaders](https://webpack.js.org/api/loaders/)

[_A Simple Loader_, bocoup.com/blog/webpack-a-simple-loader](https://bocoup.com/blog/webpack-a-simple-loader)

???

This means that they actually aren't hard to write, if you find yourself looking for a type of transformation or file information that isn't already available; I'd recommend reading both the loader documentation, as well as this article by my friend Z on writing a simple loader to parse Markdown.

---
<!-- .slide: class="full-height light-bg" data-background="url('./images/webpack-plugins.png')" data-background-position="top" data-background-size="cover" -->

???

Complementing loaders of course are Webpack's plugins.

The Plugin interface is quite powerful, and there are plugins for minification, optimization, environment variable manipulation, index file generation, you name it.

When you combine loaders and plugins together, webpack has a full dependency tree of every asset required in our frontend build, and a lot of flexibility about how to use that information. Images, stylesheets, ES6 files loaded with babel: Webpack knows their relationships.

---
<!-- .slide: class="full-height light-bg" data-background="url('./images/webpack-hmr.png')" data-background-position="top" data-background-size="cover" -->

???

One of the most powerful results of this system is a technique called Hot Module Reloading. The `webpack-dev-server` library provides a development server which is aware of those relationships, and can swap out pieces as files change without a full page reload. We can do for our source code the same thing that tools like React let do with our content. We can adjust styles, markup & component code almost as quickly from our editors as we could from the browser dev tools.

---
<!-- .slide: class="full-height light-bg" data-background="url('./images/gutenberg-npm-run-build-output.png')" data-background-position="top" data-background-size="cover" -->

???

So what's in our bundle, anyway?

If you've worked on a sufficiently large front-end application you've probably noticed that the size of our javascript bundles can get pretty large.

As developers we have a good sense of our own code, but as JS developers in particular we depend pretty heavily on NPM modules. These can be black boxes, and can pretty significantly increase our bundle size.

Fortunately we have some great tools at our disposal to help us understand where the bloat is coming from.

---

## Export Stats

```
webpack --json > stats.json
```

To use any of these tools we first need to take advantage of Webpack's stats module.

---

## Webpack Visualizer

https://chrisbateman.github.io/webpack-visualizer/

_or_

`npm install webpack-visualizer-plugin`

---
<!-- .slide: class="full-height" data-background-video="./video/webpack-visualizer-demo.mp4" -->

???

(say somethign about video)

---

## Webpack Bundle Analyzer

`npm install -g webpack-bundle-analyzer`

---
<!-- .slide: class="full-height" data-background-video="./video/webpack-bundle-analyzer-treemap.mp4" -->

---
<!-- .slide: class="full-height light-bg" data-background="url('./images/core-ticket-40894.png')" data-background-position="top" data-background-size="cover" -->

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

```
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

Diagram of source files going to compiled assets on one side, and dev server on the other.

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

_`webpack.dev.config.js`_
```diff
 const paths = require('./paths');
 
 // Webpack uses `publicPath` to determine where the app is being served from.
-// In development, we always serve from the root. This makes config easier.
-const publicPath = '/';
+// In development, we always serve from the root of the dev
+// server. This makes it easy for WordPress to find the files.
+const publicPath = 'http://localhost:3000/';

```

???

We have to find some way for WordPress to know where to look for the scripts. First, we declare a consistent location and port for Webpack to use when serving files. We'll change the `publicPath` from the root `/` to the domain `http://localhost:3000/`, so that the bundle will know to look for its assets and files on the dev server and not on disk when we load it in from WP.

---

_`webpack.dev.config.js`_
```diff
plugins: [
+    new ManifestPlugin({
+        basePath: publicPath,
+        fileName: 'asset-manifest.json',
+        writeToFileEmit: true,
+    }),
     // Makes some environment variables available in index.html.
     new InterpolateHtmlPlugin(env.raw),
     // Generates an `index.html` file with the <script> injected.
     new HtmlWebpackPlugin({
         inject: true,
         template: paths.appHtml,
     }),
```
<!-- .element: class="stretch" -->

???

Since WordPress is going to handle rendering the HTML shell, we can replace the HTMLWebpackPlugin instance with another instance of ManifestPlugin -- which helpfully takes a configuration option to force it to write to disk even when a dev server is running!

We add the basePath option, too, so that we'll see the URL in the output.

---

_Dev server's `asset-manifest.json`_
```json
{
  "http://localhost:3000/main.js":
    "http://localhost:3000/static/js/bundle.js",
  "http://localhost:3000/main.js.map":
    "http://localhost:3000/static/js/bundle.js.map",
  "http://localhost:3000/static/media/logo.svg":
    "http://localhost:3000/static/media/logo.5d5d9eef.svg"
}
```

???

The manfiest that this writes out to disk now has the complete paths to the JS bundle. (Note that there's no CSS file -- this is because the JS bundle handles injecting the CSS in dev mode.)

We can injest this file directly from WordPress by hard-coding an enqueue to add it, if it's present. That'll load our script into WordPress, but we'll get some errors.

---

_Replace `react-dev-utils/webpackHotDevClient`_

```diff
-    // Note: instead of the default WebpackDevServer client, we use a custom one
-    // to bring better experience for Create React App users. You can replace
-    // the line below with these two lines if you prefer the stock client:
-    // require.resolve('webpack-dev-server/client') + '?/',
-    // require.resolve('webpack/hot/dev-server'),
-    require.resolve('react-dev-utils/webpackHotDevClient'),
+    require.resolve('webpack-dev-server/client') +
+        '?http://localhost:3000/',
+    require.resolve('webpack/hot/dev-server'),
     // Finally, this is your app's code:

```

See [facebookincubator/create-react-app#1588](https://github.com/facebookincubator/create-react-app/pull/1588)

???

One of the files you'll see in the Webpack entry array that gets included in our build is a module called `webpackHotDevClient` that's provided by CRA. It's a useful utility but it doesn't support binding the hot reload socket connection on a different domain.

The default Webpack one doesn't have a nice error overlay, but it lets you pass in the desired host and port as a require call query parameter. So we swap that out.

There's an outstanding ticket on the create-react-app repo to support binding to a socket that doesn't match `window.location`. Hopefully this gets fixed, but until then we can use this alternative: just remember to also alter the dev server configuration to allow cross-origin requests. (not shown)

---
_`scripts/start.js`_
```diff
      clearConsole();
    }
    console.log(chalk.cyan('Starting the development server...\n'));
-   openBrowser(urls.localUrlForBrowser);
  });
 
  ['SIGINT', 'SIGTERM'].forEach(function(sig) {
    process.on(sig, function() {
+     // Remove the asset manifest file on server termination
+     fs.unlinkSync( process.cwd() + '/asset-manifest.json' );
      devServer.close();
      process.exit();
    });
```
<!-- .element: class="stretch" -->

???

We're almost good to go, but we wouldn't want our theme to look for the dev server when it isn't running. To avoid that we'll remove the dev server's asset manifest whenever the server quits, so we can error out or fall back to the built files depending on preference.

---
<!-- .slide: class="center" -->

### _`npm install -S react-hot-loader`_

???

The final step for hot reloading, at least with Webpack's default hot reloading client, is to install the react-hot-loader. This is a good refresher, since it touches most parts of Webpack.

---

```diff
   entry: [
     // We ship a few polyfills by default:
     require.resolve('./polyfills'),
+    // Support react-hot-loader
+    'react-hot-loader/patch',
     // Include an alternative client for WebpackDevServer. A client's job is to

```


???

First, we add 'react-hot-loader/patch' to our entry file array. This means it goes into the main bundle that webpack emits.

---

_`config/webpack.config.dev.js`_
```diff
  module: {
    strictExportPresence: true,
    rules: [
          // Process JS with Babel.
          {
            test: /\.(js|jsx|mjs)$/,
            include: paths.appSrc,
            loader: require.resolve('babel-loader'),
            options: {
               // Caching results for faster rebuilds.
               cacheDirectory: true,
+
+              "plugins": [ 'react-hot-loader/babel' ],
             },
           },
           // "postcss" loader applies autoprefixer to our CSS.
```
<!-- .element: class="stretch" -->

???

We add the react-hot-loader babel plugin to the configuration for our babel loader, so that as Webpack processes ES modules Babel will decorate them with the metadata needed to reload in the browser.

---

```diff
 import React from 'react';
 import ReactDOM from 'react-dom';
+import { AppContainer } from 'react-hot-loader';
 import App from './App';
 
-ReactDOM.render(<App />, document.getElementById('root'));
+const render = Component => ReactDOM.render(
+    <AppContainer><Component /></AppContainer>,
+    document.getElementById('root')
+);
+render(App);
+
+// Webpack Hot Module Replacement API
+if (module.hot) {
+  module.hot.accept('./App', () => { render(App); });
+}
```
<!-- .element: class="stretch" -->

???

And finally, at the root of our app in index.js we need to set up our base React component to accept hot updates. All these setup steps are explained in the react-hot-loader documentation.

---
<!-- .slide: class="full-height" data-background-video="./video/hot-reloading-demo.mp4" -->

???

Whew! That was a lot. But with all that in place, if we start the dev server and load our WP theme, we now have hot reloading in place!

---

### _Surely there's an easier way&hellip;_

???

It's important to know how to go through those steps, because on a complex project you're likely going to want SASS, or code splitting, or any of the other things you can only do with Webpack if you have full control over the configuration.

But tools like create-react-app were designed to achieve that goal I mentioned at the start, of giving us a build layer that just works for basic use-cases, and a dev server we don't have to think about.

---
<!-- .slide: class="full-height" data-background="url('./images/react-wp-scripts.png')" data-background-position="top" data-background-size="cover" -->

???

As we build more and more React projects on top of WordPress, we've been thinking about this goal, and I'm excited to announce that we released a brand-new project earlier this week designed to help.

---
<!-- .slide: class="full-height" data-background-video="./video/react-wp-scripts-demo.mp4" -->

???

`react-wp-scripts` is designed to work with create-react-app without ejecting; it wraps the scripts used within create-react-app projects to do all of these things we've discussed for you.

---
<!-- .slide: class="center" -->

## Thank You WCUS!

Slides: [talks.kadamwhite.com/wcus2017](http://kadamwhite.github.io/talks/2017/wcus)

~

[github.com/humanmade/**react-wp-scripts**](https://github.com/humanmade/react-wp-scripts)

[github.com/kadamwhite/**wcus-webpack-theme**](https://github.com/kadamwhite/wcus-webpack-theme)
</div>

~

<p>K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite) &bull; [Human Made](http://humanmade.com/)</p>
<!-- .element: class="italic" -->

