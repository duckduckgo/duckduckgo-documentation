### Note

This documentation is for the DuckDuckGo [public beta](https://next.duckduckgo.com/). The API has changed in some significant ways.
See [getting started](https://github.com/duckduckgo/zeroclickinfo-spice/blob/bttf/BETA.md) for more information and how to help out during the transition.

<hr>

# Spice Overview

Spice instant answers are triggered by a backend Perl component that then calls the JSON API of an upstream service. The API response is wrapped in a JavaScript function call. You, the instant answer author, define this callback function and handle the API's response on the client side, generating the display from the data returned by the API.

## Spice Frontend

The Spice frontend is the code that is triggered by the Perl backend for your spice instant answer. It mainly consists of a function (the Spice "callback" function) that takes a JSON formatted, API response as its input and uses the data to display a Spice result at the top of the DuckDuckGo search results page.

### Spice Templates

In order to display the result, the Spice callback function needs to specify a template, which will determine how the result looks. There are several built-in templates to choose from and you are able to choose whichever template works best for the given data and desired output.

### Third-Party Libraries

Aside from HTML and CSS, the Spice frontend also utilizes the following third-party libraries:

- [jQuery](https://jquery.org) v1.10.2
- and [Handlebars](http://handlebarsjs.com) v1.3.0

If you're not already familiar with Handlebars, *please* read the [Handlebars documentationn](http://handlebarsjs.com) before continuing on. Don't worry if you don't fully understand how to use Handlebars, the examples will explain everything. You should, at the very least, familiarize yourself with Handlebars concepts and terminology before moving on. It should only take a few minutes to read!

Likewise, using jQuery is not required for making a Spice instant answer, however it does offer certain benefits, such as cross-browser compatible implementations of various JavaScript functions. For example, jQuery's `$.each()` should be used in place of the native `Array.prototype.forEach()`, as it does **not** work in IE 6,7,8.

Later, we will walk you through several examples, ranging from simple to complex, which will explain how to use templates and make your instant answers look awesome :)

## Spice Files

A typical Spice instant answer requires several files to function properly.
- The Perl files go in the **lib** directory: `lib/DDG/Spice/InstantAnswerName.pm`
- The frontend files (JS, Handlebars, CSS) discussed later go in the **share** directory: `share/spice/instant_answer_name/`

**\*\*Note** : The file and folder names must adhere to our naming conventions (covered later) in order for everything to function properly.
