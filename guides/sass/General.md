[Back to Home](../../README.md)

Sass Style Guide
================

* Two spaces (no tabs) for indentation.
* Favor nested classes
* Create a "helpers.scss" file containing reusable functions.

Strict Selectors
----------------

Whenever possible, use strict CSS selectors as opposed to simple container selectors. E.g., the following is preferred...

```sass
div.content {
  > h1 {
  }
}
```

over this:

```sass
div.content {
  h1 {
  }
}
```

Naming
------

Always specify the element upon which a class or id relates to. For instance, `div#home` is always preferred to `#home`. Again, the stricter the rules, the better.


