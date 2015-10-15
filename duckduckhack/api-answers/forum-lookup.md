# How to Make a Forum Lookup

Some of our most popular Instant Answers have been direct access to forums, such as [Stack Overflow](#) or [Reddit](#). We'd love to see more community wisdom made part of search results, and this tutorial is one example of how to do that.

Together we'll build an Instant Answer that directly displays Hacker News posts alongside DuckDuckGo.com search results:

![Hacker News Spice](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fia-screenshots.s3.amazonaws.com%2Fhacker_news_index.png%3Fnocache%3D4600&f=1)

It uses an external API (the Hacker News search API), which makes it a "Spice" type of Instant Answer. You can see it in action by searching for ["hn dropbox"](#) for example.

## How It Works

When a user searches anything containing words such as "hn", "hn search", or "hacker news", DuckDuckGo will trigger this Instant Answer. That means its front-end code will run on the search results page.

When the search results page loads, the Instant Answer will make an AJAX call to the Hacker News API. If any articles come back, the Instant Answer will parse, sort, and display each item to the user.

Simple enough. So how do we make that work in code?

## Anatomy of an Instant Answer

The Hacker News Instant Answer is a combination of several backend and fronted code files, each covering a specific function. Because it calls an external API, it is a "Spice" Instant Answer, and all files will be located in the [Spice repository](#).

Backend files:

File | Purpose | Location
-----|---------|---------
[`HackerNews.pm`](#) | Specifies the query triggers, Hacker News API endpoint, and the metadata (such as attribution, name, and so on). | Perl files are placed in the [`zeroclickinfo-spice/lib/DDG/Spice`](#) directory.
[`HackerNews.t`](#) | A test file; it asserts that specific search queries will trigger (or not trigger) this Instant Answer. | Test files are placed in the [`zeroclickinfo-spice/t`](#) directory.

Frontend files:                                                                

File | Purpose | Location
-----|---------|---------
[`hacker_news.js`](#) | When the IA is triggered, this file runs on the search results page. It processes the response from the Hacker News API and specifies how to display it. | Frontend files are placed in the [`zeroclickinfo-spice/share/spice/hacker_news/`](#) directory.
[`hacker_news.css`](#) | A minor, optional, custom css file | [`zeroclickinfo-spice/share/spice/hacker_news/`](#)
[`footer.handlebars`](#) | A minor, optional [sub-template](#), a custom handlebars HTML template used as part of the main template. Its use is specified in `hacker_new.js`. | [`zeroclickinfo-spice/share/spice/hacker_news/`](#)

That's it - these are all the files and functionality necessary to create this Instant Answer. Next, we'll go line by line and build it together from scratch.

## Set Up Your Development Environment

Before we begin coding, we'll need to set up our development environment. There are three main steps:

1. Fork the [Spice Repository](#) on Github.com. ([Find out how](#))
2. Fork the [DuckDuckGo environment](#) on Codio.com (our tools). ([Find out how](#))
3. Clone your Github fork onto the Codio environment. ([Find out how](#))

If this is your first time setting up, fear not! Check out our [detailed, step-by-step guide](#) to setting up.

## Create a New Instant Answer

In Codio, load the terminal, and change into your repository home directory:

(Screenshot of clicking terminal)

```
[08:17 PM codio@border-carlo workspace ]$ cd zeroclickinfo-spice
```

The `duckpan` tool helps make and test Instant Answers. To create a new Instant Answer template, run **`duckpan new`**:

```
[08:18 PM codio@border-carlo zeroclickinfo-spice {master}]$ duckpan new                                                                                    
Please enter a name for your Instant Answer :
```

Type `Hacker Newz` (since *Hacker News* already exists in the repository, we'll change one letter for this tutorial). The tool will do the rest:

```
Created file: lib/DDG/Spice/HackerNewz.pm                                                                                                                  
Created file: share/spice/hacker_newz/hacker_newz.handlebars                                                                                               
Created file: share/spice/hacker_newz/hacker_newz.js                                                                                                       
Created file: t/HackerNewz.t                                                                                                                               
Successfully created Spice: HackerNewz
```

That's convenient: The files have each been named - and located - according to the project's conventions. Internally, each file contains correct boilerplate to save us time.

## `HackerNewz.pm`

Let's open up `HackerNewz.pm`. 

Navigate using the Codio file tree on the left, and double click on the file, in the `lib/DDG/Spice/` directory. It'll be full of comments and sample code we can change as we please.

### Settings and Metadata

Each Instant Answer is a Perl package, so we start by declaring the package namespace in CamelCase format. This has already been done for us:

```perl
package DDG::Spice::HackerNewz;
```

Next, change the comments to contain a short abstract. Easy enough:

```perl
# ABSTRACT: Search for Hacker News
```

Now we'll import the Spice class (as well as tell the Perl compiler to be strict) - also already done for us:

```perl
use strict;
use DDG::Spice;
```

On the next line, we'll leave caching on. By default, caching saves the results to individual API calls for an hour. Of course, this may not be right for some Instant Answers - so you can just replace `1` with `0`. Caching can get interesting - [learn more here](#). 

```perl
spice is_cached => 1;
```

Now for the Metadata. Because there's so many Instant Answers, metadata helps us organize, describe, and attribute your contribution. They are also used to automatically generate Instant Answer Pages - plus give you credit right on DuckDuckGo.com.

For example, these are the Metadata values used in the live HackerNews answer. You can learn more about each Metadata property [documented here](#).

```perl
primary_example_queries "hn postgresql";
description "Search the Hacker News database for related stories/comments";
name "HackerNews";
code_url "https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/HackerNews.pm";
icon_url "/i/www.hnsearch.com.ico";
topics "programming", "social";
category "forums";
attribution github => ['https://github.com/adman','Adman'],
            twitter => ['http://twitter.com/adman_X','Adman'];
```

### API Endpoint

With the formalities out of the way, let's define the most important element of our Instant Answer - the API call. This is a URL to which we'll make a GET request.

```perl
spice to => 'https://hn.algolia.com/api/v1/search?query=$1&tags=story';
```

Notice the `$1` - that's a placeholder for a dynamic value our Instant Answer will provide. Many Instant Answers take advantage of this for search endpoints, but others might not need it at all. Feel free to leave it out of your URL.

What fills the `$1`? Our *handle* function, which we'll talk about in a bit.

### Indicate our Callback Function

In most cases, APIs allow for a "callback" parameter, which we'd usually include in the URL like this:

```perl
http://www.api.awesome.com/?q=<search_term>&callback=<function_name>
```

This parameter is used to wrap the JSON object being returned in a JavaScript function call. This function is often named in the `callback` parameter - but that depends on the API. 

In this particular case, the API doesn't allow for this parameter to be specified, so we force this manually by using the **spice wrap\_jsonp\_callback** function. Enter this text on the next line to do this:

```perl
spice wrap_jsonp_callback => 1;
```

Now, when the JSON is returned by the API, it will be wrapped in a call to our Spice's JavaScript callback function, which lives in the frontend, and which we'll define in `hacker_newz.js`.

### Triggers

How will DuckDuckGo know to trigger our Instant Answer on a user's search? That's what triggers are for:

```perl
triggers startend => "hn", "hackernews", "hacker news", "news.yc", "news.ycombinator.com", "hn search", "hnsearch", "hacker news search", "hackernews search";
```

This tells DuckDuckGo that if any of these strings occurs at the *start* or *end* of any user's search query, it should activate our Instant Answer and give the API a shot. Of

Aside from `startend`, there are more types of triggers - and you can even define several together. You can [learn more about triggers here](#).

### Handle Function

Remember our `$1` placeholder before? It receives whatever is returned by the `handle` function. 

```perl
handle remainder => sub {
    return unless $_;
    return;
};
```

This function is a simple case: it returns the *remainder* of the query, unless it's blank. The *remainder* is just the query minus the trigger. If a user searches 'hacker news meteor', the remainder would be 'meteor'.

There's fancier things that can be done with this function, including regular expressions - you can [read more about handle functions here](#).

Oh - one more thing. Because this is a Perl package, it must return `1` at the end to indicate successful loading:

```perl
1;
```

Our backend is complete. Now DuckDuckGo knows *when* to call the API, *where* to call the API, and *what* query to send it. Next, we'll tell DuckDuckGo how to display the results.

## `hacker_newz.js`

Let's open up `hacker_newz.js`. Navigate using the Codio file tree on the left, and double click on the file, in the `zeroclickinfo-spice/share/spice/hacker_news/` directory. It, too, will be full of comments and sample code we can change as we please.

### JavaScript Formalities

Our JavaScript file is wrapped inside the "[module pattern](http://www.addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript)" that makes sure we can access the global scope, but that no variables inside this pattern will leak into the global scope. We also take advantage of JavaScript's [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode?redirectlocale=en-US&redirectslug=JavaScript%2FReference%2FFunctions_and_function_scope%2FStrict_mode).

```javascript
(function(env) {
    "use strict";

    // Everything else...

})(this);
```

It's not at all critical to understand this - simply that it is required for any Instant Answer frontend.

### Define the Callback

Our frontend callback is what handles any data from our API call. When our API call returns, its response is passed to this callback as `api_result`. It should already be included in the file:

```javascript
env.ddg_spice_hacker_newz = function(api_result) { 
    // Everything else...
}
```

### Call Spice.Failed() If Nothing Returned

Just because our Instant Answer triggered doesn't mean the API will necessarily return anything. Here, we check for the case of no response, error response, or empty response. 

The default code is a good start. **However, this code should be customized to fit the response of your particular API.**

```javascript
if (!api_result || api_result.error) {
    return Spice.failed('hacker_newz');
}
```

The Hacker News API, in particular, returns its data inside a `hits` property - so we check for its existence. 

Like many APIs, the results come as an *array*. That means we'll also check if `hits` has a `length`. That way, if no results were returned from the API, we can stop that as well.

```javascript
if(!api_result || !api_result.hits || api_result.hits.length === 0) {
    return Spice.failed('hacker_newz');
}
```

It's important to use `Spice.failed()` because this lets the rest of the Spice system know our Spice isn't going to display so that other relevant answers can be given an opportunity to display.

### Display the Data

With results in hand, we call `Spice.add()` to display our Spice to the user. 

While our `hacker_newz.js` boilerplate doesn't contain this, you might have noticed that our final [`hacker_news.js`](#) uses `DDG.require()`. This is not necessary for all Instant Answers, but is used to include external libraries, like [MomentJS](http://momentjs.com/) in this case. You can [learn more about `DDG.require()` here](#).

```javascript
DDG.require('moment.js', function(){ // Not required for most Instant Answers
    Spice.add({
        // Display properties go here
    });
});
```

### Set Our Display Properties

Let's look inside the `Spice.add()` call. It's passed an object with display properties - let's go through each. A full explanation of each display property can be found in the [Display Reference](#).

The `id` is automatically inserted for us:

```javascript
id: 'hacker_newz',
```

The `name` is the name of the clickable tab in the AnswerBar containing our Instant Answer.

```javascript
name: 'Social',
```

We specify the `data` returned by the API. This is usually `api_result` or the sub-property containing the actual content - in this case, `hits`.

```javascript
data: api_result.hits,
```

The `meta` property defines all the surrounding details of the Instant Answer, such as the phrase "Showing 20 Hacker News Submissions", or the link to the information source. You can learn about each meta property available to you in the [Display Reference](#).

In this example, `sourceUrl` is calculated at the top of the callback in [`hacker_news.js`](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/hacker_news/hacker_news.js#L8)

```javascript
meta: {
    sourceName: 'HN Search',
    sourceUrl: sourceUrl,
    total: api_result.hits,
    itemType: (api_result.hits.length === 1) ? 'Hacker News submission' : 'Hacker News submissions',
    searchTerm: decodeURIComponent(query)
},
```

To prepare our data for displaying as HTML, we define a `normalize` function. This optional function takes each raw API item, and returns an item ready for displaying in the HTML template. 

The `normalize` function is run on each item in the API result. For convenience, the original properties of each API result (which are not overwritten) are also included. Learn more about the [`normalize` function here](#).

```javascript
normalize: function(item) {
    return {
        title: item.title,
        url: (item.url) ? item.url : 'https://news.ycombinator.com/item?id=' + item.objectID,
        points: item.points || 0,
        num_comments: item.num_comments || 0,
        post_domain: extractDomain(item.url),
        date_from: moment(item.created_at_i * 1000).fromNow(),
        arrowUrl: DDG.get_asset_path('hacker_news','arrow_up.png')
    };
},
```

Let's specify what HTML templates we'll use to display each item. The vast majority of Instant Answers use the DuckDuckHack [built-in templates system](#). There are all sorts of specialized templates, from displaying places on a map, to displaying movie titles, to products, and lookup information. Each of these can be customized using [options and variants](#). 

[Template groups](#) are convenient presets. They're specified in the `group` property. The other properties you see under templates customize the behavior of the group. For example, `detail: false` makes sure items will always be displayed as tiles. Learn more about these options [here](#).

```javascript
templates: {
    group: 'text',
    options: {
        footer: Spice.hacker_news.footer
    },
    detail: false,
    item_detail: false,
    variants: {
        tileTitle: "3line-small",
        tileFooter: "3line"
    }
},
```

You'll notice the inclusion of the `Spice.hacker_news.footer` sub-template. This refers to the [footer.handlebars](#) file also in the `share/spice/hacker_news/` directory. You can learn more about the [inclusion of sub-templates here](#).

Finally, we'll give instructions on how to sort our results - by what properties. [Learn more about sorting here](#).

```javascript
sort_fields: {
    score: function(a, b){
        return (a.points > b.points) ? -1 : 1;
    },
    date: function(a, b){
        return (a.created_at_i > b.created_at_i) ? -1 : 1;
    }
},
sort_default: 'score'
```

That's it! We've told the DuckDuckGo search results page how to display our data.

## Handlebars Templates

Many [built-in templates](#) allow for inserting sub-templates to fill out particular features. For example, sub-templates can be used to create custom footers, calls-to-action, or decide how to display lists of values.

In this case, you'll notice that there is a `footer.handlebars` function found in [`share/spice/hacker_news`](#). You'll also notice that above in the `templates` property, it's specified to be used as the template footer:

```javascript
templates: {
    ...
    options: {
        footer: Spice.hacker_news.footer
    },
    ...
}
```

Sub-templates can either be built-in or created custom for your Instant Answer. You can learn more about how they work in the [sub-templates reference](#).

## CSS Files

You'll notice there's a [css file](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/hacker_news/hacker_news.css) in the `share/spice/hacker_news/` directory.

While any CSS files in the directory will be included automatically, **this is no longer necessary or encouraged**. Instead, the more stable and maintainable option is to use [variants](#).

## Test File

Creating a test file for your Instant Answer is a critical requirement for [submitting](#) your Instant Answer. You can learn more in the [Test File Reference](#).

In this case, `duckpan new` created a test file for us, under [`t/HackerNews.t`](#). We'll test two queries to make sure they trigger our Instant Answer:

```perl
#!/usr/bin/env perl

use strict;
use warnings;
use Test::More;
use DDG::Test::Spice;

ddg_spice_test(
    [qw( DDG::Spice::HackerNews )],
    'hn duckduckgo' => test_spice(
        '/js/spice/hacker_news/duckduckgo',
        call_type => 'include',
        caller => 'DDG::Spice::HackerNews'
    ),
    'hn postgresql' => test_spice(
        '/js/spice/hacker_news/postgresql',
        caller    => 'DDG::Spice::HackerNews',
    ),
);

done_testing;
```

A test file is required for submitting your Instant Answer. However, we don't need to it proceed with interactively testing our code, which we'll do next.

### Interactively Test Our Instant Answer

Inside Codio, we can preview the behavior of all Instant Answers on a local test server. 

In Codio, load the terminal, and make sure you're in your repository's home directory. If not, change into it.

Enter the **`duckpan server`** command and press Enter.

```
[08:18 PM codio@border-carlo zeroclickinfo-spice {master}]$ duckpan server

```

The terminal should print some text and let you know that the server is listening on port 5000.

```
Starting up webserver...

You can stop the webserver with Ctrl-C

HTTP::Server::PSGI: Accepting connections at http://0:5000/
```

Click the "**DuckPAN Server**" button at the top of the screen. A new browser tab should open and you should see the DuckDuckGo Homepage. Type your query to see the results (actual search results will be placeholders.)

(Screenshot)

Need help? [Join us over on Slack!](mailto:QuackSlack@duckduckgo.com?subject=AddMe)