# Modular
# JavaScript

*June 2014 &bull; WordCamp Chicago*

K.Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)



## Introductions



![Bob (Bocoup Logo)](../../2013/backbone-wordpress/images/bocoup-vertical-676.png)



## What is a
# Module?



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

No Dependencies



## We've all been here
![reference error: $ is not defined](images/reference-error.png)
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

<br>
*mo' HTTP Requests, mo' problems*



## Code in JS, deps in PHP? :(
<br>
```php
wp_enqueue_script( /*...*/, array( 'jquery' ), /*...*/);
```
<br>
> [A Module is] a **self-contained piece of code**...




## Code can be contained on
# many levels



### Digression:



# Module Patterns



## Patterns

Module Patterns are ways to structure code within a

JavaScript file, and to aid in structuring an application



## Basic Module

```javascript
MYAPP.utilities.array = (function () {
    return {
        inArray: function (needle, haystack) {
            // ...
        },
        isArray: function (a) {
            // ...
        }
    };
}());

```
<small>*from __JavaScript Patterns__, by Stoyan Stefanov*</small>



## Revealing Module pattern

```javascript
MYAPP.utilities.array = (function() {

    // private properties
    var array_string = "[object Array]",
    ops = Object.prototype.toString,

    // private methods
    inArray = function( haystack, needle ) {
        for (var i = 0, max = haystack.length; i < max; i += 1) {
            if ( haystack[ i ] === needle ) {
                return i;
            }
        }
        return −1;
    },
    isArray = function( a ) {
        return ops.call( a ) === array_string;
    };
    // end var

    // revealing public API
    return {
        isArray: isArray,
        indexOf: inArray
    };
}());
```
<small>*from __JavaScript Patterns__, by Stoyan Stefanov*</small>



## Module with Global Dependencies

```javascript
MYAPP.utilities.module = (function( app, global ) {
    // references to the global object
    // and to the global `app` namespace object
    // are now localized
}( MYAPP, this ));
```
<small>*from __JavaScript Patterns__, by Stoyan Stefanov*</small>



## Module augmenting a global namespace
```javascript
window.wp = window.wp || {};

(function($){
    var Attachment, Attachments, Query, PostImage, compare, l10n, media;

    /**
     * wp.media( attributes )
     *
     * @param  {object} attributes The properties passed to the main media controller.
     * @return {wp.media.view.MediaFrame} A media workflow.
     */
    media = wp.media = function( attributes ) {
        // ..
    };

    // ...
}(jQuery));
```
<small>*from WP's media-models.js*</small>



## Resources

![Stoyan Stefanov - JavaScript Patterns](images/stefanov-js-patterns.gif)
![Addy Osmani - JS Design Patterns](images/osmani-js-design-patterns.gif)

