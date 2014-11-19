# Spice Attributes (Perl)

## Spice `to`

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

## Spice `from`

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

## Spice `wrap_jsonp_callback`

If the API used for your Instant Answer does not support JSONP (ie. it doesn't provide a URI parameter to indicate the callback function to be used on the API response), set `wrap_jsonp_callback` to true and the API response will automatically be wrapped in the appropriate function call for your Instant Answer.

## Spice `proxy_cache_valid `

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

## Spice `is_unsafe`

If your Instant Answer has the potential to return unsafe results (eg. contains vulgar words, crude humour) the `is_unsafe` flag must be set to true. Any Instant Answers that have `is_unsafe` set to true can only be seen when a user has safe-search turned off, or when they add the phrase `!safeoff` to their query (eg. "automeme !safeoff").
