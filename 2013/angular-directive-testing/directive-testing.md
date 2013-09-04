# Unit Testing Directives

AngularJS Boston, September 2013

K.Adam White &bull; [@kadamwhite](https://twitter.com/kadamwhite)

[@Bocoup](http://bocoup.com/)



![Bob (Bocoup Logo)](/talks/common/images/bocoup-vertical-676.png)



## AngularJS
# &hearts;
## Unit Tests



## Testing as a 1st-class citizen

DI & mocks, Karma



## Directives == Markup



## Unit Testing Markup

> What is a unit anyway? In the best case, it is a pure function &hellip; but most of the time you need to deal with side effects, which here means **DOM manipulations**.

<small>~ [Introduction to Unit Testing](http://qunitjs.com/intro/), qunitjs.com</small>



## Not Testing Directives

leads to

> a sad life of untested code full of creepy bugs

<small>~ [Vojta](https://github.com/vojtajina/ng-directive-testing)</small>



## So test 'em!



## What to Test: Compilation

Does the directive render?

Is the template loaded?



## What to Test: Linking

Are scope properties correctly bound?

Does transclusion do its wacky thing?



## What to test: Side Effects

Are plugins initialized?

Are listeners bound? Do they fire?

Are messages sent/received?



### Today We're going to look at 
# Two Common Issues
### with directive  unit tests



## I. Avoid the document

> &hellip;we don’t append the DOM structure to the document. **That makes the tests faster**, because browser does not have to render it.

<small>~ [Vojta](https://github.com/vojtajina/ng-directive-testing)</small>



```javascript
var $element = angular.element(
  '<div><my-directive></my-directive></div>'
);

$compile( $element )( scope );

expect( $element.find('.widget').first().text() )
  .toBe('AMAZING!');
```



## That Said,
> &hellip;we don’t append the DOM structure to the document&hellip; **unless it’s necessary** (eg. you need to know some computed property of some DOM element)



## Working with jQuery Plugins

Some jQuery plugins may fail to load

if not inserted into the document



### *e.g.* SlickGrid

Needs to compute styles for instantiation

Can't do that if it's not inside the body



**$element.prependTo( document.body )**
```javascript
it('should create a SlickGrid', inject(function( $compile ) {

  // [set up scope properties & variables]

  $grid = $compile(
    '<slick-grid config="testConfig" data="testData"></slick-grid>'
  )(scope);

  $grid.prependTo( document.body );
  scope.$digest();

  expect( $grid.find('.slick-header').length ).toBe(1);
  // Etcetera

}));
```



## II. External Templates

If the template's more than one

line of HTML, it goes in a partial



## Nobody likes this

```javascript
template:
  '<div class="tabbable">' +
    '<ul class="nav nav-tabs">' +
      '<li ng-repeat="pane in panes" ' +
          'ng-class="{active:pane.selected}">'+
        '<a href="" ng-click="select(pane)">{{pane.title}}</a>' 
      '</li>' +
    '</ul>' +
    '<div class="tab-content" ng-transclude></div>' +
  '</div>',
```



## Much better

```javascript
templateUrl: 'tpl/tabs.html',
```



But then Karma's all like

<br />

## Error: Unexpected request:
## GET tpl/tabs.html
### No more request expected



# :(



# Pre-Process
## Your Partials



npm install --save-dev

### karma-ng-html2js-preprocessor



## Tell Karma where to
## find your templates

in your karma.conf.js

```javascript
preprocessors: {
  'tpl/**/*.html': 'ng-html2js'
},
```



## Require templates
## as modules in tests

```javascript
describe('tabs', function() {
  var elm, scope;
  beforeEach(module('tabs'));

  // load the templates
  beforeEach(module('tpl/tabs.html', 'tpl/pane.html'));

  // GET requests for partials will
  // now return the compiled template
  // from $templateCache

});
```
<small>[vojtajina/ng-directive-testing](https://github.com/vojtajina/ng-directive-testing/blob/master/karma.conf.js)</small>



# :)



## Gotcha: Absolute template paths

If you're at `http://myapp.com/some/route/`,

you need to use absolute URLs for templates:

```javascript
templateUrl: '/some/absolute/path.html',
```



## But by default

html2js registers the template with a relative path:
```javascript
beforeEach( module('/some/absolute/path.html') );
// Error: No module: /some/absolute/path.html
```




## And if you omit the `/`,

the module loads but you'll be staring at
```javascript
beforeEach( module('some/absolute/path.html') );
// Error: Unexpected request: GET /some/absolute/path.html
```



## The clunky solution:
```javascript
beforeEach(inject(function($templateCache) {
    var getTemplate = $templateCache.get;

    // Wrap $templateCache.get to strip leading slashes off templateUrls
    // (Karma's html2js pre-processor registers templates without the leading /)
    $templateCache.get = function(key) {
        if( key.substr(0, 1) === '/' ) {
            key = key.substr(1);
        }
        return getTemplate(key);
    };
}));
```



# :-|



## Configuring module names

Add or remove prefixes to make Karma's

module names match the requested templateUrl
```javascript
    ngHtml2JsPreprocessor: {
      // prepend this to the path
      prependPrefix: '/'

      // stripPrefix also exists
    }
```
<small>~ [karma-ng-html2js-preprocessor configuration](https://github.com/karma-runner/karma-ng-html2js-preprocessor#configuration)</small>



## <span class="nocap">cacheIdFromPath:<span>

```javascript
module.exports = function(config) {
  config.set({
    ngHtml2JsPreprocessor: {

      // Define a custom transform function
      cacheIdFromPath: function(filepath) {
        return '/' + cacheId;
      }

    }
  });
};
```
for when you need more custom transformations



# :)



## All together now!



karma.config.js
```javascript
// Karma configuration file
// See http://karma-runner.github.io/0.10/config/configuration-file.html
module.exports = function(config) {
  config.set({
    basePath: '',

    frameworks: ['jasmine'],

    // list of files / patterns to load in the browser
    files: [
      // libraries
      'lib/jquery-1.8.1.min.js',
      'lib/angular.js',
      'lib/angular-mocks.js',

      // our app
      'js/*.js',

      // tests
      'test/*.js',

      // templates
      'tpl/*.html'
    ],

    // generate js files from html templates
    preprocessors: {
      'tpl/*.html': 'ng-html2js'
    },

    ngHtml2JsPreprocessor: {
      // prepend this to the path
      prependPrefix: '/'
    },

    autoWatch: true,
    browsers: ['Chrome']
  });
};
```



tabSpec.js

```javascript
describe('tabs', function() {
  var elm, scope;

  // load the tabs code
  beforeEach(module('tabs'));

  // load the templates
  beforeEach(module('/tpl/tabs.html', '/tpl/pane.html'));

  beforeEach(inject(function($rootScope, $compile) {
    elm = angular.element(
      '<div>' +
        '<tabs>' +
          '<pane title="First Tab">' +
            'first content is {{first}}' +
          '</pane>' +
          '<pane title="Second Tab">' +
            'second content is {{second}}' +
          '</pane>' +
        '</tabs>' +
      '</div>');

    scope = $rootScope;
    $compile(elm)(scope);
    scope.$digest();
  }));

  // Actual tests go here
});
```



## Too Many Templates?



Angular encourages you to create many directives
```
beforeEach( module(
  '/app/directives/slickgrid/slickgrid-directive.html',
  '/app/directives/slickgrid/partials/bulkFieldEditor.html',
  '/app/directives/slickgrid/partials/bulkEditor.html',
  '/app/directives/slickgrid/partials/multiFilter.html',
  '/app/directives/slickgrid/partials/checkboxFilter.html',
  '/app/directives/slickgrid/partials/numericRangeFilter.html',
  '/app/directives/slickgrid/partials/dateRangeFilter.html',
  '/app/directives/slickgrid/partials/exclusionFilter.html'
) );
```
Which can be&hellip; frustrating, at times



## One Module to Rule Them All

In karma.conf.js:
```javascript
ngHtml2JsPreprocessor: {
  // Create a single module containing templates from all
  // the files, so you can load them all with module('foo')
  moduleName: 'slickgridTemplates'
}
```
then in your tests:
```javascript
beforeEach( module('slickgridTemplates') );
```



## Recap



### Be aware of plugin DOM dependencies

and append directive markup to `body` as needed



### Precompile templates with html2js

so that they can be easily required in tests



### Configure compiled template module names

to match GET requests to the right template



### Group templates for convenience

as needed or desired



<small>`var $talk = $compile('<lightning-talk></lightning-talk>')( scope );`</small>
#### <span class="nocap">`expect( $talk ).toBe('over');`</span>

<br />

------

<br />

Slides: [talks.kadamwhite.com/directive-testing](http://kadamwhite.github.io/talks/2013/angular-directive-testing/)

<small>[@kadamwhite](http://twitter.com/kadamwhite) &bull; [@bocoup](http://twitter.com/bocoup)</small>

<br />

------

Resources:
<small>

* [Karma](http://karma-runner.github.io/) test runner
* [karma-ng-html2js-preprocessor](https://github.com/karma-runner/karma-ng-html2js-preprocessor) on Github
* [ng-directive-testing](https://github.com/vojtajina/ng-directive-testing) example on Github

</small>