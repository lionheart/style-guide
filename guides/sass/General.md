[Back to Home](../../README.md)

Sass Style Guide
================

* Two spaces (no tabs) for indentation.
* Favor nested classes
* Create a "helpers.scss" file containing reusable functions.

Strict Selectors
----------------

Whenever possible, use strict CSS selectors as opposed to simple container selectors. E.g., the following is *bad*:

```sass
div.content {
  h1 {
  }
}
```

But this is good:

```sass
div.content {
  > h1 {
  }
}
```

Naming
------

Always specify the element upon which a class or id relates to. For instance, `div#home` is always preferred to `#home`. Again, the stricter the rules, the better.

## Centering Elements

### Simple text

`text-align: center` will pretty much always work.

### Images

For images, the best route is usually to make the image a block element and specify `margin: 0 auto;`.

```sass
img#example {
    /* ... */
    display: block;
    margin: 0 auto;
}
```

### Block Elements

Specify `margin: 0 auto;` and provide a width.

```sass
div#example {
    /* ... */
    margin: 0 auto;
    width: 100px;
}
```

### Inline Elements

At this point, we have to resort to desperate measures. We use two nested classes (`center-outer` and `center-inner`) and wrap our element inside of them.

```sass
div.center-outer {
  float:right;
  right:50%;
  position:relative;

  div.center-inner {
    float:right;
    right:-50%;
    position:relative;
  }
}
```

And the corresponding HTML (assume `span` is an element with `display: inline-block;`).

```html
<div class="center-outer">
  <div class="center-inner">
  </div>
</div>
```

