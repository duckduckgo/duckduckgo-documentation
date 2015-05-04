## Spice Overview  

**If you have questions about Spice, ask our [Spice Chat room](https://gitter.im/duckduckgo/zeroclickinfo-spice)**    

Spice Instant Answers are triggered by a backend Perl component that then calls the JSON API of an upstream service. The API response is wrapped in a JavaScript function call. You, the Instant Answer author, define this callback function and handle the API's response on the client side, generating the display from the data returned by the API.

## Important Spice Criteria

- APIs called by Spice Instant Answers **must use the JSON or JSONP formats**. We do not support the use of XML (it's coming soon though!), HTML, or plain text responses.
- APIs used should be **reliable**. Pick sources that will be most likely be around and accurate for the foreseeable future.
- APIs used should represent the **most credible source** for the information. This means it should draw upon the preferred data source of the relevant community.
- APIs should respond to requests in **less than one second** (< 1s).

If you're not sure about whether the API you'd like to use fits these criteria, we're happy to help figure it out. Email us over at [open@duckduckgo.com](mailto:open@duckduckgo.com).

## Spice Frontend

The Spice frontend is the code that is triggered by the Perl backend for your spice Instant Answer. It mainly consists of a function (the Spice "callback" function) that takes a JSON formatted, API response as its input and uses the data to display a Spice result at the top of the DuckDuckGo search results page.

## Spice Templates

In order to display the result, the Spice callback function needs to specify a template, which will determine how the result looks. There are several built-in templates to choose from and you are able to choose whichever template works best for the given data and desired output.

## Third-Party Libraries

Aside from HTML and CSS, the Spice frontend also utilizes the following third-party libraries:

- [jQuery](https://jquery.org) v1.10.2
- and [Handlebars](http://handlebarsjs.com) v1.3.0

If you're not already familiar with Handlebars, *please* read the [Handlebars documentationn](http://handlebarsjs.com) before continuing on. Don't worry if you don't fully understand how to use Handlebars, the examples will explain everything. You should, at the very least, familiarize yourself with Handlebars concepts and terminology before moving on. It should only take a few minutes to read!

<!-- /summary -->

Likewise, using jQuery is not required for making a Spice Instant Answer. But, it does offer certain benefits, such as cross-browser compatible implementations of various JavaScript functions. For example, jQuery's `$.each()` should be used in place of the native `Array.prototype.forEach()`, as it does **not** work in IE 6,7,8.

Later, we will walk you through several examples, ranging from simple to complex, which will explain how to use templates and make your Instant Answers look awesome :)

## Spice Files

A typical Spice Instant Answer requires several files to function properly.
- The Perl files go in the **lib** directory: `lib/DDG/Spice/InstantAnswerName.pm`
- The frontend files (JS, Handlebars, CSS) discussed later go in the **share** directory: `share/spice/instant_answer_name/`

**\*\*Note** : The file and folder names must adhere to our naming conventions (covered later) in order for everything to function properly.
