# Spice Attributes (Perl)

### Spice `to`
(tbd)

### Spice `from`
(tbd)

### Spice `wrap_jsonp_callback`
If the API used for your plugin does not support JSONP (ie. it doesn't provide a URI parameter to indicate the callback function to be used on the API response), set `wrap_jsonp_callback` to true and the API response will automatically be wrapped in the appropriate function call for your plugin.

### Spice `proxy_cache_valid `
(tbd)

### Spice `is_unsafe`
If your plugin has the potential to return unsafe results (eg. contains vulgar words, crude humour) the `is_unsafe` flag must be set to true. Any plugins that have `is_unsafe` set to true can only be seen when a user has safe-search turned off, or when they add the phrase `!safeoff` to their query (eg. "automeme !safeoff").
