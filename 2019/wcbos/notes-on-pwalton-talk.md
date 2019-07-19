# Philip Walton talk notes



Can queries resize to a div element, instead of screen?

gallagher proposed component-level queries

jonathan neal proposed syntax

ian storm taylor - media queries are a hack

"anti-modular" because they couple component definitions to site layout

Proposed "element queries"

Tab Completion, element queries blog post. Summarizes problems. De facto resp from CSS WG

Filament group "working around element queries"

element query polyfills: each polyfill created their own syntax. lots of future/cross-compatibility risk.

RICG use cases and requirements for element queries.

- work was met w/ a lot of resistence from CSSWG and browser vendors
- Mat marquis article, COntainer Queries: once more unto the breach

Container Queries less problematic than element, but still a problem

chris coyier: over 50% of element queries would be obviated

jehl: media queries wouldn't matter at all

So, why don't they exist?

- Jeremy Keith: browser vendors seem to ignore devs
- browser problems:
  - infinite loops
  - they break the cascade
    - browsers go from root element in HTML down; css props are inherited
    - Once hierarchy is established, style cascade is computed
    - Then layout is calculated. all the rectangles are calculated.
    - Children can impact parent heights: you need to construct the entire box tree, have all the styles, and then let things shake out
    - Because style has to be thoroughly known before the layout, you end up with a feedback loop between the styles and the layout. Layout causes new style rules to be applied, which goes against the grain of CSS computation, and is very slow.
  - Browsers therefore have a good argument
- browsers have been looking at alternatives
  - Chrome CSS Containment: mark a part of the page as independent from other parts, to avoid the circularity issue. You could mark an element as being unaffected by child element sizes.
  - Chrome: ResizeObserver
    - Performantly monitor resize events on an element
- And, we can actually style containers... with classes. State classes allow us to specify themes, active states, etc.
- (Goes through Responsive Container approach)
- Technique does not break without JS. Base styles still apply. Your site will render. This is progressive enhancement.
- We can also use CSS to guarantee that even hidden-until-observed elements will be displayed.
- Dynamically-generated DOM?
  - Hook into the component lifecycle.
    - fire connectedCallback
  - Garbage collection will handle unobserving removed elements
- Benefits
  - performant
  - easy
  - doesn't require a JS framework or build tool
  - has no-js fallback
- Future
  - Element query work has been started again -- but not moved in over a year https://wicg.github.io/cq-usecases/
  - 