# DDG Methods (JavaScript)

### `DDG.get_query()`

#### Return:
  
- `String`
  
Provides the original query as it appears in the search box (ie, leading, trailing and extra spaces removed)


### `DDG.get_query_encoded()`

#### Return:
  
- `String`

Provides the return of `DDG.get_query` as a URIEncoded string, i.e. (`encodeURIComponent(DDG.get_query())`).


### `DDG.isRelevant()`

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)


### `DDG.getRelevants()`

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

- Comparator function is required to assign a property of the candidate called comparable which is the string undergoing relevancy check in isRelevant)


### `DDG.getDateFromString(date_as_string)`

#### Input:

- `date_as_string` : string formatted as yyyy-mm-dd

#### Return:

- `Date`

Creates a [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) instance from the input string.


### `DDG.getOrdinal(n)`

#### Input:

- `n` : number

#### Return:

-`String`

Provides the ordinal suffix for a number `n` appended to the number 

E.g. `DDG.getOrdinal(1)` evaluates to `"1st"`


### `DDG.get_asset_path( spice_name, asset_name  )`

#### Input:
  
- `spice_name` : string
- `asset_name` : string
  
Provides a path to the named asset (image) in the share directory for the specified spice instant answer

E.g.

`/share/spice/<spice_name>/<spice_version/<asset_name>`


### `DDG.get_is_safe_search()`

#### Return:

- `Boolean`

Provides a boolean value indicating whether the current result has prevented an unsafe (adult) Spice instant answer from showing
