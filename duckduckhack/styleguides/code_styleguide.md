# DuckDuckHack - Code Style Guide

In any large open-source project, maintainability is required, so a set of style rules is a must to keep clean, readable code.

## General

+ All DuckDuckHack code should be formatted to tabs of four spaces. If you need to change a file to fix this, keep that change in its own commit.
+ Comments are a Good Thing<sup>TM</sup>. Let's have more of those!
+ Commit messages should be concise and informative. They are generally in the form `InstantAnswer: changed colors to match mockup`. If the specific commit fixes a bug on GitHub, note that by saying `fixes #123`, where `123` is the issue number (this automatically closes the issue when your pull request is merged). 

## Javascript
**We generally adhere to Crockford's Code Convetions: http://javascript.crockford.com/code.html** Most importantly:

+ Be sure to follow the closure structure listed [here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_basic_tutorial.md#npm-spice---frontend-javascript). The canonical structure is as follows: 

```javascript
(function(env){
    "use strict";
    env.ddg_spice_name = function(){
        ...
        Spice.add({
            ...
        });
    }

    // private functions here
    function doSomething(){
        ...
    }

    // handlebars helpers here
    Spice.registerHelper("name", function(){
        ...
    });
}(this));
```

+ We use semicolons everywhere for consistency.
+ Use the ["One True Brace Style"](https://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS) (opening brace on the same line)
+ Use `{}` instead of `new Object()`, and `[]` instead of `new Array()`.
+ Use `===` and `!==` instead of `==` and `!=`. [Why?](http://stackoverflow.com/a/359509/1998450)
+ We're using ECMAScript's [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode?redirectlocale=en-US&redirectslug=JavaScript%2FReference%2FFunctions_and_function_scope%2FStrict_mode), so you'll need to declare every variable with `var`. Chaining these like so is encouraged, with one line per variable.

```javascript
var foo = 1,
    bar = true;
```

+ We try to support all modern browsers, including IE 8. As such, please remember the following:
    + Trailing commas in objects will not work.

    ```javascript
    var foo = {
        a: 'b',
        c: 42, //<-- BAD
    };
    ```
    
    + `Array.prototype.map()` and `Array.prototype.forEach()` will not work. Consider using the jQuery equivalents [`$.map()`](http://api.jquery.com/jQuery.map/) and [`$.each()`](http://api.jquery.com/jQuery.each/).
+ Don't modify a native object's prototype, as this takes global effect. Consider using local functions instead.
+ Objects are better defined all at once:

```javascript
//prefer this:
var foo = {
    a: 'b',
    c: 42
};

//over this:
var bar = {};
bar.a = 'b';
bar.c = 42;
```

+ If you're using a jQuery selector many times, it's best to assign it to a variable.

```javascript
// prefer this:
var $text_element = $('#text_element');
$text_element.show();
$text_element.html('abc');

//over this:
$('#text_element').show();
$('#text_element').html('abc');
```

## Handlebars

The goal here is to ensure the Handlebars template is easy to read and understand. Please:

+ put nested elements on new lines:

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

+ All CSS should be "namespaced" with the container element (usually `.zci--spicename` for Spices and `.zci--answer` for Goodies).

```css
.zci--stopwatch .spice-pane {
    ...
}
```

+ Put selectors on multiple lines.

```css
.zci--stopwatch .spice-pane,
.zci--stopwatch .spice-pane-right {
    ...
}
```

+ Please no inline CSS. For Goodies, we prefer a separate share file that can be slurped in.

## Perl

(This section is coming soon! Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)