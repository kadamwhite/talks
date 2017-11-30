

---
<!-- .slide: class="full-height" data-background="url('./images/dorkq.png')" data-background-position="center" data-background-size="cover" data-transition="none" -->

???

(visual gag, proceed to next slide)



---

### _Browserify Transforms_

or the command line&hellip;

```
browserify -t coffeeify \
           -t [ browserify-ngannotate --ext .coffee --bar ] \
           index.coffee > index.js
```
