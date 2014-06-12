# Modular
# JavaScript

*June 2014 &bull; WordCamp Chicago*

K.Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)



## Introductions



![Bob (Bocoup Logo)](../../2013/backbone-wordpress/images/bocoup-vertical-676.png)



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



## Using jQuery via Require.js

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





# Questions?

&nbsp;

Slides: [talks.kadamwhite.com/modular-javascript](http://kadamwhite.github.io/talks/2014/modular-javascript)

Me: [kadamwhite.com](http://kadamwhite.com) &bull; [@kadamwhite](http://twitter.com/kadamwhite)

Us: [Bocoup](http://bocoup.com) &bull; [@bocoup](http://twitter.com/bocoup)

&nbsp;

## *Thank You!*

