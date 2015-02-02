## Language API

The [core DDG library](https://github.com/duckduckgo/duckduckgo) exposes a Language API which Goodie and Spice Instant Answers can access in their `handle` functions. The location data is contained in the `$lang` variable.

<!-- /summary -->

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

**Note**: The user's locale does not imply their preferred language. It simply provides the locale based on the user's IP. Thus, the locale should not be used to determine the display language for an Instant Answer.

When testing interactively with `duckpan`, the locale will always be set to `en_US`.

It is possible to set different locales when running automated tests. Please refer to the [Language API testing guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/testing_language_api.md) for more information.
