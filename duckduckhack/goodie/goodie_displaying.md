# Displaying Your Goodie in the DuckDuckGo AnswerBar

The final step of providing your Goodie results is displaying them in the DuckDuckGo AnswerBar.

## Setting Display Properties in a Goodie

Goodies are displayed according to a set of properties which can (mostly) be defined in each Goodie's Perl file. These options are returned as a hash called `structured_answer` when the Perl file finishes running. This hash is returned alongside the `$plaintext` string version of your Goodie result, used for the API):

```perl
return $plaintext,
    structured_answer => {
        ...
    };
```

For an example of how this works, take a look at the final return statement of the [BPM to ms](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/BPMToMs.pm) Goodie Perl file.

Specifying options in Perl is the most straightforward method, but there are several optional properties that cannot be specified on the server-side. These must be [specified in the Goodie's frontend](#setting-goodie-display-properties-in-the-frontend), in a Javascript file.

## Available Options

The properties you can return in your `structured_answer` hash are documented in the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference). This document provides an in-depth overview of all that the Instant Answer framework allows you to set.

In some scenarios, you may also want to handle the AnswerBar's events (for example, to stop media playing when the user hides your Instant Answer). These [events](https://duck.co/duckduckhack/display_reference#events) are covered at the end of the reference.

## Returning Display Properties in a Goodie's Perl

The following is a code summary of how the options covered in the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference) are returned in your Goodie Perl file.

```perl
return $plaintext,
    structured_answer => {
        id => String,
        name => String,
        data => Array,
        meta => {
            sourceUrl => String,
            sourceName => String
	        hidden => Boolean,
	        searchTerm => String,
	        itemType => String,

            primaryText => String,
            secondaryText => String,

            sourceName => String,
            sourceLogo => String,
            sourceUrl => String (url),
            sourceIcon => Boolean,
            sourceIconUrl => String (url),

            snippetChars => Integer
        },
        templates => {
            group => String,
            options => Hash

            item: String,
            item_custom: String,
            item_mobile: String,

            detail: String,
            detail_custom: String,
            detail_mobile: String,
            item_detail: String,

            variants: Hash

            elClass: Hash
        }

        view: String,
        model: String,
    };

```

For more information on each property and its usage, visit the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference).

## Setting Goodie Display Properties in the Frontend

