# Spice Helpers (Handlebars)
<!--
<span class="summary">Spice handlebars helpers</span>
<span class="summary-text" markdown="1">
List of Spice specific Handlebars helpers:
- [concat](https://duck.co/duckduckhack/spice_handlebars_helpers/#concat): Concatenates all the elements in a collection
- [condense](https://duck.co/duckduckhack/spice_handlebars_helpers/#condense): Shortens a string
- [stripHTML](https://duck.co/duckduckhack/spice_handlebars_helpers/#stripHTML): Strips HTML tags/elements from text
- [loop](https://duck.co/duckduckhack/spice_handlebars_helpers/#loop): Counts from zero to the value of `context`
- [each](https://duck.co/duckduckhack/spice_handlebars_helpers/#each): Extends Handlebars' built-in `{{each}}` lets you specify optional inclusive first and last indices
- [keys](https://duck.co/duckduckhack/spice_handlebars_helpers/#keys): Iterates over the properties of an object and provides a new object containing the "key" and "value" for each
- [include](https://duck.co/duckduckhack/spice_handlebars_helpers/#include): Loads the specified Handlebars template and applies it with the current context
- [plural](https://duck.co/duckduckhack/spice_handlebars_helpers/#plural): Returns the value of `context` and appends the singular or plural form of the specified word
- [numFormat](https://duck.co/duckduckhack/spice_handlebars_helpers/#numFormat): Delimits a number or string with multiple numbers, using commas or given delimiter
- [imageProxy](https://duck.co/duckduckhack/spice_handlebars_helpers/#imageProxy): Rewrite a URL as a DuckDuckGo image redirect
- [ellipsis](https://duck.co/duckduckhack/spice_handlebars_helpers/#ellipsis): Shortens a string by removing words until string length is <= `limit` and appends an ellipsis ('...') to the output
- [trim](https://duck.co/duckduckhack/spice_handlebars_helpers/#trim): Removes leading and trailing spaces from text

For the built-in helpers included with Handlebars see: [Handlebars Helpers](http://handlebarsjs.com/#helpers)
</span>
###{{#concat}}

**Block Helper**

Concatenates all the elements in a collection

An optional item separator can be appended to
each item and an optional conjunction can be
used for the last item.

Example:

```html
{{#concat context sep="," conj="and"}}
{{this}}
{{/concat}}
```

when `context` is:
- `['a']`           returns:  `a`
- `['a', 'b']`      returns:  `a and b`
- `['a', 'b', 'c']` returns:  `a, b and c`

**Parameters**

**sep**:  *string*,  **[optional]** Item separator. Default: `''`

**conj**:  *string*,  **[optional]** Final separator, precedes last item. Default: `''`


###{{#condense}}

**Block Helper**

Shortens a string

An optional maximum string length can be provided if preferred.

Example:

`{{condense myString maxlen="135" truncation="..."}}`

This will output the value of `myString` up to a maximum of 135 characters
(not including the length of the truncation string) and then append
the truncation string to the output

**Parameters**

**maxlen**:  *number*,  **[optional]** Maximum allowed string length. Default: `10`

**fuzz**:  *number*,  The allowable deviation from the maxlen, used to allow a sentence/word to complete if it is less than fuzz characters longer than the maxlen

**{string**,  truncation **[optional]** The truncation string. Default: `'...'`


###{{#stripHTML}}

**Block Helper**

Strips HTML tags/elements from text

Example:

`{{#stripHTML stringWithHTML}}Here is my string: {{this}}{{/stripHTML}}`


###{{#loop}}

**Block Helper**

Counts from zero to the value of `context` (assuming `context` is a **number**)
applying the content of the block each time

Note: A maximum of 100 loops is allowed.

Example:

```html
{{#loop star_rating}}
<img src="{{star}}" class="star"></span>
{{/loop}}
```


###{{#each}}

**Block Helper**

Extends Handlebars' built-in `{{each}}`
lets you specify optional inclusive first and last indices
to iterate between

Example:

`{{#each myArray from="2" to="5"}} ... {{/each}}`

This will limit the iteration to array indices 2, 3 and 4.

If `to` is not given, defaults to array (or object) length:

`{{#each myArray from="2"}} ... {{/each}}`

will skip the first two items

If `from` is not given, defaults to 0:

`{{#each myArray to="5"}} ... {{/each}}`

will only do the first five items

**Parameters**

**from**:  *number*,  **[optional]** Index to start from. Default: `0`

**to**:  *number*,  **[optional]** Index to end on. Default: array/object length


###{{#keys}}

**Block Helper**

Iterates over the properties of an object and provides
a new object containing the "key" and "value" for each

Example:

```html
{{#keys myObject}}
{{key}} : {{value}}
{{/keys}}
```


###{{include}}

Loads the specified Handlebars template and applies it with
the current context

Note: There is no recursive cycle detection! **Be careful**.

Example:

`{{include ../myTemplate}}`

Applies the template `myTemplate` using `this` as the data context

`{{include ../myTemplate with="x"}}`

Applies the template `myTemplate` using `this.x` as the data context.
Identical to:

`{{#with x}} {{include ../template}} {{/with}}`

**Parameters**

**with**:  *string*,  **[optional]** Context to use when including the template. Supports simple dot paths.


###{{plural}}

Returns the value of `context` (assuming `context` is a **number**)
and appends the singular or plural form of the specified word,
depending on the value of `context`

Example:

`{plural star_rating singular="star" plural="stars"}}`

Will produce:
- `{{star_rating}} star`  if the value of `star_rating` is `1`, or
- `{{star_rating}} stars` if `star_rating` > `1`

**Parameters**

**singular**:  *string*,  Indicates the singular form to use

**plural**:  *string*,  Indicates the plural form to use

**delimiter**:  *string*,  **[optional]** Format the number with the `numFormat` helper


###{{numFormat}}

Delimits a number or string with multiple numbers,
using commas or given delimiter

Note: This supports integers and decimal numbers.

Credit: This function was borrowed from
http://cwestblog.com/2011/06/23/javascript-add-commas-to-numbers/

Example:

```html
{{numFormat num}}
{{numFormat num delimiter="." }}
```

**Parameters**

**delimiter**:  *string*,  **[optional]** The delimiter string. Default: `','`

###{{imageProxy}}

Rewrite a URL as a DuckDuckGo image redirect

Example:

`{{imageProxy imageURL}}`

produces: `/iu/?u={{imageURL}}`


###{{trim}}

Removes leading and trailing spaces from text

Example:

`{{trim stringWithSpaces}}`


###{{ellipsis}}

Shortens a string by removing words until string length is <= `limit` and
appends an ellipsis ('...') to the output

Note: It automatically appends any closing tag if one is missing.

Example:

`{{ellipsis title 50}}`

**Parameters**

**text**:  *string*,  text to shorten

**limit**:  *number*,  maximum length of shortened string