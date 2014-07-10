# DuckDuckHack - Code Style Guide

## Javascript

**We generally adhere to Crockford's Code Convetions: http://javascript.crockford.com/code.html**

But most importantly:

- use 4 spaces, *not* tabs
- use semicolons (;)
- use the ["One True Brace Style"](https://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS) (opening brace on the same line)
- use `{}` instead of `new Object()`
- use `[]` instead of `new Array()`
- use `===` and `!==` instead of `==` and `!=`
- declare multiple variables with one `var` and each variable on a new line:

```javascript
// good
var foo,
    bar,
    baz;

// bad
var foo, bar, baz
```

## Handlebars

The goal here is to ensure the Handlebars template is easy to read and understand. Please:

- put nested elements on new lines:

```html
<ul>
    <li>
        <a href="#">link text</a>
    </li>
    <li>
        <div>
            <a href="#">other link text</a>
        </div>
    </li>
</ul>
```

## CSS

(This section is coming soon! Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

## Perl

(This section is coming soon! Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)