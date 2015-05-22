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

Specifying options in Perl is the most straightforward method, but there are several optional properties that cannot be specified on the server-side. These must be [specified in the Goodie's frontend](#setting-goodie-display-properties-in-the-frontend), in a JavaScript file.

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
        data => Array or Hash (in the case of a single item),
        meta => {
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

            # Note that while the following may reference JavaScript variables, 
            # they are still specified as strings in Perl

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

While most display properties can be set in a Goodie's Perl file, others by their nature must be specified in the frontend part of the code. These are:

- [Normalize function](https://duck.co/duckduckhack/display_reference#codenormalizecode-emfunctionem-optional)
- [Events](https://duck.co/duckduckhack/display_reference#events)
- [Relevancy](https://duck.co/duckduckhack/display_reference#coderelevancycode-emobjectem-optional)
- [Sort fields](https://duck.co/duckduckhack/display_reference#codesortfieldscode-emobjectem-optional)

To specify any of these, simply create a javascript file in `share/goodie/INSTANT_ANSWER_ID/INSTANT_ANSWER_ID.js`. For example, using the ["BP to ms" Instant Answer](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/BPMToMs.pm) as an example (where the `id` is set to `'bpmto_ms'`):

Create a file at `share/goodie/bpmto_ms/bpmto_ms.js`, which creates a namespace and a build function. 



```javascript
DDH.bpmto_ms = DDH.bpmto_ms || {}; // create the namespace in case it doesn't exist

DDH.bpmto_ms.build = function(ops) {
    
    return {
        // Specify any frontend display properties here
    };
    
};
```

The build function takes `ops` as an argument; this represents the `structured_answer` hash from the Perl as a JavaScript object.

Your build function returns an object with any frontend display properties you want to set. For example, you could set an [event](https://duck.co/duckduckhack/display_reference#events):

```javascript
return {
    onShow: function() {
        console.log("onShow for bpmto_ms");
    },
}
```

Or you could set a [`normalize` function](https://duck.co/duckduckhack/display_reference#codenormalizecode-emfunctionem-optional) - and so on:

```javascript
return {
	...
    normalize: function(item){
        return {
            title: item.heading
        };
    }
}
```

Additionally, it is worth noting that all of the display options specified in Perl could instead be specified in your JavaScript - if you so desired. 

For example:

```javascript
return {
    ...
    templates: {
        group: 'base',
        detail: false,
        options: {
            // Note that because this is JavaScript, sub-templates are specified
            // as function references rather than strings. 
            content: DDH.bpmto_ms.content
        }
    }
}
```