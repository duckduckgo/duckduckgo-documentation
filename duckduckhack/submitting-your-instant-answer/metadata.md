# Instant Answer Metadata

Including metadata allows us to categorize and describe your instant answer on the [Goodies page](http://duckduckgo.com/goodies). This document explains the different types of metadata that you may add to the source code of your instant answer.

------

## name

A unique name for this instant answer.

While this can be arbitrary, it is considered good practice to have the chosen name be similar to the Perl package in which it is contained, e.g., DDG::Spice::RedditSubSearch.

```perl
name "Subreddit Search";
```

## source

The name of the data source used for your instant answer.

```perl
source "Reddit";
```

## icon_url (optional)

The favicon URL for the data source used.

**Note:** The favicon is not always located at `http://domain/favicon.ico`. It is often given as an explicit URL in the HTML header as `x-icon`, `apple-touch-icon` or similar.

Favicons can sometimes be found by searching for the data source on DuckDuckGo. If a favicon exists, we will display it beside any results from that domain. Feel free to use our link from there :)

```perl
icon_url "http://www.reddit.com/favicon.ico";
```

or, for DuckDuckGo-sourced favicons,

```perl
icon_url "/i/reddit.com.ico";
```

## description

A succinct explanation of what the instant answer does. Please **exclude** the source name if possible.

```perl
description "Search for Subreddits";
```

## primary_example_queries

Examples of the most common types of queries which will trigger the instant answer.

```perl
primary_example_queries "/r/pizza", "subreddit nature";
```

## secondary_example_queries (optional)

Examples of other, less common, trigger words or phrases for the instant answer, if applicable.

```perl
secondary_example_queries "r/accounting";
```

## category

The category into which your instant answer best fits.

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

**Note:** Instant answers may specify ***exactly one*** category.

```perl
category "forums";
```

## topics

A list of the topics to which your instant answer applies.

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

**Note:** Instant answers may specify ***multiple*** topics.

```perl
topics "social", "entertainment", "special_interest";
```

## code_url

URL for the instant answer code on github.

```perl
code_url "https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/RedditSubSearch.pm";
```

## attribution

Information about you, the author.

Supported attribution sources include:

- email
- twitter
- web
- github
- facebook
- cpan

**Note:** For each attribution type, you may provide either a single string or an array reference with two values.

If a single string is given, it will be used to create a link to the defined profile and **also** serve as the **text** for the link.

When an array reference is provided, the first element will be used to create the link while the second will be used as the text for the link.

```perl
attribution twitter => "mithrandiragain",
            github  => ["MithrandirAgain", "Gary Herreman"],
            web     => ['http://atomitware.tk/mith', 'MithrandirAgain'];
```
