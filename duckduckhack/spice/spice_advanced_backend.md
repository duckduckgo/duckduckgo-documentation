# Advanced Spice Handlers
<!--
<h2 class="summary" moreat="spice-advanced-backend">Spice: advanced backend</h2>
-->
<div class="summary-text" markdown="1">

- [Multiple Placeholders in Spice To URL](http://duck.co/duckduckhack/spice_advanced_backend#Multiple-Placeholders-in-Spice-To-URL)

- [Returning Multiple Values (to Spice From)](http://duck.co/duckduckhack/spice_advanced_backend#Returning-Multiple-Values-to-Spice-From)

- [API Keys](http://duck.co/duckduckhack/spice_advanced_backend#api-keys)

- [JSON -> JSONP](http://duck.co/duckduckhack/spice_advanced_backend#json-gt-jsonp)

- [Pure JS functions](http://duck.co/duckduckhack/spice_advanced_backend#pure-js-functions)

- [Caching API Responses](http://duck.co/duckduckhack/spice_advanced_backend#caching-api-responses)

- [Caching API Calls](http://duck.co/duckduckhack/spice_advanced_backend#caching-api-calls)

</div>
## Multiple Placeholders in Spice To URL
<!--
<h2 class="summary" moreat="spice_advanced_backend#multiple-placeholders-in-spice-to-url">Spice: URL placeholders</h2>
<span class="summary-text" markdown="1">
If you need to substitute multiple parameters into the API call like how the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm) uses two numbers to specify the min and max length of the random word, you can use the **Spice from** keyword:

```perl
spice from =\> '(?:([0-9]+)\-([0-9]+)|)';
```
</span>

-->
If you need to substitute multiple parameters into the API call like how the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm) uses two numbers to specify the min and max length of the random word, you can use the **Spice from** keyword:

```perl
spice from => '(?:([0-9]+)\-([0-9]+)|)';
```

Whatever you return from the handle function gets sent to this **spice from** regexp, which then gets fed into the **spice to** API:

For example, if your `handle` function looked like this:

```perl
handle remainder => sub {
  ...
  if ( $foo ){
    my $minMax = "10-100"
    return $minMax;
  }
  return;
}
```

Then the the string `10-100` would be sent to the `spice from` regexp, which would capture the two numbers into `$1` and `$2`. These two placeholders are then used to replace `$1` and `$2` in the `spice to` URL:

```perl
spice to => 'http://api.wordnik.com/v4/words.json/randomWord?minLength=$1&maxLength=$2&api_key={{ENV{DDG_SPICE_RANDWORD_APIKEY}}}&callback={{callback}}';
```

**\*\*Note:** The reason why you do not need to specify a **from** keyword by default, is that the default value of `spice from` is **(.*)**, which means whatever you return gets gets captured into `$1`.

## Returning Multiple Values (to Spice From)
<!--
<h2 class="summary" moreat="spice_advanced_backend#returning-multiple-values-to-spice-from">Spice: returning multiple values</h2>
<div class="summary-text" markdown="1">
You can have multiple return values in your handle function like the [AlternativeTo Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/AlternativeTo.pm).

```perl
return $prog, $platform, $license;
```
</div>
-->
You can have multiple return values in your handle function like the [AlternativeTo Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/AlternativeTo.pm).

```perl
return $prog, $platform, $license;
```

In this case they are URL encoded and joined together with '/' chars, e.g., in this case **$prog/$platform/$license**. Then that full string is fed into the **spice from** regexp.

```perl
spice from => '([^/]+)/?(?:([^/]+)/?(?:([^/]+)|)|)';
```

## API Keys
<!--
<h2 class="summary" moreat="spice_advanced_backend#api-keys">Spice: API keys</h2>
<div class="summary-text" markdown="1">
Some APIs require API keys to function properly like in the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm). You can insert an API key for testing in the callback function and replace it with a variable reference when submitting.

```perl
spice to => 'http://api.wordnik.com/v4/words.json/randomWord?minLength=$1&maxLength=$2&api_key={{ENV{DDG_SPICE_RANDWORD_APIKEY}}}&callback={{callback}}';
```
</div>
-->
Some APIs require API keys to function properly like in the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm). You can insert an API key for testing in the callback function and replace it with a variable reference when submitting.

```perl
spice to => 'http://api.wordnik.com/v4/words.json/randomWord?minLength=$1&maxLength=$2&api_key={{ENV{DDG_SPICE_RANDWORD_APIKEY}}}&callback={{callback}}';
```

You can set the variable when you start DuckPAN server like this:

```bash
DDG_SPICE_RANDWORD_APIKEY=xyz duckpan server
```

## JSON -> JSONP
<!--
<h2 class="summary" moreat="spice_advanced_backend#json-gt-jsonp">Spice: JSONP</h2>
<div class="summary-text" markdown="1">
Some APIs don't do JSONP by default, i.e. don't have the ability to return the JSON object to a callback function. In this case, first you should try to contact the API provider and see if it can be added. Where it cannot, you can tell us to wrap the JSON object return in a callback function like in the [XKCD Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Xkcd.pm).

```perl
spice wrap_jsonp_callback => 1;
```
</div>
-->
Some APIs don't do JSONP by default, i.e. don't have the ability to return the JSON object to a callback function. In this case, first you should try to contact the API provider and see if it can be added. Where it cannot, you can tell us to wrap the JSON object return in a callback function like in the [XKCD Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Xkcd.pm).

```perl
spice wrap_jsonp_callback => 1;
```

## Pure JS functions
<!--
<h2 class="summary" moreat="spice_advanced_backend#json-gt-jsonp">Spice: pure JS functions</h2>
<div class="summary-text" markdown="1">
Sometimes no external API is necessary to deliver the instant answer like how the [Flash Version Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/FlashVersion.pm) just prints out your [Flash Player version](https://duckduckgo.com/?q=flash+version) using an [internal call](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/flash_version/spice.js).
</div>
-->
Sometimes no external API is necessary to deliver the instant answer like how the [Flash Version Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/FlashVersion.pm) just prints out your [Flash Player version](https://duckduckgo.com/?q=flash+version) using an [internal call](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/flash_version/spice.js).

In cases like these you can define a **spice\_call\_type** as 'self' like this:

```perl
spice call_type => 'self';
```

Then in the handle function you can return call, e.g.:

```perl
return $_ eq 'flash version' ? call : ();
```

The return of **call** will run whatever is in the **call\_type** setting. **self** is a special keyword to just run the callback function directly, in this case **ddg\_spice\_flash_version()**.

## Caching
<!--
<h2 class="summary" moreat="spice_advanced_backend#caching">Spice: caching</h2>
<div class="summary-text" markdown="1">
Spice instant answers have two forms of caching: API Response caching (remembers the JSON returned from the API) and API Call caching (remembers the API call URL created for a given query).

- [Caching API Responses](http://duck.co/duckduckhack/spice_advanced_backend#caching-api-responses)

- [Caching API Calls](http://duck.co/duckduckhack/spice_advanced_backend#caching-api-calls)

</div>
-->

Spice instant answers have two forms of caching: API Response caching (remembers the JSON returned from the API) and API Call caching (remembers the API call URL created for a given query). Both of these will be explained with examples.

### Caching API Responses

By default, we cache API responses for for **24 hours**. We use [nginx](https://duckduckgo.com/?q=nginx) and get this functionality by using the [proxy_cache_valid](http://wiki.nginx.org/HttpProxyModule#proxy_cache_valid) directive. You can override our default behavior by setting your own `spice proxy_cache_valid` directive like in the [RandWord Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RandWord.pm):

```perl
spice proxy_cache_valid => "200 304 1d";
```

This will cache any HTTP 200 and 304 responses for 1 day. You can also force API responses to **not** be cached like so:

```perl
spice proxy_cache_valid => "418 1d";
```

This is a special declaration that will only cache [418 HTTP](https://duckduckgo.com/?q=HTTP+418) return values for 1 day. Since regular return codes are [200](https://duckduckgo.com/?q=HTTP+200) and [304](https://duckduckgo.com/?q=HTTP+304), nothing will get cached.

If you expect API response to change very frequently you should lower the caching time. As well, if your API is supposed to return random results (such as the RandWord spice) it makes sense to prevent all caching so every time the spice is trigger a new result will be returned.

### Caching API Calls

When a Spice triggers, its Perl code is used to construct the URL for the API call. It's likely that a given query will always map to the same API call so by default we cache the API calls for a given query for **1 hour**:

```
# This query will always make the same API call
"random word" => http://api.wordnik.com/v4/words.json/randomWord
```

Sometimes, a given query won't always require the same API call. This scenario generally arises when a Spice instant answer uses the Location API and uses it to append the user's location to the API call:

```
# This query will NEVER make the same API call, because the location is dynamic
"weather" => http://forecast.io/ddg?q=<user_location>
```

To **turn off** API Call caching, you must set `spice is_cached` to `0` as we do in the [Forecast](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Forecast.pm) instant answer:

```perl
spice is_cached => 0;
```

This way, every time the Forecast instant answer is triggered, **Forecast.pm** will be run, so the correct URL will be built and  the current user's location will be used for the API call.
