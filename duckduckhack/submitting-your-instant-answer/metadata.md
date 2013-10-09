# Instant Answer Metadata

Metadata allows us to categorize and describe instant answers on our [Goodies page](http://duckduckgo.com/goodies).

The different types of metadata that you can add to your instant answer are explained below. The metadata must be added to the appropriate `.pm` file(s) for your instant answer.

------

## Name

An arbitrary, unique name for the instant answer (generally this should match the name that you've given Perl module and the `.pm` file. E.g DDG::Spice::RedditSubSearch, RedditSubSearch.pm).

```perl
name "Subreddit Search";
```

## Description

A succinct explanation of what the instant answer does. Try to *exclude* the source name if possible.

```perl
description "Search for Subreddits";
```

## Primary Example Queries

Used to highlight the most common types of queries which will trigger your instant answer.

```perl
primary_example_queries "/r/pizza", "subreddit nature";
```

## Secondary Example Queries (optional)

Used to highlight any other, less common trigger words or phrases for your instant answer, should they exist.

```perl
secondary_example_queries "r/accounting";
```

## Source

Name of the data source used for your instant answer.

```perl
source "Reddit";
```

## Category

The category which best fits your instant answer.

**\*\*Note:** Only ***one*** category can be specified.

```perl
category "forums";
```

Supported categories include:

- bang
- calculations
- cheat_sheets
- computing_info
- computing_tools
- conversions
- dates
- entertainment
- facts
- finance
- food
- formulas
- forums
- geography
- ids
- language
- location_aware
- physical_properties
- programming
- q/a
- random
- reference
- special
- software
- time_sensitive
- transformations

## Topics

The topic(s) which best fit your instant answer.

**\*\*Note:** ***Multiple*** topics can be specified.

```perl
topics "social", "entertainment", "special_interest";
```

Supported topics include:

- everyday
- economy\_and\_finance
- computing
- cryptography
- entertainment
- food_and_drink
- gaming
- geek
- geography
- math
- music
- programming
- science
- social
- special_interest
- sysadmin
- travel
- trivia
- web_design
- words\_and\_games

## icon_url (optional)

If a favicon exists for the data source used, provide the URL. 

**\*\*Note:** The favicon is not always at `http://url/favicon.ico`, but is often given as an explicit URL in the HTML header as `x-icon` or `apple-touch-icon` or possibly, something similar.

```perl
icon_url "http://www.reddit.com/favicon.ico";
```

or

Favicons can sometyimes be found by searching for the data source on DuckDuckGo, if a favicon exists, we will display it beside any results from that domain. Feel free to use our link from there :)

```perl
icon_url "/i/reddit.com.ico";
```

## code_url

URL for the instant answer code on github.

```perl
code_url "https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RedditSubSearch.pm";
```

## Attribution

```perl
attribution twitter => ["mithrandiragain", "Mithrandir"],
            github => ["MithrandirAgain", "Gary Herreman"],
            web => ['http://atomitware.tk/mith','MithrandirAgain'];
```

Supported attribution sources include:

- Email
- Twitter
- Web (website)
- Github
- Facebook
- Cpan

**\*\*Note:** There is a specific syntax for giving attribution. For each attribution type you can provide a single string, or an array with two values.

If one value is given, it will be used to create a link to whichever profile you are defining and it will serve as the **text** for the link.

Likewise, if two values are given, the first will be used for the `href`, while the second will be used as the **text** for the link.

E.g.

```perl
github => ["duckduckgo", "DuckDuckGo"];
```

Will render `<a href=https://github.com/duckduckgo>DuckDuckGo</a>`

Similarly,

```perl
twitter => "duckduckgo";
```

Will render `<a href=https://twitter.com/duckduckgo>@duckduckgo</a>`