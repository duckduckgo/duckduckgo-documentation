d# Basic Spice Tutorial

In this tutorial, we'll be making a Spice instant answer that lets you search for Node.js packages, using the [Node Packaged Modules API](http://registry.npmjs.org/uglify-js/latest). The end result works [like this](https://next.duckduckgo.com/?q=npm+http-server) and the first part, the "backend" component, will look like this:

# NPM Spice - Backend (Perl)

###### Npm.pm

```perl
package DDG::Spice::Npm;
# ABSTRACT: Returns package information from npm package manager's registry.

use DDG::Spice;

triggers startend => 'npm';

spice to => 'http://registry.npmjs.org/$1/latest';
spice wrap_jsonp_callback => 1;

handle remainder => sub {
    return $_ if $_;
    return;
};

1;
```

## Naming our Spice Package

To begin, open your favorite text editor like [gedit](http://projects.gnome.org/gedit/), notepad or [emacs](http://www.gnu.org/software/emacs/) and type the following:

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
triggers startend => 'npm';
```

**triggers** are keywords/phrases that tell us when to make the instant answer run. When a particular *trigger word* (or phrase) is part of a search query, it tells DuckDuckGo to *trigger* the instant answer(s) that have indicated they should trigger for the given word (or phrase).

In this case there is one trigger word: "**npm**". 

Let's say someone searched "**npm uglify-js**". "**npm**" is the *first* word, so it would trigger our Spice because the **startend** keyword says, "Make sure the *trigger word* is at the *start*, or the *end*, of the query." 

There are several other keywords like **startend** which will be covered shortly. The **=>** symbol is there to separate the trigger words from the keywords (for readability).

## Define the API Call

On the next line enter:

```perl
spice to => 'http://registry.npmjs.org/$1/latest';
```

The **spice to** attribute indicates the API endpoint we'll be using, which means a `GET` request will be made to this URL. The URL has a **$1** placeholder, which will eventually be replaced with whatever string our `handle` function (which we'll define shortly) returns. Generally, Spice instant answers use a search endpoint for a given API and so, we'll need to pass along our search term(s) in the API request. We do this by returning the desired search terms in the `handle` function and then the **$1** placeholder, in the `spice to` URL, will be replaced accordingly.

Using the previous example, if we wanted to search for "**uglify-js**" with the NPM API, we'd need to replace `$1` with `uglify-js` which would result in this URL: <http://registry.npmjs.org/uglify-js/latest>. If you follow that link, you'll notice the API returns a JSON object containing all the data pertaining to the "uglify-js" NPM Package.

## Indicate our Callback Function

In most cases, APIs allow for a "callback" parameter, which usually looks like this:

```perl
http://www.api.awesome.com/?q=<search_term>&callback=<function_name>
```

This parameter is used to wrap the JSON object being returned, in a JavaScript function call to the function named in the `callback` parameter. Unfortunately, the NPM API doesn't allow for this parameter to be specified, so we force this manually by using the **spice wrap\_jsonp\_callback** function. Enter this text on the next line to do this:

```perl
spice wrap_jsonp_callback => 1;
```

Now, when the JSON is returned by the API, it will be wrapped in a call to our Spice's JavaScript callback function, which we'll define later.

------

**If the API *did* support the callback parameter**, our `spice to` would look like this:

```perl
spice to => 'http://registry.npmjs.org/$1/latest?callback={{callback}}';
```

Where `{{callback}}` is another special placeholder which will be **automatically** replaced with the correct Spice callback function name.

**\*\*Note:** Not every API uses the word "callback" for their callback parameter. Some use "jsonp" (i.e.`&jsonp=myCallbackFn`), but these names are simply convention. Therefore it's best to read the documentation for the API you're using to ensure the correct callback parameter name is used.

## Define the Handle Function

Moving on, enter this on the next line:

```perl
handle remainder => sub {
```

Once triggers are specified, we define how to *handle* the query. `handle` is another keyword, similar to **triggers**.

You can *handle* different parts of the search query, but the most common is the **remainder**, which refers to the remainder of the query, after the first matched trigger word/phrase has been removed. 

For example, if the query was "**npm uglify-js**", the trigger would be *npm* and the **remainder** would be *uglify-js*.

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

Finally, all Perl packages that load correctly should [return a true value](http://stackoverflow.com/questions/5293246/why-the-1-at-the-end-of-each-perl-package) so add a `1;` on the very last line.

```perl
1;
```

And that's it! At this point you have written a functional backend for a Spice instant answer. Now, the frontend components need to written so that we can display our instant answer result on the page.

## Recap (So Far)

The instant answer system works like this at the highest level:

- First, DuckDuckGo breaks down the query (search terms) into separate words.

- Then we see if any of those words or groups of words are **triggers** for any instant answers. These **triggers** are defined by the developer when creating an instant answer. In the example we used above, the trigger word is "**npm**".

- If a Spice is triggered, we run its `handle` function.

- If the Spice's `handle` function returns a value, it is used to replace our **$1** placeholder in the **spice to** URL, and then a request is made to that URL. When the API responds with a JSON object, it is wrapped in a function call, making the JSON object the input to our JavaScript callback function.

------

# NPM Spice - Frontend (JavaScript)

As mentioned, every instant answer requires a Spice callback function. For the *NPM* instant answer, the callback function will be named `ddg_spice_npm()` and will be defined in the **npm.js** file. 

The name of the callback function is determined by the **Npm.pm** Perl module we wrote, which specifies the name of the package, `DDG::Spice::Npm`. The portion after `DDG::Spice::` is lower cased and converted from camel case to underscore separated (i.e. `DDG::Spice::CamelCase` -> `ddg_spice_camel_case`) in order to create the name of our callback function. This generated name is what the previous `{{callback}}` placeholder will be replaced with. Similarly, if we instead had to use `spice wrap_jsonp_callback`, that will also wrap the JSON returned by the API with a function call to this generated callback name.

To clarify:

```perl
{{callback}} => ddg_spice_npm

or

{ JSON_API_RESPONSE: 1, ... } => ddg_spice_npm( { JSON_API_RESPONSE: 1, ... } );
```

The final **npm.js** will look like this:

###### npm.js

```javascript
(function (env) {
    "use strict";
    env.ddg_spice_npm = function(api_result){

        if (api_result.error) {
            return Spice.failed('npm');
        }

        Spice.add({
            id: "npm",
            name: "NPM",
            data: api_result,
            meta: {
                sourceName: "npmjs.org",
                sourceUrl: 'http://npmjs.org/package/' + api_result.name
            },
            templates: {
                group: 'base',
                options:{
                    content: Spice.npm.content,
                    moreAt: true
                }
            }
        });
    };
}(this));
```

Let's go through it line-by-line:

## Invoke an Immediate Function

###### npm.js (continued)

```javascript
(function (env) {
    "use strict";
```

We begin by invoking an anonymous, immediately-executing function, which takes an object as input (i.e. the environment). This is better known as the JavaScript "[Module Pattern](http://www.addyosmani.com/resources/essentialjsdesignpatterns/book/#modulepatternjavascript)" and it ensures that any variables or functions created within our anonymous function do not affect the global scope. It also allows us to explicitly import anything from the outside environment, which we use to pass along the global scope into our `env` variable (you'll see this at the end), so we can still access and modify the global scope as needed. After creating our module, we then we turn on JavaScript's [Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode?redirectlocale=en-US&redirectslug=JavaScript%2FReference%2FFunctions_and_function_scope%2FStrict_mode) which also offers various benefits. You don't really need to understand the purpose of these first two lines to create a Spice instant answer; however, they're both necessary and must be included when defining a Spice callback function.

## Define our Callback Function

```javascript
    env.ddg_spice_npm = function (api_result) {
```

We now define our callback function, `ddg_spice_npm`, using a function expression and set it as a property of the `env` object that was passed into our anonymous function. The name we specify here ***must*** match the name of our Spice package, which we discussed above. We also specify that the callback function takes one input parameter, which we have named `api_result`. All Spice callback functions should look like this. The name for the input should **always** be called `api_result`. This is part of our naming convention and helps to standardize the JavaScript code.

## Validate our API Response

###### npm.js (continued)

```javascript
        if (api_result.error) {
            return Spice.failed('npm');
        }
```

Here we specify that if the `error` property in the API result is defined (meaning there are no results to use) we `return` a call to `Spice.failed('npm')`, which stops the execution of the function and as a result, won't display an instant answer. It's important to use `Spice.failed();` because this lets the rest of the Spice system know our Spice isn't going to display so that other relevant answers can be given an opportunity to display.

In other cases, because most APIs return an array of results, a similar check should be made to see if the results array has a `length`. This way, if no results were returned from the API we can stop and display nothing.

Moving on, the next part is very important, it defines how the Spice result should look and specifies which parts of the API result are important. This piece of code tells DuckDuckGo to show the instant answer:

## Display our Spice Result (and Specify some Details)

###### npm.js (continued)

```javascript
        Spice.add({
            id: "npm",
            name: "NPM",
            data: api_result,
            meta: {
                sourceName: "npmjs.org",
                sourceUrl: 'http://npmjs.org/package/' + api_result.name
            },
            templates: {
                group: 'base',
                options:{
                    content: Spice.npm.content,
                    moreAt: true
                }
            }
        });
```

Here we make a call to the `Spice.add()` function, which operates on an input object that we normally define inside the function call. Let's go over each of the parameters specified in the object we give to `Spice.add()`:

- `id` is the unique identifier for your Spice instant answer, as convention, we use the name of the spice, just like we do for the callback function.

- `name` is the text to be used for the Spice's AnswerBar tab.

- `data` is the object (meaning it can be an array, because they're technically objects too) that is passed along to the Handlebars template. In this case, the *context* of the NPM template will be the `api_result` object. This is very important to understand because **only the data passed along to the template is accessible to the template**. In most cases the `data` parameter should be set to `api_result` so all the data returned from the API is accessible to the template. 

- `meta:{...}` is used to provide meta-data about the instant answer. This is used for the MetaBar (which appears above the tiles when multiple results are returned) and also for the "More at" link which appears in the detail area of a single result instant answer:
    
    + `sourceName` is the name of the source for the "**More at <source>**" link that's displayed for attribution purposes.

    + `sourceUrl` is the target of the "**More at**" link. It's the page that the user will click through to and is intended to provide the user with further information related to the instant answer.

- `templates:{...}` is used to specify which template group, templates and sub-templates are to be used for displaying your Spice instant answer:
    
    + `group` is used to specify the template group that we are using. Here', we're using the built-in, **'base'** template group. Doing this lets the templating system know which default, built-in templates should be used for the tile view and detail area, when they are present.
    
    + `options:{...}` is used to specify certain things about our templates. Some templates have components which can be turned on and off and some have the ability to include a sub-template, called `content`. In our case, we're indicating the template to be used for `content` and that the `moreAt` component should be turned on.
        
        * For `content` we pass along a reference to our handlebars template, `Spice.npm.content`. The templates contained in each Spice's share directory are pre-compiled and added to the global `Spice` object whenever a Spice instant answer is triggered. In order to namespace all the templates, we use a naming hierarchy, so `Spice.npm.content` references the **content.handlebars** template located in the **zeroclickinfo-spice/share/spice/npm/** directory.
        
        * Seeing as we've provided a `sourceName` and `sourceURL`, we have the necessary information to create a "**More at**" link and so we tell the template system to enable the creation of it by setting the `moreAt` flag to `true`.

## Global Import

```javascript
    }
}(this));
```

Lastly, we close our callback function expression, as well as our module, and we "import" the global scope, via `this`, as the input to our module. This means within the module, we can access the global scope using the `env` variable defined at the very beginning.

## Define our Handlebars Template

At this point, the rendering of the Spice instant answer changes context from JavaScript to Handlebars.js. As mentioned, our `Spice.add()` call specifies our template and the **context** for the template, so now `Spice.add()` executes the template function using `data` as the input. Let's look at the NPM instant answer's Handlebars template to see how it displays the instant answer result:

###### detail.handlebars

```html
<h5>
    {{name}} ({{version}})
</h5>
<div>{{description}}</div>
<pre>$ npm install {{name}}</pre>
```

As you can see, this is a special type of HTML template where all of `api_result`'s properties (e.g., `version`, `description`) can be accessed by wrapping their respective names in double curly braces. This is possible, because we passed along the `api_result` object (containing all the JSON) to the `data` parameter, which becomes the **context** for our template.

This is what our JSON response looks like, and our template refers by name to the properties of our JSON object:

###### Sample API response from NPM

```json
{

    "name": "http-server",
    "version": "0.6.1",
    "author": {
        "name": "Nodejitsu",
        "email": "support@nodejitsu.com"
    },
    "description": "a simple zero-configuration command-line http server",
    ...
}
```

For the NPM Spice, we have created a basic HTML skeleton and filled it in with the some useful information, by indicating which variables should go where. `{{name}}`, `{{version}}` and `{{description}}` can also be thought of as placeholders, which will be replaced by their respective values in `api_result`.

**\*\*Note:** When dealing with the detail area, an `<h5>` tag is the biggest heading tag you should use.

## All Done!

And that's it, you're done! You now have a working Spice instant answer! The backend (Perl) tells DuckDuckGo when to trigger our Spice and the frontend (JavaScript & Handlebars) tells DuckDuckGo what to put on the page. Before moving on, lets do a quick recap...

## What We've Accomplished

We've created **one** file in the Spice lib directory, `lib/DDG/Spice/`, named `Npm.pm`, which defines the API to use and the triggers for our Spice and we've created **two** files in the Spice share directory, `share/spice/npm/`:

1. `npm.js` - which delegates the API's response and calls `Spice.add()`
2. `detail.handlebars` - which specifies the instant answer's HTML structure and determines which properties of the API response are placed into the HTML result

Again, the Spice instant answer system works like so:

- First, DuckDuckGo breaks down the query (search terms) into separate words.

- Then we see if any of those words or groups of words are **triggers** for any instant answers. These **triggers** are defined by the developer when creating an instant answer. In the example we used above, the trigger word is "**npm**".

- If a Spice is triggered, we run its `handle` function.

- If the Spice's `handle` function returns a value, it is used to replace our **$1** placeholder in the **spice to** URL, and then a request is made to that URL. When the API responds with a JSON object, it is wrapped in a function call, making the JSON object the input to our JavaScript callback function.

- Our JavaScript callback function takes the API result (JSON Object), and passes it along to our `Spice.add()` call which specifies, using the elements of the JSON object, which parts are to be used in creating the instant answer "More at" link and most importantly, passes along our JSON object to our Spice's Handlebars template.

- The template then defines, using HTML and variables, what the actual content for the Spice result will be

- This content is then created and rendered onto the page by the Spice system's backend.

## Next Steps

Congratulations! You have now written your first Spice instant answer. Now, let's move on to testing, so we can make sure our instant answer functions as expected!
