# Spice JavaScript API Reference

## DDG Namespace


### get_query_encoded()

Provides the value of `DDG.get_query` as a URIEncoded string

Note: The query is trimmed (i.e. no leading or trailing spaces) and
has any extra spaces within the query removed


### get_query()

Provides the search query, as displayed in the search box

Note: The query is trimmed (i.e. no leading or trailing spaces) and
has any extra spaces within the query removed


### get_is_safe_search()

Indicates if "safe search" is on, for the current query

**Returns**

*boolean*,  Either `1` or `0` (on/off)


### get_asset_path(spice_name, asset)

Provides the path to the given asset, for the specified Spice Instant Answer

Example:

`DDG.get_asset_path('quixey', 'quixey_logo.png')` -> `'/share/spice/quixey/1234/quixey_logo.png'`

**Parameters**

**spice_name**:  *string*,  The name of the Spice (this gives us the correct `/spice/share` subdirectory)

**asset**:  *string*,  The filename of the asset, including extension


### getRelevants(p)

Provides an array of relevant strings, given an input array of comparator strings

Note: This is a shortcut to running `isRelevant()` against an array and collecting only the relevant results

Example:

```javascript
var relevants = DDG.getRelevants({
    num:        10, // the first 10 relevant candidates will be returned
    candidates: ['is this relevant', 'is this one relevant', 'how about this one', ... ], //candidate strings
    skipArray:  ['a', 'list', 'of', 'words'], //words to ignore in comparison
    strict:     false
});
```
Only the `candiates` array is required, the other parameters are optional. `num` defaults to `candidates.length`

**Parameters**

**p**:  *object*,  An object containing an array of candidate strings and other optional parameters to be passed along to `DDG.isRelevant`, including: `num` - the maximum amount of results to return, `skipArray`, `minWordLength`, and `strict`


### isRelevant(candidate, skipArray, minWordLength, strict)

Determines if the candidate string is relevant to **the search query**

**Parameters**

**candidate**:  *string*,  The string to be checked for relevancy

**skipArray**:  *array*,  **[optional]** An array of words (usually the trigger words) that should not be considered in determining the candidate string's relevancy

**minWordLength**:  *number*,  **[optional]** The minimun length for any words to be considered in the comparison (used to ignore small words like "to", "and", "is", "a", etc.), Default: `4`

**strict**:  *boolean*,  **[optional]** Turns on stricter relevancy checking, by switching candidate and comparator strings, Default: `0`


### stringsRelevant(s1, s2, skipArray, minWordLength, strict)

Determines if the candidate string is relevant to the given comparator string

**Parameters**

**s1**:  *string*,  The string to be checked for relevancy

**s2**:  *string*,  The string to be compared against

**skipArray**:  *array*,  **[optional]** An array of words (usually the trigger words) that should not be considered in determining the candidate string's relevancy

**minWordLength**:  *number*,  **[optional]** The minimun length for any words to be considered in the comparison (used to ignore small words like "to", "and", "is", "a", etc.), Default: `4`

**strict**:  *boolean*,  **[optional]** Turns on stricter relevancy checking, by switching candidate and comparator strings, Default: `0`


### parse_link(string, wanted)

Parses a string containing an anchor tag, ('<a href="URL">text</a>'), and returns the URL or text
as indicated

Note: If more than one anchor tag exists in the string, the first will be parsed

Example:

`str = '<a href="https://mywebsite.com">Click here!</a> to see my website.'`

- `DDG.parse_link(str)` -> `'https://mywebsite.com'`
- `DDG.parse_link(str, 'text')` -> `'Click here!'`
- `DDG.parse_link(str, 'rest')` -> `' to see my website.'`

**Parameters**

**string**:  *string*,  A string containing an anchor tag

**wanted**:  *string*,  **[optional]** The piece of the link to return Default: `'url'`


### getDateFromString(date)

Provides a JavaScript `Date()` object for the given Date string

**Parameters**

**date**:  *string*,  Date string in UTC format with time (yyyy-mm-ddThh:mm:ss) or without (yyyy-mm-dd)


### strip_html(html)

Removes HTML tags/characters from a string

**Parameters**

**html**:  *string*,  String containing HTML

### getOrdinal(number)

Provides the proper ordinal noun for a given number

Example:

`DDG.getOrdinal(456)` -> `'456th'`

**Parameters**

**number**:  *number*,  The number you need an ordinal for


### strip_non_alpha(str)

Removes Non-Alpha characters (`\W`) from a string

**Parameters**

**str**:  *sting*,  The input string to strip

### capitalize(str)

Capitalizes the first letter of the given string

**Parameters**

**str**:  *string*,  String to capitalize


### capitalizeWords(str)

Capitalizes the first letter of each word in the given string

**Parameters**

**str**:  *string*,  String to capitalize


### getProperty(obj, pathname)

Provides the member of an object using dot separated path

It's best to use this only when the sub elements might not be defined,
to avoid complex and awkward expressions.

Note: Arrays can use the index number since we access object
properties and array indices in the same way

Example:

`obj = { a: { b: { c: 'test', d: [1,2,3] }}}`

- `getProperty(obj, 'a.b.c')`     -> `'test'`
- `getProperty(obj, 'a.b')`       -> `{ c:'test' }`
- `getProperty(obj, 'a.b.d.0')`   -> `1`

**Parameters**

**obj**:  *object*,  the object to look through

**pathname**:  *string*,  the dot separated path of object properties and/or array indices

------

## Spice Namespace


### add(ops)

Add a Spice instant answer to the AnswerBar and display it

Note: A detailed explanation of `Spice.add()` can be found in [Displaying your Spice](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md)

**Parameters**

**ops**:  *object*,  The object containing all necessary information for creating a Spice instant answer


### getDOM(id)

Provides a scoped DOM for a given Spice id

Note: Seeing as we maintain a cache, this is more efficient than using jQuery, i.e. `$('spice_name')`

Example:

`var $my_spice = Spice.getDOM('my_spice')`

**Parameters**

**id**:  *string*,  The id of the Spice Instant Answer, should match the `id` property of the object given to `Spice.add()`

**Returns**

*object*, A jQuery object, matching the selector that targets the given Spice id


### registerHelper(id, fn)

Provides access to `Handlebars.registerHelper()` so you can register helpers for your Spice

**Parameters**

**id**:  *string*,  The name of the helper to register

**fn**:  *function*,  The function we are registering


### failed(id)

Alerts the frontend that a Spice has stopped executing, preventing it from being displayed.

Note: This is generally used when a Spice API returns no useful results.

Example:

```javascript
if (/* check for no results */) {
    
```

**Parameters**

**id**:  *string*,  The id of the Spice Instant Answer, should match the `id` property of the object given to `Spice.add()`