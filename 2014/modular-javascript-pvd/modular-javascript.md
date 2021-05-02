# Modular
# JavaScript

*September 2014 &bull; WordCamp Providence*

K. Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)



## Introductions



![Bob (Bocoup Logo)](../../2013/backbone-wordpress/images/bocoup-vertical-676.png)



![Photograph of a stack of $100 bills](images/AndrewMagill-Money.jpg)

<small>*[Andrew Magill, "Money"](https://www.flickr.com/photos/amagill/3366720659)*</small>



![Photograph of a cut-up $100 bill](images/TaxCredits.net-Money.jpg)

<small>*[TaxCredits.net, "Money"](https://www.flickr.com/photos/76657755@N04/7408506410)*</small>



`media-views.js`

Note: There are over 400 functions defined in media-views.js, and over 50 different views. Finding the code you want takes a lot of scrolling!



![Screenshot of the final lines of media-views.js](images/media-zoom-01.png)



![Screenshot of the final lines of media-views.js](images/media-zoom-02.png)



![Screenshot of the final lines of media-views.js](images/media-zoom-03.png)



![Screenshot of the final lines of media-views.js](images/media-zoom-04.png)



![Screenshot of the final lines of media-views.js](images/media-zoom-05.png)



# Modules



> A self-contained piece of code defining a set of related functionality



## The Most Basic JS Module System



<pre><code>
&#60;script type="text/javascript" src="lib/jquery.min.js">&#60;/script>
&#60;script type="text/javascript" src="lib/plugin.js">&#60;/script>
&#60;script type="text/javascript" src="lib/horrible-image-slider.js">&#60;/script>
&#60;script type="text/javascript" src="my-app.js">&#60;/script>

</code></pre>



## We're Done!



## :(



Bad Granularity

Note: We're still trying to buy a coke with a $50



No Dependencies



## We've all been here
![reference error: $ is not defined](../modular-javascript/images/reference-error.png)
<pre><code>
&#60;script type="text/javascript" src="my-app.js">&#60;/script>
&#60;script type="text/javascript" src="lib/jquery.min.js">&#60;/script>

</code></pre>



## What is a Module?, v2
> A self-contained piece of code defining a set of related functionality **and any required dependencies**



## The WordPress JS Module System



## Dependencies!
```php
wp_register_script(
    'my-plugin-script',
    plugin_dir_url( __FILE__ ) . 'js/awesome-plugin.js',
    array( 'jquery' ),
    '9000.0.1',
    true
);
```



## File size... not so much
<br>
`wp_enqueue_script` &rarr; `<script/>`



## Code in JS, deps in PHP? :(
<br>
```php
wp_enqueue_script( /*...*/, array( 'jquery' ), /*...*/);
```
<br>
> [A Module is] a **self-contained piece of code**...



We need to be able to
## Author modules
as separate files, then
## release modules
as enqueue'able, built scripts



# Module Systems



## AMD vs CommonJS



# CommonJS
**(Node is a variant)**



## Node's require() &amp; module.exports
```javascript
var globule = require('globule');
var findup = require('findup-sync');
var resolve = require('resolve').sync;
var stackTrace = require('stack-trace');
var path = require('path');

// export object
var matchdep = module.exports = {};
```
<small>*from [node-matchdep](https://github.com/tkellen/node-matchdep), by Tyler Kellen*</small>



# AMD



Practically speaking,

**AMD &#8776; Require**



## define()
```javascript
define([
    './cart',
    './inventory'
], function( cart, inventory ) {
    // return an object to define the module
    return {
        color: 'blue',
        size: 'large',
        addToCart: function() {/* ... */}
    }
});
```
Require has [many ways to `define` a module](http://requirejs.org/docs/api.html#define):  
this is the most common



## The Future:
#ES6 Modules

Note: The next version of JavaScript will have native modules!



```javascript
    //------ lib.js ------
    export const sqrt = Math.sqrt;
    export function square(x) {
        return x * x;
    }
    export function diag(x, y) {
        return sqrt(square(x) + square(y));
    }

    //------ main.js ------
    import { square, diag } from 'lib';
    console.log(square(11)); // 121
    console.log(diag(4, 3)); // 5
```

[ES6 Modules: The Final Syntax](http://www.2ality.com/2014/09/es6-modules-final.html)



...but they won't be in browsers for a while.



## We're going to focus on AMD

because it's designed for the browser



Choose Your Own Granularity



## AMD Structure in jQuery

`jquery.js`:
```javascript
define([
    "./core",
    "./selector",
    "./traversing",
    "./callbacks",
    "./deferred",
    "./core/ready",
    "./data",
    "./queue",
    "./queue/delay",
    "./attributes",
    "./event",
    "./event/alias",
    "./manipulation",
    "./manipulation/_evalUrl",
    "./wrap",
    "./css",
    "./css/hiddenVisibleSelectors",
    "./serialize",
    "./ajax",
    "./ajax/xhr",
    "./ajax/script",
    "./ajax/jsonp",
    "./ajax/load",
    "./event/ajax",
    "./effects",
    "./effects/animatedSelector",
    "./offset",
    "./dimensions",
    "./deprecated",
    "./exports/amd",
    "./exports/global"
], function( jQuery ) {

return jQuery;

});
```



## Loading AMD modules with Require.js
<pre><code>
&#60;!doctype html&#62;
&#60;html&#62;
&#60;head&#62;
  &#60;title&#62;jQuery via AMD&#60;/title&#62;
  &#60;script type="text/javascript"
          data-main="./jquery/src/jquery"
          src="require.js"&#62;
  &#60;/script&#62;
  &#60;script type="text/javascript"&#62;
    requirejs.config({
      paths: {
        sizzle: "../../sizzle/src/sizzle"
      }
    });
  &#60;/script&#62;
&#60;/head&#62;
&#60;body&#62;
  &#60;!-- This will get rendered via JS --&#62;
  &#60;h1 id="title"&#62;&#60;/h1&#62;

  &#60;script type="text/javascript"&#62;
    require(['jQuery'], function($) {
      $('#title').text('Title!');
    });
  &#60;/script&#62;
&#60;/body&#62;
&#60;/html&#62;
</code></pre>



## Why would you do that?

(Adds a ton of HTTP overhead)



No Sourcemaps! Reload to "recompile!"



and *If You Build It...*



<pre><code>
                 &#60;script src="js/jquery.min.js"&#62;&#60;/script&#62;

</code></pre>



## AMD beats Concatenation



## Hierarchy

* jquery
* app config
* app init
* module 1
* dependency util for module 2
* module 2



## Hierarchy with AMD

* AMD config
    - app
        + module 1
            * submodule a
            * submodule b
                - jQuery
            * common utility 1
        + module 2
            * jQuery
            * common utility 1
        + common utility 2



AMD hierarchy means
## Obvious Relationships

* Which modules are needed by which other?
* Which modules are commonly used across the app?
* Are poorly-structured relationships?

Note: This knowledge of your system can easily be lost with a traditional, linear/concat-based module inclusion model



### good for
# Testability



## Why care about Modules in tests?

> [module systems] makes dependencies explicit, and unit tests benefit from this property just as much as any application code.

[Effective Unit Testing with AMD](http://bocoup.com/weblog/effective-unit-testing-with-amd/), by Mike Pennisi



# AMD &amp; WP



# AMD <small>vs</small> WP



### WP has an existing
# plugin / script ecosystem



AMD *cannot* be the be-all and end-all



## Internal <small>vs</small> External
# Dependencies



### Registered Scripts
WordPress already contains a lot of built-in scripts:
```php
    // jQuery
    $scripts->add( 'jquery', false, array( 'jquery-core', 'jquery-migrate' ), '1.11.1' );
    $scripts->add( 'jquery-core', '/wp-includes/js/jquery/jquery.js', array(), '1.11.1' );
    $scripts->add( 'jquery-migrate', "/wp-includes/js/jquery/jquery-migrate$suffix.js", array(), '1.2.1' );

    // full jQuery UI
    $scripts->add( 'jquery-ui-core', '/wp-includes/js/jquery/ui/jquery.ui.core.min.js', array('jquery'), '1.10.4', 1 );
    $scripts->add( 'jquery-effects-core', '/wp-includes/js/jquery/ui/jquery.ui.effect.min.js', array('jquery'), '1.10.4', 1 );

    $scripts->add( 'jquery-effects-blind', '/wp-includes/js/jquery/ui/jquery.ui.effect-blind.min.js', array('jquery-effects-core'), '1.10.4', 1 );
    $scripts->add( 'jquery-effects-bounce', '/wp-includes/js/jquery/ui/jquery.ui.effect-bounce.min.js', array('jquery-effects-core'), '1.10.4', 1 );
    $scripts->add( 'jquery-effects-clip', '/wp-includes/js/jquery/ui/jquery.ui.effect-clip.min.js', array('jquery-effects-core'), '1.10.4', 1 );
    $scripts->add( 'jquery-effects-drop', '/wp-includes/js/jquery/ui/jquery.ui.effect-drop.min.js', array('jquery-effects-core'), '1.10.4', 1 );
    $scripts->add( 'jquery-effects-explode', '/wp-includes/js/jquery/ui/jquery.ui.effect-explode.min.js', array('jquery-effects-core'), '1.10.4', 1 );
    // And so on... you get the idea
```



## WordPress

should be used to enqueue built-in scripts,

and non-AMD/UMD dependencies



## Your module system

should pull in your own plugins, libraries,

utilities, wrappers, templates, *etc*



## How This Can Work:
# AMD WP Plugin Boilerplate

[View on Github](https://github.com/kadamwhite/js-plugin-boilerplate)

*use for learning, not production*



# Demo



## how it works



WordPress kicks things off
```php
// plugin.php
// ----------
wp_register_script(
    'require',
    $plugin_path . 'js/require.js',
    array()
);

wp_register_script(
    'js-plugin-boilerplate',
    $plugin_path . 'js/require-config.js',
    array(
        'jquery',
        'require'
    )
);
```



Tell Require where to find the scripts
```javascript
// require-config.js
// -----------------
require.config({
    baseUrl: REQUIRE_CONFIGURATION.baseUrl
});

// Load the application
require(['app']);
```
```php
// plugin.php
// ----------
wp_localize_script( 'js-plugin-boilerplate',
    'REQUIRE_CONFIGURATION',
    array( 'baseUrl' => $plugin_path . 'js/src' )
);
```



## Roll your own shims
*for other enqueued scripts*
```javascript
                           define(function() {
                             return window.jQuery;
                           });
```
<small>(Even for AMD-compatible libraries like jQuery!)</small>



Then it's AMD all the way down
```javascript
// app.js
// ------
define([
    'jquery',
    'module1',
    'module2'
], function( $, module1, module2 ) {
    'use strict';

    module1.init();

    console.log( '%s loaded', module2.name );

    $('.entry-title').text('Demo Loaded!');
});
```



## Pitfalls



### Require likes to run the show

and will not play nice with some libraries



## For example, Backbone

![Backbone error when loaded outside of Require](images/backbone-amd-error.png)




### From the Require docs:

> Be sure to load all scripts that call define() via the RequireJS API. Do not manually code script tags in HTML to load scripts that have define() calls




## AMD?
# No Can Do.

*It breaks WordPress.*



## But if you build it...



## RequireJS for Authoring,
## Single file for Deployment

![Require.JS build process with Grunt](../modular-javascript/images/require-build-process.png)



# Modular Code
### without side effects



Modules &rarr; Require.js optimizer &rarr; AMDClean &rarr; App.js



## Demo, continued



## What is a
# Module?



![Signs requesting small bills/exact change](images/AJSchuster-Desperation.jpg)

<small>*[AJ Schuster, "Desperation"](https://www.flickr.com/photos/ajschu/2581316304)*</small>

Note: Modules are like *always* having exact change



## Resources

- [RequireJS: A JavaScript Module Loader](http://gregfranko.com/requirejs-talk/), by Greg Franko
- [Using RequireJS In WordPress](http://kaidez.com/requirejs-wordpress/), by Kai Gittens
- [Writing Modular JavaScript](http://addyosmani.com/writing-modular-js/), by Addy Osmani
- [Understanding Require.js](http://www.sitepoint.com/understanding-requirejs-for-effective-javascript-module-loading/), on SitePoint
- The official [Require.js API documentation](http://requirejs.org/docs/api.html)
- [Browserify](http://http://browserify.org/)
- [es6-module-transpiler](https://github.com/square/es6-module-transpiler)

*Books:*

- JavaScript Patterns, a book by Stoyan Stefanov
- [JavaScript Design Patterns](http://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript), a free book by Addy Osmani



# Questions?

&nbsp;

Slides: [talks.kadamwhite.com/modular-js-pvd](http://kadamwhite.github.io/talks/2014/modular-javascript-pvd)

Me: [kadamwhite.com](http://kadamwhite.com) &bull; [@kadamwhite](http://twitter.com/kadamwhite)

Us: [Bocoup](http://bocoup.com) &bull; [@bocoup](http://twitter.com/bocoup)

&nbsp;

## *Thank You!*

