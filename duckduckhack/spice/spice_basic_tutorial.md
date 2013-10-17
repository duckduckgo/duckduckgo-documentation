# Basic Spice Tutorial

In this tutorial, we'll be making a Spice instant answer that let's you search for Node.js packages with [the Node.js package search API](http://registry.npmjs.org/uglify-js/latest). The end result works [like this](https://duckduckgo.com/?q=Npm+How+many+characters+are+in+this+sentence%3F) and the first part, the "backend" component, will look like this:

# NPM Spice - Backend (Perl)

###### Npm.pm

```perl
package DDG::Spice::Npm;
# ABSTRACT: Give the number of characters (length) of the query.

use DDG::Spice;

triggers start => 'Npm';

spice to => 'http://registry.npmjs.org/$1/latest';
spice wrap_jsonp_callback => 1;

handle remainder => sub {
    return 'Npm: ' . length $_ if $_;
    return;
};
1;

```

## Naming our Spice Package

To begin, open your favourite text editor like [gedit](http://projects.gnome.org/gedit/), notepad or [emacs](http://www.gnu.org/software/emacs/) and type the following:

```perl
package DDG::Spice::Npm;
# ABSTRACT: Returns package information from npm package manager's registry.
```

Each instant answer is a [Perl package](https://duckduckgo.com/?q=perl+package), so we start by declaring the package namespace. For a new Spice (or any new instant answer), you would change **npm** to the name of the instant answer (written in [CamelCase](https://duckduckgo.com/?q=camelcase) format).

The second line is a special comment line that is used for documentation purposes.

## Import the Spice Class

Next, type the following [use statement](https://duckduckgo.com/?q=perl+use) to import [the magic behind](https://github.com/duckduckgo/duckduckgo/tree/master/lib/DDG) our instant answer system.

```perl
use DDG::Spice;
```

**\*\*Note:** Right after the above line, you should include any Perl modules that you'll be leveraging to help generate the answer. **Make sure** you add those modules to the `dist.ini` file in this repository. If you're not using any additional modules, carry on!

## Define the Trigger Word(s)

On the next line, type:

```perl
triggers start => 'npm';
```

**triggers** are keywords/phrases that tell us when to make the instant answer run. When a particular *trigger word* (or phrase) is part of a search query, it tells DuckDuckGo to *trigger* the instant answer(s) that have indicated they should trigger for the given word (or phrase).

In this case there is one trigger word: "**npm**". 

Let's say someone searched "**npm uglify-js**". **npm** is the *first* word, so it would trigger our Spice because the **start** keyword says, "Make sure the *trigger word* is at the *start* of the query." 

There are several other keywords like **start** which will be covered shortly. The **=>** symbol is there to separate the trigger words from the keywords (for readability).

## Define the API Call

On the next line enter:

```perl
spice to => 'http://registry.npmjs.org/$1/latest';
```

The spice **to** is used to define the URL that the Spice will use to make an API request. The URL has a **$1** placeholder, which will eventually be populated with whatever value our `handle` function (which we'll define shortly) returns. In most cases, Spice instant answers tend to use some sort of search endpoint for a given API. We need to indicate in our API request what it is we're searching for and so the `handle` function and the `spice to` URL work together to send our search term(s) to the API by replacing the **$1** placeholder, with the term(s) we're searching for.

Using the previous example, if we wanted to search for "**uglify.js**" with the Node.js API, we'd need to replace `$1` with `uglify_js` which would result in this URL: <http://registry.npmjs.org/uglify-js/latest>. If you follow that link, you'll notice the API returns a JSON object containing all the data pertaining to the "Uglify-JS" NPM Package.

## Indicate our Callback Function

In most cases, API's allow for a "callback" parameter, which usually look like this:

```perl
http://www.api.awesome.com/?q=<search_term>&callback=<function_name>
```

This parameter is used to wrap the JSON object being returned in a JavaScript function call, to the function named in the callback parameter. Unfortunately, the Node.js API doesn't allow for this parameter to be specified, so we force this manually by using the **spice wrap\_jsonp\_callback** function. Enter this text on the next line to do this:

```perl
spice wrap_jsonp_callback => 1;
```

Now, when the JSON is returned by the API, it will be wrapped in a call to our Spice's JavaScript callback function, which we'll define later.

------

**If the API *did* support the callback parameter**, our spice to would look like this:

```perl
spice to => 'http://registry.npmjs.org/$1/latest?callback={{callback}}';
```

Where `{{callback}}` is another special placeholder which will be **automatically** replaced with the correct spice callback function name.

## Define the Handle Function

Moving on, enter this on the next line:

```perl
handle remainder => sub {
```

Once triggers are specified, we define how to *handle* the query. `handle` is another keyword, similar to **triggers**.

You can *handle* different parts of the search query, but the most common is the **remainder**, which refers to the remainder of the query, after the first matched trigger word/phrase has been removed. 

For example, if the query was "**npm uglify-js**", the trigger would be *npm* and the remainder would be *uglify-js*.

Now let's add a few more lines to complete the handle function:

```perl
handle remainder => sub {
    return $_ if $_;
    return;
};
```

This function (the part within the **{}**, after **sub**) is a very important part of the Spice. It defines what our Spice instant answer will replace the **$1** placeholder with.

Whatever you are *handling* is passed to the `handle` function in the **$\_** variable ( **$\_** is a special default variable in Perl that is commonly used to store temporary values). For example, if you searched DuckDuckGo for *"npm uglify-js"*, the value of **$\_** will be *"this is a test"*, i.e. the **remainder** of the query.

Let's take a closer look at the first line of the function:

```perl
return $_ if $_;
```

The heart of the function is just this one line. The **remainder** is in the **$\_** variable as discussed. If it is not blank ( **if $\_** ), we return the **$\_** variable, which as we just saw, contains the **remainder** of the query.

If we are unable to provide a good instant answer, we simply **return nothing**. That's exactly what the second line in the function does:

```perl
return;
```

This line is only run if **$\_** contained nothing, because otherwise the line before it would return something and end the function execution.

If for example you searched DuckDuckGo for "npm", this would trigger our NPM Spice, and then in the `handle` function the value of **$\_**, the **remainder** of the query, would be blank (because "npm" is the trigger word and would have been stripped out) and so our handle function would **return nothing**, meaning no API call would be made, and no result will be displayed.

## Return True at EOF

Finally, all Perl packages that load correctly should [return a true value](http://stackoverflow.com/questions/5293246/why-the-1-at-the-end-of-each-perl-package) so add a 1 on the very last line, and make sure to also add a newline at the end of the file.

```perl
1;

```

And that's it! At this point you have a working Spice instant answer. 
## Recap (So Far)
The instant answer system works like this at the highest level:

- We break the query (search terms) down into seperate words, which is a process that happens in the background.

- We see if any of those words or groups of words are **triggers** for any instant answers. These **triggers** are defined by the developer when creating an instant answer. In the example we used above, the trigger word is "**npm**".

- If a Spice is triggered, we run its `handle` function.

- If the Spice's handle function returns a value, it is used to replace our **$1** placeholder in the **spice to** URL, and then a request is made to to that url. When the API responds with a JSON object, it is wrapped, making the JSON object the input to our javascript callback function (which will now define!)

------

# NPM Spice - Backend (JavaScript)

As mentioned, every instant answer requires a Spice callback function. For the *NPM* instant answer, the callback function will be named `ddg_spice_npm()` and will be defined in the **npm.js** file. 

The name of the callback function is determined by the **Npm.pm** Perl module we wrote, which specifies the name of the package, `DDG::Spice::NPM`. The portion after `DDG::Spice::` is lowercased and converted from camel case to underscore seperated (ie. `DDG::Spice::CamelCase` -> `ddg\_spice\_camel_case`) in order to create the name of our callback function. This generated name is what the previous `{{callback}}` placeholder will be replaced with. Similarly, if we instead had to use `spice wrap_jsonp_callback`, that will also wrap the JSON returned by the api with a function call to this generated callback name.

To clarify:

```perl
{{callback}} => ddg_spice_npm

or

{ JSON_API_RESPONSE: 1, ... } => ddg_spice_npm( { JSON_API_RESPONSE: 1, ... } );
```

The final **npm.js** will look like this:

###### npm.js

```javascript
function ddg_spice_npm (api_result) {
    if (api_result.error) return;

    Spice.render({
         data              : api_result,
         force_big_header  : true,
         header1           : api_result.name + ' (' + api_result.version + ')',
         source_name       : "npmjs.org", // More at ...
         source_url        : 'http://npmjs.org/package/' + api_result.name,
         template_normal   : 'npm',
    });
}
```

Let's go through it line-by-line:

###### npm.js (continued)

```perl
function ddg_spice_npm (api_result) {
```

We begin by defining our callback function, `ddg_spice_npm`. The name we specify here ***must*** match the name that would be determined from the package name (as we discussed above). We also specify that the callback function takes one input paramter, which we have named `api_result`. All spice callback functions should look like this. The name for the input should **always** be called `api_result`. This is part of our naming convention and helps to standardize the JavaScript code.

###### npm.js (continued)

```javascript
if (api_result.error) return;
```

Here, we specify that if the `error` object in the API result is defined, we `return` nothing, stopping the execution of the function and as a result, we won't display an instant answer. In the case of this API, when the error object is defined, it means no results are given, so we have no data to use for a Spice result.

In other cases, because most API's return an array of results, a similar check should be made to see if the the results array has a length greater than `1`. This way, if no results were returend from the API we can stop, and display nothing.

Moving on, the next part is very important, it defines how the Spice result should look and specifies which parts of the API result are important. This piece of code tells DuckDuckGo to render the instant answer:

###### npm.js (continued)

```javascript
Spice.render({
     data              : api_result,
     force_big_header  : true,
     header1           : api_result.name + ' (' + api_result.version + ')',
     source_name       : "npmjs.org",
     source_url        : 'http://npmjs.org/package/' + api_result.name,
     template_normal   : 'npm',
});
```

Here we make a call to the `Spice.render()` function that the instant answer system has already defined, which operates on an input object. Let's go over each of the parameters specified in the object we give to `Spice.render()`:

- `data` is perhaps the most important parameter. The object given here will be the object that is passed along to the Handlebars template. In this case, the context of the NPM template will be the **api_result** object. This is very important to understand because **only the data passed along to the template is accessible to the template**. In most cases the `data` parameter should be set to `api_result` so all the data returned from the API is accessible to the template. 

- `force_big_header` is related to the display formatting. It forces the system to display the large grey header bar that you see when you click the example link above. 

- `header1` is the text of this header, i.e. the text displayed inside the large grey bar, at the top of an instant answer. 

- `source_name` is the name of the source for the "**More at <source>**" link that's displayed below the text of the instant answer for attribution purposes. 

- `source_url` is the target of the "**More at**" link. It's the page that the user will click through to.

- `template_normal` is the name of the Handlebars template for your instant answer.

------

At this point, the rendering of the instant answer changes context from JavaScript to Handlebars.js. As mentioned, our `Spice.render()` call specified our template, and the data to be used by the template. What `Spice.render()` actually does, is apply the given template, with the `data` as input. So now, let's look at the NPM instant answer's Handlebars template, to see how it displays the instant answer result:

###### npm.handlebars

```html
<div>
    <div>{{description}}</div>
    <pre> $ npm install {{name}}</pre>
</div>
```

As you can see, this is a special type of HTML template. Within the template, you can refer directly to objects that are returned by the API (which were passed along through our `data` parameter). `description` and `name` are both from the `api_result` object that we discussed earlier which containts the data returned by the API. 

All of `api_result`'s sub-objects (e.g. `name`, `description`) are 
in the template's scope. You can access them by name using double or triple curly braces (triple braces **will not** escape the contents -- and so should be avoided unless absolutely necessarry). Here, we just create a basic HTML skeleton and fill it in with the proper information, my indicating which variables should go where. `{{description}}` and `{{name}}` call also be though of as placeholders which will be replaced by their respective values as defined in the `api_result` object.

And that's it, you're done! You should now have a working Spice instant answer.

## Recap

We've created two files in the Spice share directory `share/spice/npm/`:

1. `npm.js` - which delegates the API's response and calls `Spice.render()`
2. `npm.handlebars` - which specifies the instant answer's HTML structure and determines which attributes of the API response are placed in the HTML result

You may notice other instant answers also include a css file. For **NPM** the use of CSS wasn't necessary and this is also true for many other instant answers. This is primarly the reason why we've created a template system. It helps to alleviate the need for styling through css and also helps normalize the look and feel of all instant answers. In some cases however, the light use of CSS for styling is needed and can be added. Example Spice instant answers with CSS usage will be covered shortly.

Again, the Spice instant answer system works like so:

- We break the query (search terms) down into seperate words, which is a process that happens in the background.

- We see if any of those words or groups of words are **triggers** for any instant answers. These **triggers** are defined by the developer when creating an instant answer. In the example we used above, the trigger word is "**npm**".
- If a Spice is triggered, we run its `handle` function.
- If the Spice's handle function returns a value, it is used to replace our **$1** placeholder in the **spice to** URL, and then a request is made to to that url. When the API responds with a JSON object, it is wrapped, making the JSON object the input to our javascript callback function
- Our JavaScript callback function takes the API result (JSON Object), and passes it along to our `Spice.render()` call which specifies, using the elements of the JSON object, which parts are to be used in creating the instant answer "header", "More at" link and most importantly, passes along our JSON object to our Spice's Handlebars template.
- The template then defines using HTML and variables, what the actual content for the Spice result will be
- This content is then created and rendered onto the page by the Spice system's backend.