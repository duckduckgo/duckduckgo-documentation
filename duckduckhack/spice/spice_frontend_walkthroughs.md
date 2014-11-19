## Spice Frontend Walkthoughs

- [Walkthrough #1: Alternative.To (Simple)](#walkthrough-1-alternativeto-simple)
- [Walkthrough #2: Movies (Medium)](#walkthrough-2-movies-medium)
- [Walkthrough #3: Airlines (Medium)](#walkthrough-3-airlines-medium)
- [Walkthrough #4: Quixey (Advanced)](#walkthrough-4-quixey-advanced)

<!-- /summary -->

------

## Walkthrough #1 - Alternative.To (Simple)

The Alternative.To Instant Answer is very similar to NPM in that it's also relatively simple. However, it returns multiple items, and so it produces a tile view, where each tile represents a single result item. Let's take a look at the code and see how this is done:
<!-- /summary -->

###### alternative_to.js

```javascript
(function(env) {
    "use strict";

    env.ddg_spice_alternative_to = function(api_result) {

        if (!api_result || !api_result.Items) {
            return Spice.failed('alternative_to');
        }

        Spice.add({
            id: 'alternative_to',
            name: 'Software',
            data: api_result.Items,
            signal: 'high',
            meta: {
                searchTerm: api_result.Name,
                itemType: 'Alternatives',
                sourceUrl: 'http://alternativeto.net/',
                sourceName: 'AlternativeTo'
            },
            normalize: function(item) {
                return {
                    ShortDescription: DDG.strip_html(DDG.strip_href(item.ShortDescription)),
                    url: item.Url,
                    icon: item.IconUrl,
                    title: item.Name,
                    description: item.ShortDescription
                };
            },
            templates: {
                group: 'icon',
        options: {
            footer: Spice.alternative_to.footer
        }
            }
        });
    };

    Handlebars.registerHelper("AlternativeTo_getPlatform", function (platforms) {
        return (platforms.length > 1) ? "Multiplatform" : platforms[0];
    });

}(this));
```

Just like the NPM Spice, Alternative.To uses `Spice.add()` with most of the same properties. However, it also uses a few new properties as well. The biggest difference between the two Spices though, is that the AlternativeTo API returns an array of items, which is given to `data`, rather than a single item like the NPM API. This means first and foremost, that we'll be dealing with a tile view, so that each item can be separately displayed. In order to do that, we must specify an `item` template which determines the content of each tile. Let's begin by taking a look at the new `Spice.add()` properties used by Alternative.To:

- `searchTerm` is used to indicate the term that was searched, stripped of unimportant words (e.g., "cat videos" would be "cat") or more formally, this is known as the *[noun adjunct](https://en.wikipedia.org/wiki/Noun_adjunct)*. The `searchTerm` will be used for the MetaBar wording where it reads, for example, "Showing 10 **iTunes** Alternatives", where "iTunes" is the `searchTerm` for the query "alternatives to iTunes".

- `itemType` is the type of item being shown (e.g., Videos, Images, Alternatives) and this is also used in the MetaBar. In the previous example, "Showing 10 **iTunes** Alternatives", "Alternatives" is the `itemType`.

- `normalize` allows you to normalize an item before it is passed on to the template. You can add or modify properties of the item that are used by your templates. In our case, we're using `normalize` to modify the `ShortDescription` property of each item, by removing HTML content from it and we also use it to add a few properties to our `item`, which our template will use.

    **Note:** This function uses jQuery's `$.extend()` method, so it will modify your `data` object by adding any returned properties that don't already exist, or simply overwrite the ones that do.

- `templates` is used to specify the template `group` and any other templates that are being used. Template `options` may also be provided to enable or disable template components used by the chosen `group`. In our case we've specified that we're using the `icon` template group and in the `options` block, we've specified the sub-template to be used for the `footer` component.

    The `icon` template has a few features including a `title`, `icon` and `description`. It also has an optional `footer` feature, which is actually a sub-template. We've created a **footer.handlebars** template and placed in the AlternativeTo Spice's share directory, **/share/spice/alternative_to**. We specify in the `options` block that the template to be used for the `footer` feature is the template we've created by referencing its name: `Spice.alternative_to.footer`.

------

Now, let's take a look at the Footer Handlebars template:

###### footer.handlebars (in /share/spice/alternative_to/)

```html
<div>
    {{Votes}} likes{{#if Platforms}} &bull; {{AlternativeTo_getPlatform Platforms}}{{/if}}
</div>
```

As you can see, this is some fairly simple HTML, which contains a few Handlebars expressions referencing properties of `data` as well as some Handlebars **helper** functions (i.e. `if` and `AlternativeTo_getPlatform`).

These helpers are really JavaScript functions, which operate on input and return their content to the template.

The `if` helper is a **block helper**, which acts like a normal `if` statement. When the specified variable exists, the code contained within the block, `{{#if}}...{{/if}}`, is executed. In our case, we use it to make sure the `Platforms` property is defined for the current item (remember we're looping over each item and applying this template) and if so, we add a bullet point, ` &bull; ` and the result of `{{AlternativeTo_getPlatform Platforms}}` to the page.

You may have noticed that `AlternativeTo_getPlatform` is actually defined alongside our `ddg_spice_alternative_to` callback function. Let's take a quick look at it:

###### alternative_to.js

```javascript
    Handlebars.registerHelper("AlternativeTo_getPlatform", function (platforms) {
        return (platforms.length > 1) ? "Multiplatform" : platforms[0];
    });
```

This code demonstrates how Handlebars helpers are created and made available to the templates. Using the `Handlebars.register()` method, you are able to specify the name of the helper you are registering, as well as the function it executes. The `AlternativeTo_getPlatform` helper is very simple: it takes an array as input and depending on the length, returns either the first element in the array, or if more than one element exists, returns the string "Multiplatforms".

The AlternativeTo Spice also uses a little bit of CSS to further customize and perfect the layout of the tiles. Let's take a look at the CSS:

###### alternative_to.css

```css
.tile--alternative_to .tile__icon {
    float: right;
    margin-top: 0;
    margin-right: 0;
}

.tile--alternative_to .tile__body {
    height: 13em;
}

.tile--alternative_to .tile__footer {
    bottom: 0.6em;
}
```

As you can see, this Spice requires very little CSS. This layout is a bit unique and so we opted to modify the layout of the content slightly. In most case the use of templates will alleviate the need to write custom CSS, however sometimes it is necessary and can be used sparingly.

The most important thing to note is that we have prefaced each of our CSS rules with the class `.tile--alternative_to`. Each Spice Instant Answer is wrapped in a `<div>` that has a class called `.zci--<spice_name>` where `<spice_name>` matches the Spice's package name. As well, when a tile view is used, *each tile* is wrapped in a `div` that has a class called `.tile--<spice_name>`. These allow us to **namespace** all the CSS rules for each individual Spice and their tiles. The is very important because DuckDuckGo simultaneously loads and triggers multiple Spice Instant Answers (depending on the query) and so namespaceing the CSS is necessary to ensure that none of our Spices' CSS rules affect other elements on the page. If your Spice requires any CSS, it **must** only target child elements of `.zci--<spice_name>` for the detail area and/or `.tile--<spice_name>` for the tiles.


<More to Come...>

<!-- ## Walkthrough #2: InTheaters (Medium)

The **InTheaters** Instant Answer is a little more advanced than **NPM** and **Alternative.To**, but it's still fairly easy to understand. Let's start by looking at the JavaScript:

###### in_theaters.js
 -->

<!--

We start by making sure that the `api_result` actually returned 1 or more results, if not we exit out, which will display nothing because no call has been made to `spice.add()`.

We then go on to define some functions used to determine which movie is the most relevant by taking into consideration the rating, release date and relevancy of the title, compared to the search terms. We won't go into the details of how the `score()` and `better()` functions are defined, but you'll notice that inside `better()` we use the function `DDG.isRelevant()`. This function takes as input a string and has an optional second input containing an array of strings. `DDG.isRelevant` can be used to compare the given string to the search terms and returns a `boolean` which lets us know if the input is considered "relevant" to the search terms. The optional 2nd input, the array of strings is called the **skip array** and it contains words which should be ignored when considering the relevancy of the search term and the input to `DDG.isRelevant`. In this case, we are using `DDG.isRelevant` to compare the title of the movies returned from the Rotten Tomatoes API to the user's search term. The skip array contains arbitrary words which are likely to be found in the query, that we assume aren't relevant to the title of the movie.

You'll also notice the use of `DDG_bestResult()`. This function takes as input a list of objects, and a comparator function. It then applies the comparator function, which takes two parameters, `currentbest` and `next` to each consecutive item in the input list. It assumes that the first item is the `currentbest`.

By this point we have either determined that there is a relevant movie to display, or we have found nothing to be relevant and have exited out. If we have a relevant movie, we then call `Spice.add()` as we would in any other Spice Instant Answer:

###### movie.js (continued)

```javascript
    Spice.render({
        data: result,
        source_name: 'Rotten Tomatoes',
        template_normal: "movie",
        template_small: "movie_small",
        force_no_fold: 1,
        source_url: result.links.alternate,
        header1: result.title + checkYear(result.year),
        image_url: result.posters.thumbnail.indexOf("poster_default.gif") === -1 ? result.posters.thumbnail : ""
    });
}
```

This is a fairly simple call to `Spice.add()`, but it slightly differs from other Instant Answers because it not only defines `template_normal`, the default template to be used, but it also defines `template_small` which is the template to be used when this Instant Answer is shown in a stacked state i.e., it is shown below another zero click result, but the content is minimal, preferably a single line of text.

Before looking at the implementation of the Handlebars helper functions, let's first take a look at the Movie Spice's Handlebars template to see how the helper functions are used:

###### movie.handlebars

```html
<div id="movie_data_box" {{#if hasContent}}class="half-width"{{/if}}>
    <div>
        {{#if ratings.critics_rating}}
            <span class="movie_data_item">{{ratings.critics_rating}}</span>
            <span class="movie_star_rating">{{{star_rating ratings.critics_score}}}</span>
            <div class="movie_data_description">
            ({{ratings.critics_score}}% critics,
             {{ratings.audience_score}}% audience approved)
            </div>
        {{else}}
            <span>No score yet...</span>
            <div class="movie_data_description">
                ({{ratings.audience_score}}% audience approved)
            </div>
        {{/if}}
    </div>

    <div><span class="movie_data_item">MPAA rating:</span>{{mpaa_rating}}</div>
    {{#if runtime}}
        <div><span class="movie_data_item">Running time:</span>{{runtime}} minutes</div>
    {{/if}}

    {{#if abridged_cast}}
        <div><span class="movie_data_item">Starring:</span>
            {{#concat abridged_cast sep=", " conj=" and "}}<a href="http://www.rottentomatoes.com/celebrity/{{id}}/">{{name}}</a>{{/concat}}.
        </div>
    {{/if}}
</div>

{{#if hasContent}}
    <span>
        {{#if synopsis}}
            {{condense synopsis maxlen="300"}}
        {{else}}
            {{condense critics_consensus maxlen="300"}}
        {{/if}}
    </span>
{{/if}}

```

In the template, we create a few `div`'s and reference properties of the context just like we did in **NPM** and **Alternative.To**. We also use a few more Handlebars helper functions, `{{#star_rating}}` and `{{#rating_adjective}}` which are defined in **movie.js** as well as `{{#concat}}` and `{{#condense}}`, which we've already discussed, and another block helper, `{{#if}}` (a default Handlebars helper) which should be self-explanatory.

We use the `{{#if}}` helper to check if a variable exists in the current context and then adds the contents of its own block to the template when the input variable does exist. As well, the `{{if}}` block allows the use of the optional `{{else}}` block which lets you add alternate content to the template when the input variable does not exist.

Moving on, let's take a look at the implementation of `{{#star_rating}}`:

###### movie.js (continued) - star_rating helper

```javascript
/* star rating */
Handlebars.registerHelper("star_rating", function(score) {
    var r = (score / 20) - 1;
    var s = "";

    if (r > 0) {
        for (var i = 0; i < r; i++) {
            s += "&#9733;";
        }
    }

    if (s.length == 0) {
        s = "0 Stars";
    }

    return s;
});
```

As you can see this is a pretty simple function, it takes a number as input, and use that to calculate a star rating. Then creates a string of ASCII stars and returns it to the template which will then be rendered by the browser to show a star rating of the movie.

Now let's take a look at the implementation of `{{#rating_adjective}}`:

###### movie.js (continued) - rating_adjective helper

```javascript
/*
 * rating_adjective
 *
 * help make the description of the movie grammatically correct
 * used in reference to the rating of the movie, as in
 *   'an' R rated movie, or
 *   'a'  PG rated movie
 */
Handlebars.registerHelper("rating_adjective", function() {
    return (this.mpaa_rating === "R"
         || this.mpaa_rating === "NC-17"
         || this.mpaa_rating === "Unrated") ?  "an" :"a";
});
```

Again, this is a fairly simple function which simply returns either "a" or "an" based on the rating of the movie.

Now that you've seen a more advanced Instant Answer and understand how to use Handlebars helpers, let's look at another advanced Instant Answer example.

## Walkthrough #3 - Quixey (Advanced Carousel Instant Answer)

The Quixey Instant Answer is one of our more advanced carousel Instant Answers which uses a considerable amount of Handlebars helpers and similarly to the **Movie** Instant Answer has a relevancy checking component. Let's begin by taking a look at the Quixey Instant Answer's JavaScript:

###### quixey.js

```javascript
// spice callback function
function ddg_spice_quixey (api_result) {

    if (api_result.result_count == 0) return;

    var q = api_result.q.replace(/\s/g, '+');
    var relevants = getRelevants(api_result.results);

    if (!relevants) return;

    Spice.render({
        data: api_result,
        source_name: 'Quixey',
        source_url: 'https://www.quixey.com/search?q=' + q,
        header1: api_result.q + ' (App Search)',
        force_big_header: true,
        more_logo: "quixey_logo.png",
        spice_name: 'quixey',
        template_frame: "carousel",
        template_options: {
            template_item: "quixey",
            template_detail: "quixey_detail",
            items: relevants
        }
    });

```

Similarly to **Alternative.To**, the Quixey Instant Answer uses the carousel, and sets values for all the required carousel-specific properties. However, this Instant Answer also uses the `force_big_header` property to create a ZeroClick header and subsequently sets the value of the header text, `header1`. Also, the `more_logo` property is set, which allows a custom image to be used instead of the `source_name` text for the "More at" link.

Similarly to the **Movie** Instant Answer, in the **Quixey** Instant Answer, we use the `getRelevants()` function (defined below in **Quixey.js**), which is used to check for relevant results before calling `Spice.add()`. We are required to get relevant results in this manner so that only the results we want included in the carousel are passed on to the **quixey.handlebars** template.

Moving on, let's take a look at the implementation of the `getRelevants()` helper:

###### quixey.js (continued) - getRelevants function

```javascript
// Check for relevant app results
function getRelevants (results) {

    var res,
        apps = [],
        backupApps = [],
        categories = /action|adventure|arcade|board|business|casino|design|developer tools|dice|education|educational|entertainment|family|finance|graphics|graphics and design|health and fitness|kids|lifestyle|medical|music|networking|news|photography|productivity|puzzle|racing|role playing|simulation|social networking|social|sports|strategy|travel|trivia|utilities|video|weather/i,
        skip_words = ["app", "apps", "application", "applications", "android", "droid", "google play store", "google play", "windows phone", "windows phone 8", "windows mobile", "blackberry", "apple app store", "apple app", "ipod touch", "ipod", "iphone", "ipad", "ios", "free", "search", "release", release date"];

    for (var i = 0; i < results.length; i++) {

        app = results[i];

        // check if this app result is relevant
        if (DDG.isRelevant(app.name.toLowerCase(), skip_words)) {
            apps.push(app);
        } else if (app.hasOwnProperty("short_desc") &&
                   DDG.isRelevant(app.short_desc.toLowerCase(), skip_words)) {
                        backupApps.push(app);
        } else if (app.custom.hasOwnProperty("category") &&
                   DDG.isRelevant(app.custom.category.toLowerCase(), skip_words)) {
                        backupApps.push(app);
        } else{
            continue;
        }
    }

    // Return highly relevant results
    if (apps.length > 0) {
        res = apps;
    }

    // Return mostly relevant results
    else if (backupApps.length > 0) {
        res = backupApps;
    }

    else {
        // No relevant results,
        // check if it was a categorical search
        // E.g."social apps for android"
        var q = DDG.get_query();
        res = q.match(categories) ? results : null;
    }
    return res;
});
```

We begin by defining the function and its input, `results` which is an array of apps. Then we define some variables, notable we define `skip_words`, which we will use later for a call to the `isRelevant()` function we discussed earlier. Then, we move onto a `for` loop which does the bulk of the work by iterating over every app in the `results` array and applies a series of `isRelevant()` checks to see if either the app name, short description or category are relevant to the search query. If the name is considered to be relevant we add it to the `apps` array which contains all the relevant app results. If the name isn't relevant but the description or category is, we add it to the `backupApps` array, because we might need them later. If none of those properties are considered relevant we simply exclude that app from the set of apps that will be displayed to the user.

After we've checked every app, we check to see if there were any relevant apps and if so, we show them to the user. Otherwise, we check our `backupApps` array to see if there were any apps who might be relevant and show those to the user. Failing that, we check if the search was for an app category and if so, we return all the results because the Quixey API is assumed to have relevant results.

Before looking at the implementation of the remaining Quixey Handlebars helpers, let's look at the template to see how the helpers are used:

###### quixey.handlebars

```html
<p><img src="{{{icon_url}}}" /></p>
<span>{{{condense name maxlen="40"}}}</span>
```

This template is very simple, it creates an `<img>` tag, for the resulting app icon and a `<span>` tag for the app name. You may also notice that unlike **Alternative.To**, we placed the `<img>` tag inside `<p>` tags. We do this to automatically center and align the images, through the use of carousel specific CSS that we wrote, because the images aren't all the same size and would otherwise be misaligned. So, if the images for your Instant Answer aren't the same size, simply wrap them in `<p>` tags and the carousel will take care of the rest. If not, simply ignore the use of the `<p>` tags.

Now let's take a look at the Quixey `carousel_template_detail` template. This template is more advanced, but most of the content is basic HTML which is populated by various `api_result` properties and Handlebars helpers:

###### quixey\_detail.handlebars (continued)

```html
<div id="quixey_preview" style="width: 100%; height: 100%;" app="{{id}}">
    <div class="app_info">
        <a href="{{{url}}}" class="app_icon_anchor">
            <img src="{{{icon_url}}}" class="app_icon">
        </a>
        <div class="name_wrap">
            <a href="{{url}}" class="name" title="{{name}}">{{name}}</a>
```

Here we create the outer div that wraps the content in the detail area. Note the use of HTML ids and classes - this is to make the css more straightforward, modular and understandable.

###### quixey\_detail.handlebars (continued)

```html
            {{#if rating}}
                <div title="{{rating}}" class="rating">
                    {{#loop rating}}
                        <img src="{{quixey_star}}" class="star"></span>
                    {{/loop}}
                </div>
            {{/if}}
```

Here we use the `{{#if}}` block helper and nested inside that, we use our own `{{#loop}}` block helper (defined internally), which simply counts from 0 to the value of its input, each time applying the content of its own block. In this example, we use it to create a one or more star images to represent the app's rating.

###### quixey\_detail.handlebars (continued)

```html
            <div class="price">{{pricerange}}</div>
            <div class="app_description">{{{short_desc}}}</div>
            <div id="details_{{id}}" class="app_details">
                <div class="app_editions">
                    {{#each editions}}
                        <div class="app_edition" title="{{name}} - Rating: {{rating}}">
                            <a href="{{{url}}}" class="app_platform">
                                {{#with this.platforms.[0]}}
                                <img src="{{platform_icon icon_url}}" class="platform_icon">
                                {{/with}}
                                {{platform_name}}
                                {{#if ../hasPricerange}}
                                     - {{price cents}}
                                {{/if}}
                            </a>
                        </div>
                    {{/each}}
                </div>
            </div>
        </div>
    </div>
    <div class="clear"></div>
</div>
```

Here, we create a few more `<div>`'s and then we use another block helper, `{{#each}}`, which takes an array as input, and iterates over each of the array's elements, using them as the context for the `{{#each}}` block. Nested within the `{{#each}]` helper, we also use the `#{{with}}` block helper, which takes a single object as input, and applies that object as the context for its block. One more interesting thing to note is the input we give to the `{{#if}}` block nested in our `{{#each}}` block. We use the `../` to reference the parent template's context.

Now that we've seen the template and the helpers we're using, let's take a look at how they're all implemented:

###### quixey.js (continued) -  qprice function

```javascript
// format a price
// p is expected to be a number
function qprice(p) {
    if (p == 0) {    // == type coercion is ok here
        return "FREE";
    }

    return "$" + (p/100).toFixed(2).toString();
}
```

This is a simple function that formats a price. We don't register it as a helper because we don't need to use this function directly in our templates, however our helper functions do use this function `qprice()` function.

###### quixey.js (continued) -  price helper

```javascript
// template helper for price formatting
// {{price x}}
Handlebars.registerHelper("price", function(obj) {
    return qprice(obj);
});
```

This helper function is relatively simple, it takes a number as input, calls the `qprice()` function we just saw, and returns its output to the template. It essentially abstracts our `qprice()` function into a Handlebars helper. We do this because the next function we'll see also uses `qprice()` and it's simply easier to call it as a locally defined function, rather than register it as a helper and then use the `Handlebars.helpers` object to call the `qprice()` function.

###### quixey.js (continued) -  pricerange helper

```javascript
// template helper to format a price range
Handlebars.registerHelper("pricerange", function(obj) {

    if (!this.editions)
        return "";

    var low  = this.editions[0].cents;
    var high = this.editions[0].cents;
    var tmp, range, lowp, highp;

    for (var i in this.editions) {
        tmp = this.editions[i].cents;
        if (tmp < low) low = tmp;
        if (tmp > high) high = tmp;
    }

    lowp = qprice(low);

    if (high > low) {
       highp = qprice(high);
       range = lowp + " - " + highp;
       this.hasPricerange = true;
    } else {
        range = lowp;
    }

    return range;
});
```

This function is a little more complex, it takes an object as input, iterates over the objects keys, and records the highest and lowest prices for the app. Then, it verifies that the range has different high and low values. If not, it simply returns the low price, formatted using our `qprice()` function. Otherwise, it creates a string indicating the range and formats the values with `qprice()`.

###### quixey.js (continued) -  platform\_icons helper

```javascript
// template helper to replace iphone and ipod icons with
// smaller 'Apple' icons
Handlebars.registerHelper("platform_icon", function(icon_url) {
    if (this.id === 2004 || this.id === 2015) {
        return "https://icons.duckduckgo.com/i/itunes.apple.com.ico";
    }

    return "/iu/?u=" + icon_url + "&f=1";
});
```

Another very simple helper function, the `platform_icon()` function simply checks if its input is equal to `2005` or `2015` and if so returns a special url for the platform icon. If not, it returns the original icon url but adds our proxy redirect, `/iu/?u=` as previously discussed.

###### quixey.js (continued) -  platform\_name helper

```javascript
// template helper that returns and unifies platform names
Handlebars.registerHelper("platform_name", function() {
    var name;
    var platforms = this.platforms;

    name = platforms[0].name;

    if (platforms.length > 1) {
        switch (platforms[0].name) {
            case "iPhone" :
            case "iPad" :
                name = "iOS";
                break;

            case "Blackberry":
            case "Blackberry 10":
                name = "Blackberry";
                break;
        }
    }

    return name;
});
```

This helper is also quite simple, it is used to return a platform name and sometimes also unifies the platform name when multiple platforms exist for an app. If the app is available for both 'iPhone' and 'iPad', the `switch()` will catch this and indicate the app is available for "iOS".

###### quixey.js (continued) -  quixey\_star helper

```javascript
// template helper to give url for star icon
Handlebars.registerHelper("quixey_star", function() {
    return DDG.get_asset_path("quixey", "star.png").replace("//", "/");
});
```

This helper is also very simple, but it is important because it uses the `DDG.get_asset_path()` function which returns the URI for an asset stored in an Instant Answer's share folder. This is necessary because Spice Instant Answers and their content are versioned internally. So the URI returned by this function will contain the proper version number, which is required to access any assets.

## Walkthrough #4 - Dictionary (More Advanced Instant Answer)

The dictionary Instant Answer is a more advanced Instant Answer than the previous examples, because it requires multiple endpoints (which means it has multiple perl modules -`.pm` files) in order to function properly. You will notice the `definition` endpoint is a sub-directory of the `dictionary` directory: `zeroclickinfo-spice/share/spice/dictionary/definition/`. In the case of the **Dictionary** Instant Answer, its Perl modules work together as one Instant Answer, however if the other endpoints worked separately from the `definition` endpoint, such as they do in the **[Last.FM](https://github.com/duckduckgo/zeroclickinfo-spice/tree/spice2/share/spice/lastfm)** Instant Answer, they would each have their own sub-directories and would also each have their own respective JavaScript, Handlebars and CSS files.

To begin, let's look at the first callback function definition in the Dictionary JavaScript:

###### dictionary\_definition.js

```javascript
// Description:
// Shows the definition of a word.
//
// Dependencies:
// Requires SoundManager2.
//
// Commands:
// define dictionary - gives the definition of the word "dictionary."
//
// Notes:
// ddg_spice_dictionary_definition - gets the definitions of a given word (e.g., noun. A sound or a combination of sounds).
// ddg_spice_dictionary_pronunciation - gets the pronunciation of a word (e.g., wûrd).
// ddg_spice_dictionary_audio - gets the audio file.
// ddg_spice_dictionary_reference - handles plural words. (Improve on this in the future.)
```

The comments at the beginning of the file explain what the various callbacks are for. Each of these callback functions is connected to a different endpoint, meaning they each belong to a different Perl module. As you can see, the name of each callback correlates to the name of the perl module. So `dictionary_definition()` is the callback for `DDG::Spice::Dictionary::Definition`, likewise `dictionary_audio` is for `DDG::Spice::Dictionary::Audio`, etc.

Each of these endpoints are used to make different API calls (either to a different endpoint or possibly even a different API altogether), which can only be done by creating a different Perl module for each endpoint. We can make these endpoints work together for a given Instant Answer by using the jQuery `getScript()` function which makes an AJAX call to a given endpoint, which results in a call to that endpoint's callback function. This function needs to be defined before it is called, so the Dictionary Instant Answer defines all **four** callback functions in **dictionary\_definition.js**

Moving on, let's take a look at the implementation of the `Spice.add()` call and the `dictionary_definition()`  callback:

###### dictionary\_definition.js (continued) - dictionary_definition callback

```javascript
// Dictionary::Definition will call this function.
// This function gets the definition of a word.
function ddg_spice_dictionary_definition (api_result) {
    "use strict";
    var path = "/js/spice/dictionary";

    // We moved Spice.render to a function because we're choosing between two contexts.
    var render = function(context, word, otherWord) {
        Spice.render({
            data              : context,
            header1           : "Definition (Wordnik)",
            force_big_header  : true,
            source_name       : "Wordnik",
            source_url        : "http://www.wordnik.com/words/" + word,
            template_normal   : "dictionary_definition"
        });

        // Do not add hyphenation when we're asking for two words.
        // If we don't have this, we'd have results such as "black• hole".
        if(!word.match(/\s/)) {
            $.getScript(path + "/hyphenation/" + word);
        }

        // Call the Wordnik API to display the pronunciation text and the audio.
        $.getScript(path + "/pronunciation/" + otherWord);
        $.getScript(path + "/audio/" + otherWord);
    };
```

We begin by wrapping the `Spice.add()` call in a function which also does a little extra work. Specifically after rendering the result it calls the Wordnik API, this time using two different API endpoints. The first gets the pronunciation text, the second gets the audio file for the pronunciation of the word. As mentioned, these endpoints are used to work together as one Instant Answer, so, using the returns from the separate API calls, we construct one dictionary Instant Answer result which contains the word definition, the pronunciation text and the audio recording of the pronunciation.

The reason for wrapping the `Spice.add()` call in a function is because we need to be able to call our `render()` function from both the `dictionary_definition()` callback as well as the `dictionary_reference()` callback, as you will see below:

###### dictionary\_definition.js (continued) - dictionary_definition callback

```javascript
    // Expose the render function.
    ddg_spice_dictionary_definition.render = render;

    // Prevent jQuery from appending "_={timestamp}" in our url when we use $.getScript.
    // If cache was set to false, it would be calling /js/spice/dictionary/definition/hello?_=12345
    // and that's something that we don't want.
    $.ajaxSetup({
        cache: true
    });

    // Check if we have results we need.
    if (api_result && api_result.length > 0) {

        // Wait, before we display the Instant Answer, let's check if it's a plural
        // such as the word "cacti."
        var singular = api_result[0].text.match(/^(?:A )?plural (?:form )?of <xref>([^<]+)<\/xref>/i);

        // If the word is plural, then we should load the definition of the word
        // in singular form. The definition of the singular word is usually more helpful.
        if(api_result.length === 1 && singular) {
            ddg_spice_dictionary_definition.pluralOf = api_result[0].word;
            $.getScript(path + "/reference/" + singular[1]);
        } else {
            // Render the Instant Answer if everything is fine.
            render(api_result, api_result[0].word, api_result[0].word);
        }
    }
};
```

After defining the `render()` function we give the function a `render` property, `ddg_spice_dictionary_definition.render = render;` (so we can access the `render()` function from other callbacks) and then move on to check if we actually have any definition results returned from the API. If so, we then check if the queried word is a plural word and if so, make another API call for the singular version of the queried word. This call, `$.getScript(path + "/reference/" + singular[1]);` will result in calling the `dictionary_reference()` callback which eventually calls our `render()` function to show our Spice result on the page. If the word is not a plural, we instead immediately call the `render()` function and display our result.

**Note:** More info on the jQuery `$.getScript()` method is available [here](http://api.jquery.com/jQuery.getScript/).

###### dictionary\_definition.js (continued) - dictionary_reference callback

```javascript
// Dictionary::Reference will call this function.
// This is the part where we load the definition of the
// singular form of the word.
function ddg_spice_dictionary_reference (api_result) {
    "use strict";

    var render = ddg_spice_dictionary_definition.render;

    if(api_result && api_result.length > 0) {
        var word = api_result[0].word;

        // We're doing this because we want to say:
        // "Cacti is the plural form of cactus."
        api_result[0].pluralOf = word;
        api_result[0].word = ddg_spice_dictionary_definition.pluralOf;

        // Render the Instant Answer.
        render(api_result, api_result[0].word, word);
    }
};
```

In this relatively simple callback, we begin by using the previously defined render property of the `dictionary_definition()` function to give this callback access to the `render()` function we defined at the beginning of `quixey.js`. Then we confirm that this callback's `api_result` actually received the singular form of the originally searched query. If so, we add the singular and plural form of the word to our `api_result` object so we can check for and use them later in our Handlebars template.

###### dictionary\_definition.js (continued) - dictionary_hyphenation callback

```javascript
// Dictionary::Hyphenation will call this function.
// We want to add hyphenation to the word, e.g., hello -> hel•lo.
function ddg_spice_dictionary_hyphenation (api_result) {
    "use strict";

    var result = [];
    if(api_result && api_result.length > 0) {
        for(var i = 0; i < api_result.length; i += 1) {
            result.push(api_result[i].text);
        }
        // Replace the, rather lame, non-hyphenated version of the word.
        $("#hyphenation").html(result.join("•"));
    }
};
```

This callback is also fairly simple. If the API returns a result for the hyphenated version of the word, we loop over the response to get the various parts of the word, then join them with the dot character "•", and inject the text into the HTML of the **#hyphenation** `<div>` using jQuery.

###### dictionary\_definition.js (continued) - dictionary_pronunciation callback

```javascript
// Dictionary::Pronunciation will call this function.
// It displays the text that tells you how to pronounce a word.
function ddg_spice_dictionary_pronunciation (api_result) {
    "use strict";

    if(api_result && api_result.length > 0 && api_result[0].rawType === "ahd-legacy") {
        $("#pronunciation").html(api_result[0].raw);
    }
};
```

Similarly to the `dictionary_hyphenation()` callback, this callback receives a phonetic spelling of the queried word and injects it into the Spice result by using jQuery as well to modify the HTML of the **#pronunciation** `<div>`.

###### dictionary\_definition.js (continued) - dictionary_audio callback

```javascript
// Dictionary::Audio will call this function.
// It gets the link to an audio file.
function ddg_spice_dictionary_audio (api_result) {
    "use strict";

    var isFailed = false;
    var url = "";
    var icon = $("#play-button");

    // Sets the icon to play.
    var resetIcon = function() {
        icon.removeClass("widget-button-press");
    };

    // Sets the icon to stop.
    var pressIcon = function() {
        icon.addClass("widget-button-press");
    };
```

This callback begins by defining a few simple functions and some variables to used below. Again, jQuery is used to modify the DOM as needed in this callback.

```javascript
    // Check if we got anything from Wordnik.
    if(api_result && api_result.length > 0) {
        icon.html("▶");
        icon.removeClass("widget-disappear");

        // Load the icon immediately if we know that the url exists.
        resetIcon();

        // Find the audio url that was created by Macmillan (it usually sounds better).
        for(var i = 0; i < api_result.length; i += 1) {
            if(api_result[i].createdBy === "macmillan" && url === "") {
                url = api_result[i].fileUrl;
            }
        }

        // If we don't find Macmillan, we use the first one.
        if(url === "") {
            url = api_result[0].fileUrl;
        }
    } else {
        return;
    }
```

The callback then verifies the API returned a pronunciation of the queried word and if so, injects a play icon, "▶" into the **#play-button** `<button>` and grabs the url for the audio file from the API response.

```javascript
    // Load the sound and set the icon.
    var isLoaded = false;
    var loadSound = function() {
        // Set the sound file.
        var sound = soundManager.createSound({
            id: "dictionary-sound",
            url: "/audio/?u=" + url,
            onfinish: function() {
                resetIcon();
                soundManager.stopAll();
            },
            ontimeout: function() {
                isFailed = true;
                resetIcon();
            },
            whileplaying: function() {
                // We add this just in case onfinish doesn't fire.
                if(this.position === this.durationEstimate) {
                    resetIcon();
                    soundManager.stopAll();
                }
            }
        });

        sound.load();
        isLoaded = true;
    };
```

Here, we define a function, `loadSound()` that uses the [**SoundManager**](http://www.schillmania.com/projects/soundmanager2/) JavaScript library to load the audio file and also allows us to easily control the playing of the audio. An important piece of this `loadSound()` function is the use of our audio proxy: `url: "/audio/?u=" + url`. Similarly to any images used in a Instant Answer, any audio files must also be proxied through DuckDuckGo to ensure our users' privacy.

**Note:** The use of the SoundManager library for this Instant Answer shouldn't be taken lightly. We chose to use a JavaScript library to ensure cross-browser compatibility but the use of 3rd party libraries is not something we advocate, however since this was an internally written Instant Answer, we decided to use the SoundManager library for this Instant Answer as well as all others which utilize audio (e.g., [Forvo](https://duckduckgo.com/?q=pronounce+awesome)).

```javascript
    // Initialize the soundManager object.
    var soundSetup = function() {
        window.soundManager = new SoundManager();
        soundManager.url = "/soundmanager2/swf/";
        soundManager.flashVersion = 9;
        soundManager.useFlashBlock = false;
        soundManager.useHTML5Audio = false;
        soundManager.useFastPolling = true;
        soundManager.useHighPerformance = true;
        soundManager.multiShotEvents = true;
        soundManager.ontimeout(function() {
            isFailed = true;
            resetIcon();
        });
        soundManager.beginDelayedInit();
        soundManager.onready(loadSound);
    };
```

As the comment explains, this function is used to initialize SoundManager so we can then use it to control the audio on the page.

```javascript
    // Play the sound when the icon is clicked. Do not let the user play
    // without window.soundManager.
    icon.click(function() {
        if(isFailed) {
            pressIcon();
            setTimeout(resetIcon, 1000);
        } else if(!icon.hasClass("widget-button-press") && isLoaded) {
            pressIcon();
            soundManager.play("dictionary-sound");
        }
    });
```

Here we define a click handler function using jQuery. Based on the state of the sound widget, `isFailed`, the handler either

```javascript
    // Check if soundManager was already loaded. If not, we should load it.
    // See http://www.schillmania.com/projects/soundmanager2/demo/template/sm2_defer-example.html
    if(!window.soundManager) {
        window.SM2_DEFER = true;
        $.getScript("/soundmanager2/script/soundmanager2-nodebug-jsmin.js", soundSetup);
    } else {
        isLoaded = true;
    }
};
```

Now that we've seen how all the API callback functions are implemented, let's take a look at the Handlebars to see what helpers are used and how the display is built:

```html
<div>
    <b id="hyphenation">{{this.[0].word}}</b>
    {{#if this.[0].pluralOf}}
        <span> is the plural form of {{this.[0].pluralOf}}</span>
    {{/if}}
    <span id="pronunciation"></span>
    <button id="play-button" class="widget-button widget-disappear"></button>
</div>
{{#each this}}
    <div class="definition">
        <i>{{part partOfSpeech}}</i>
        <span>{{{format text}}}</span>
    </div>
{{/each}}
```

As you can see, the template and layout for the dictionary Spice are relatively simple. We begin by placing the term to be defined in a `<b>` tag. As you can see, to access the element from the context, we need to use a special array notation: `this.[0].word`, where the `[0]` indicates the first element in the array.

We then check if the `this.[0].pluralOf` variable has been set. As you may recall, we set this variable in the `dictionary_reference()` callback function, after checking in the `dictionary_definition()` callback if the queried term is a plural. If the `pluralOf` variable has been set we then create a `<span>` tag and for a sentence to indicate which word the queried word is a plural of.

Then the template creates two empty elements, a `<span>` tag to contain the phonetic spelling, which may or may not be populated by our `dictionary_pronunciation()` callback, depending on whether or not the API has a phonetic spelling for the queried word. Similarly we create an empty `<button>` tag to play an audio recording of the word pronunciation which is potentially populated by the `dictionary_audio()` callback, again if the API has an audio file for the queried word's pronunciation.

The template then uses a Handlebars `{{#each}}` helper to iterate over the context (because it is an array in this case, not an object) and for each element creates a snippet of text indicating the usage of the term (e.g., noun, verb) and provides the definition of the term. This `{{#each}}` helper also uses two Handlebars helpers defined in **dictionary\_definition.js**, `{{part}}` and `{{format}}`. Let's take a look at how they're implemented:

###### dictionary\_definition.js (continued) - part helper

```javascript
// We should shorten the part of speech before displaying the definition.
Handlebars.registerHelper("part", function(text) {
    "use strict";

    var part_of_speech = {
        "interjection": "interj.",
        "noun": "n.",
        "verb-intransitive": "v.",
        "verb-transitive": "v.",
        "adjective": "adj.",
        "adverb": "adv.",
        "verb": "v.",
        "pronoun": "pro.",
        "conjunction": "conj.",
        "preposition": "prep.",
        "auxiliary-verb": "v.",
        "undefined": "",
        "noun-plural": "n.",
        "abbreviation": "abbr.",
        "proper-noun": "n."
    };

    return part_of_speech[text] || text;
});
```

As the comment explains, this simple helper function is used to shorten the "part of speech" word returned by the API.

###### dictionary\_definition.js (continued) - format helper

```javascript
// Make sure we replace xref to an anchor tag.
// <xref> comes from the Wordnik API.
Handlebars.registerHelper("format", function(text) {
    "use strict";

    // Replace the xref tag with an anchor tag.
    text = text.replace(/<xref>([^<]+)<\/xref>/g,
                "<a class='reference' href='https://www.wordnik.com/words/$1'>$1</a>");

    return text;
});
```

This helper is used to create hyperlinks within the word definition text. The Wordnik API we are using for this Instant Answer provides definitions which often contain words or phrases that are wrapped in `<xref>` tags indicating that Wordnik also has a definition for that word or phrase. This helper is used to replace the `<xref>` tags with `<a>` tags that link to a search for that particular word on **Wordnik.com**.

Now that we have seen the Handlebars template and all looked over all the JavaScript related to the dictionary Instant Answer, let's take a look at the CSS used to style the display of the result:

###### dictionary_definition.css

```css
#spice_dictionary_definition .widget-button {
    background: #eee; /* Old browsers */
    background: #eee -moz-linear-gradient(top, rgba(255,255,255,.1) 0%, rgba(0,0,0,.1) 100%); /* FF3.6+ */
    background: #eee -webkit-gradient(linear, left top, left bottom, color-stop(0%,rgba(255,255,255,.1)), color-stop(100%,rgba(0,0,0,.1))); /* Chrome,Safari4+ */
    background: #eee -webkit-linear-gradient(top, rgba(255,255,255,.1) 0%,rgba(0,0,0,.1) 100%); /* Chrome10+,Safari5.1+ */
    background: #eee -o-linear-gradient(top, rgba(255,255,255,.1) 0%,rgba(0,0,0,.1) 100%); /* Opera11.10+ */
    background: #eee -ms-linear-gradient(top, rgba(255,255,255,.1) 0%,rgba(0,0,0,.1) 100%); /* IE10+ */
    background: #eee linear-gradient(top, rgba(255,255,255,.1) 0%,rgba(0,0,0,.1) 100%); /* W3C */

    border-left: 1px solid #ccc;
    border-right: 0;
    border-top: 0;
    border-bottom: 0;

    -webkit-border-radius: 4px;
    -moz-border-radius: 4px;
    border-radius: 4px;

    color: #444;
    display: inline-block;
    font-size: 11px;
    font-weight: bold;
    text-decoration: none;
    text-shadow: 0 1px rgba(255, 255, 255, .75);
    cursor: pointer;
    line-height: normal;
    padding: 2px 5px;
    vertical-align: text-bottom;
}

#spice_dictionary_definition .widget-button-press {
    border-color: #666;
    background: #ccc; /* Old browsers */
    background: #ccc -moz-linear-gradient(top, rgba(255,255,255,.25) 0%, rgba(10,10,10,.4) 100%); /* FF3.6+ */
    background: #ccc -webkit-gradient(linear, left top, left bottom, color-stop(0%,rgba(255,255,255,.25)), color-stop(100%,rgba(10,10,10,.4))); /* Chrome,Safari4+ */
    background: #ccc -webkit-linear-gradient(top, rgba(255,255,255,.25) 0%,rgba(10,10,10,.4) 100%); /* Chrome10+,Safari5.1+ */
    background: #ccc -o-linear-gradient(top, rgba(255,255,255,.25) 0%,rgba(10,10,10,.4) 100%); /* Opera11.10+ */
    background: #ccc -ms-linear-gradient(top, rgba(255,255,255,.25) 0%,rgba(10,10,10,.4) 100%); /* IE10+ */
    background: #ccc linear-gradient(top, rgba(255,255,255,.25) 0%,rgba(10,10,10,.4) 100%); /* W3C */ }


    /* Fix for odd Mozilla border & padding issues */
    button::-moz-focus-inner,
    input::-moz-focus-inner {
    border: 0;
    padding: 0;
}

#spice_dictionary_definition .widget-disappear {
  display: none;
}

#spice_dictionary_definition #play-icon {
  line-height: normal;
}

#spice_dictionary_definition .definition em {
    font-style: italic;
}
```
Most of the above CSS has actually been borrowed from the [Skeleton](http://getskeleton.com) framework, to recreate their button styling. Understanding that particular CSS isn't very important here, however what is important to understand is that we have targeted every CSS rule to only apply to elements found within the element with an ID of **#spice\_dictionary\_definition**. Every spice Instant Answer is automatically wrapped in a div with an ID of "#spice_spiceCallbackName". This allows you to force any/all CSS to only apply to the elements on the page related to the Spice Instant Answer.

As you can see, most of this CSS is specific to the `.widget-button` class and is used to style the look of the play button. Also its worth mentioning that this particular CSS has been written to be very cross-browser compatible as you can see by the comments which indicate the browsers each line has been written for.

As you can see, the Dictionary Instant Answer is one of the most involved Spice Instant Answers we have due to its use of multiple endpoints and their respective callback functions. Most Instant Answers however shouldn't need to be so complex in order to function, so we greatly prefer that Instant Answers are built as simple and straightforward as possible.
 -->