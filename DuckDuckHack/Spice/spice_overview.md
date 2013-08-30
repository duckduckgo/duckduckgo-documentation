# Spice Overview

Spice instant answers are triggered by a backend Perl component that then calls the JSON API of an upstream service. The API response is wrapped in a JavaScript function call. You, the instant answer author, define this callback function and handle the API's response on the client side, generating the display from the data returned by the API.

## Spice Frontend
The Spice frontend is the code that is triggered by the Perl backend for your spice instant answer. It mainly consists of a function (the Spice "callback" function) that takes a JSON formatted, API response as its input, specifies which template format you'd like your result to have and uses the data to render a Spice result at the top of the DuckDuckGo search results page.

The Perl part of the instant answers go in lib directory: `lib/DDG/Spice/instant answerName.pm`, while all of the frontend files discussed below should go in the share directory: `share/spice/instant answer_name/`.

**\*\*Note** : The file and folder names must adhere to our [naming conventions](#) in order for everything to function properly.

### Tech
The Spice frontend uses [Handlebars](http://handlebarsjs.com) for templates and includes [jQuery](https://jquery.org) (although it's use is not required). It also allows the use of custom CSS when required.

If you're not already familiar with Handlebars, *please* read the [Handlebars documentation](http://handlebarsjs.com) before continuing on. Don't worry if you don't fully understand how to use Handlebars; the examples will explain it to you. But you should, at the very least, familiarize yourself with Handlebars concepts and terminology before moving on. (Don't worry, it should only take a few minutes to read!)

Below, we will walk you through several examples ranging from simple to complicated, which will explain how to use the template system and make your instant answers look awesome.

