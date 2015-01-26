## Language API

While at the moment DuckDuckGo only accepts Instant Answers in English, it sometimes might be useful to know a user's locale. For instance, it is currently used by the [Translation](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Translate/FromTo.pm) Instant Answer.

Keep in mind the locale's language might not necessarily be the user's preferred language.

<!-- /summary -->

The [core DDG library](https://github.com/duckduckgo/duckduckgo) exposes a Language API which Goodie and Spice Instant Answers can access in their `handle` functions. The location data is contained in the `$lang` variable.

`$lang` refers to a [Language object](https://github.com/duckduckgo/duckduckgo/blob/master/lib/DDG/Language.pm) with the following properties:

```perl
my @language_attributes = qw( flagicon flag_url name_in_local rtl locale nplurals name_in_english);
```

Example data from `$lang`:

```perl
'nplurals'        => 2,
'name_in_local'   => 'English of United States',
'rtl'             => 0,
'flag_url'        => 'https://duckduckgo.com/f2/us.png',
'name_in_english' => 'English of United States',
'locale'          => 'en_US',
'flagicon'        => 'us'
```

When testing interactively with `duckpan`, the locale will always be set to `en_US`.

It is possible to set different locales when running automated tests. Please refer to the [Language API testing guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/testing_language_api.md) for more information.

When your Instant Answer goes live, `$lang` will refer to the user's chosen locale.
