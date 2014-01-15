# DDG Methods (JavaScript)

### `DDG.get_query()`

#### Return:
  
- `String`
  
Provides the original query as it appears in the search box (ie, leading, trailing and extra spaces removed)


### `DDG.get_query_encoded()`

#### Return:
  
- `String`

Provides the return of `DDG.get_query` as a URIEncoded string, i.e. (`encodeURIComponent(DDG.get_query())`).


### `DDG.isRelevant(candidate, skipArray, minWordLength, strict)`

#### Input:

- `candidate` &mdash; string

- `skipArray` (optional) &mdash; array of strings 

-  `minWordLength` (optional) &mdash; number
       -   default value: `4`

- `strict` (optional) &mdash; boolean

#### Return:

- `Boolean`

Determines if `candidate` is relevant to the search query. 

`skipArray` is an array of words (usually the trigger words) that should not be considered in determining the candidate string's relevancy.


### `DDG.getRelevants()`

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

- Comparator function is required to assign a property of the candidate called comparable which is the string undergoing relevancy check in isRelevant)


### `DDG.getDateFromString(date_as_string)`

#### Input:

- `date_as_string` &mdash; string in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format
  - valid formats: `yyyy-mm-dd` or `yyyy-mm-ddThh:mm:ss`

#### Return:

- `Date`

Creates a [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) instance from the input string. 


### `DDG.getOrdinal(n)`

#### Input:

- `n` &mdash; number

#### Return:

- `String`

Provides the ordinal suffix for a number `n` appended to the number 

E.g. `DDG.getOrdinal(1)` evaluates to `"1st"`


### `DDG.get_asset_path( spice_name, asset_name  )`

#### Input:
  
- `spice_name` &mdash; string
- `asset_name` &mdash; string
  
Provides a path to the named asset (image) in the share directory for the specified spice instant answer

E.g.

`/share/spice/<spice_name>/<spice_version>/<asset_name>`


### `DDG.get_is_safe_search()`

#### Return:

- `Boolean`

Provides a boolean value indicating whether the current result has prevented an unsafe (adult) Spice instant answer from showing