<small>(Addy's book is [available online for free](http://addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript))



## 1/2 of the way there



## Module *Authoring*

Patterns give us a consistent and repeatable way

of declaring modular intent...



## Module *Transport*

But how does a request for a module in a JavaScript

file get connected to a filesystem call?



Still fighting huge files



We need to be able to
## Author modules
as separate files, then
## release modules
as enqueue'able, built scripts



# Module Systems



## AMD vs CommonJS



# CommonJS
## (Node is a variant)



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



## require()
```javascript
require([ 'cart', 'store', 'store/util' ],
function(  cart,   store,   util ) {
    //use the modules as usual.
});
```
<small>*from the Require.js [API docs](http://requirejs.org/docs/api.html#jsfiles)*</small>



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



*Simplified CommonJS Wrapper*
```javascript
define(function( require, exports, module ) {
  'use strict';

  var Grammar = require( './grammar' );
  var Tokenizer = require( './tokenizer' );
  var Tree = require( './tree' );
  var Compiler = require( './compiler' );
  // ...
  module.exports = Combyne;
});
```
<small>*from [Combyne.js](https://github.com/tbranyen/combyne), by Tim Branyen*</small>



## A brief glimpse of
# the future



## ES6 Modules

The next version of JavaScript will have native modules...

...but they won't be in browsers for a while yet.



## Transpiling ES6

You can use ES6 modules now if you use a "transpiler"

like Square's [es6-module-transpiler](https://github.com/square/es6-module-transpiler), like [Ember App Kit](http://iamstef.net/ember-app-kit/guides/using-modules.html) does:
```javascript
var IndexRoute = Ember.Route.extend({
  model: function() {
    return ['red', 'yellow', 'blue'];
  }
});

// Ought to look something like this:
export default IndexRoute;
```



## We're going to focus on AMD

because it's designed for the browser

<small><br>*but we'll return to the rest later*</small>



## AMD Structure in jQuery

jQuery's main `jquery.js` file:
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



## "./core",
First dependency creates jQuery object,  
adds core functionality, returns `jQuery`
```javascript
define([
    "./var/arr",
    "./var/slice",
    "./var/concat",
    "./var/push",
    "./var/indexOf",
    "./var/class2type",
    "./var/toString",
    "./var/hasOwn",
    "./var/support"
], function( arr, slice, concat, push, indexOf, class2type, toString, hasOwn, support ) {

var
    // Use the correct document accordingly with window argument (sandbox)
    document = window.document,

    version = "@VERSION",

    // Define a local copy of jQuery
    jQuery = function( selector, context ) {
        // The jQuery object is actually just the init constructor 'enhanced'
        // Need init if jQuery is called (just allow error to be thrown if not included)
        return new jQuery.fn.init( selector, context );
    },

    // ...Define jQuery.fn, jQuery.extend, etcetera
    // ...
    // ...

return jQuery;
});
```



## "./data"
Require core, extend it with data methods
```javascript
define([
    "./core",
    "./var/rnotwhite",
    "./core/access",
    "./data/var/data_priv",
    "./data/var/data_user"
], function( jQuery, rnotwhite, access, data_priv, data_user ) {

var rbrace = /^(?:\{[\w\W]*\}|\[[\w\W]*\])$/,
    rmultiDash = /([A-Z])/g;

function dataAttr( elem, key, data ) { /* ... */ },

jQuery.extend({
    hasData: function( elem ) { /* ... */ },

    data: function( elem, name, data ) { /* ... */ },

    removeData: function( elem, name ) { /* ... */ },

    // ...
});

jQuery.fn.extend({
    data: function( key, value ) { /* ... */ },

    removeData: function( key ) { /* ... */ },
});

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
    require(["jQuery"], function($) {
      $('#title').text('Title!');
    });
  &#60;/script&#62;
&#60;/body&#62;
&#60;/html&#62;
</code></pre>



## Why would you do that?

(Adds a ton of HTTP overhead)



*If You Build It...*

![Require.JS build process with Grunt](images/require-build-process.png)



## Why would you do that?

(What benefit does this have over lots of concatenated scripts?)



## Hierarchy

* jquery
* app config
* app init
* module 1
* dependency util for module 2
* module 2



## Hierarchy with AMD

* amd config
    - app
        + module 1
            * submodule a
            * submodule b
                - jquery
            * common utility I
        + module 2
            * jquery
            * common utility I
        + common utility II



AMD hierarchy means
## Obvious Relationships

* Which modules are needed by which other?
* Which modules are commonly used across the app?
* Are poorly-structured relationships?



This knowledge of your system can easily be  
lost with a traditional, linear/concat-based  
module inclusion model



# AMD &amp; WP



AMD cannot be the be-all and end-all in WP:  
It has to exist within the existing
## plugin/script ecosystem



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



If we included these in our require process,

stuff would probably break



## WordPress

should be used to enqueue built-in scripts



## Your module system

should pull in any non-bundled plugins, libraries, utilities, wrappers, templates, *etc*



## How This Can Work:
# AMD WP Plugin Boilerplate

[View on Github](https://github.com/kadamwhite/js-plugin-boilerplate)

*This is a work-in-progress, and may break things!*
*<br>use for learning, not production*



# Testing



## Why care about Modules in tests?

> [module systems] makes dependencies explicit, and unit tests benefit from this property just as much as any application code.

[Effective Unit Testing with AMD](http://bocoup.com/weblog/effective-unit-testing-with-amd/), by Mike Pennisi



## More to come!

Code Coverage, dependency graphs, *etc*


Resources I'm exploring to add/comment upon:

* [Madge](https://www.npmjs.org/package/madge)
* [Blanket.js](http://blanketjs.org/)
* [Dependo](http://kenneth.io/blog/2013/04/01/visualize-your-javaScript-dependencies-with-dependo/)
* [Universal Module Definition (UMD)](https://github.com/umdjs/umd)



## What is a
# Module?



> A piece of code that can depend on something and/or return something else



## Resources

**If you know of good, beginner-friendly resources, please share!**

[Using RequireJS In WordPress](http://kaidez.com/requirejs-wordpress/), by Kai Gittens

[Writing Modular JavaScript](http://addyosmani.com/writing-modular-js/), by Addy Osmani

[Blog articles](http://unscriptable.com) and [presentations](http://unscriptable.com/code/Using-AMD-loaders) by John Hann ([@unscriptable](https://twitter.com/unscriptable))

[Understanding Require.js](http://www.sitepoint.com/understanding-requirejs-for-effective-javascript-module-loading/), on SitePoint

[Require.js API documentation](http://requirejs.org/docs/api.html)



# Questions?

&nbsp;

Slides: [talks.kadamwhite.com/modular-javascript](http://kadamwhite.github.io/talks/2014/modular-javascript)

Me: [kadamwhite.com](http://kadamwhite.com) &bull; [@kadamwhite](http://twitter.com/kadamwhite)

Us: [Bocoup](http://bocoup.com) &bull; [@bocoup](http://twitter.com/bocoup)

&nbsp;

## *Thank You!*

