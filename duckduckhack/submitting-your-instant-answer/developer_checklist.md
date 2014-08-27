# Developer Checklist

Before your instant answer is ready to be submitted, please go over this checklist to make sure everything is ready and has been done correctly.

## General Questions

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

- Is it well documented? Make sure you comment your code well so that it's easier for other people to maintain.

## Goodie

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

- Can this instant answer return unsafe content (bad words, etc)
     - Did you set `is_unsafe` to true?

- Can this instant answer return an HTML response?
     - Have you guaranteed that the response does not contain unsanitized user-supplied strings (e.g., the query string) which could lead to [cross-site scripting attacks](https://www.owasp.org/index.php/Cross-site_Scripting_%28XSS%29)? [The html_enc function is an easy way to fix this.](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_helpers.md#html-encoding)

## Spice

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

- Did you write any custom css?
    - Did you namespace the css? (every instant answer has a div with id="spice_<template_name>", use that to target your styles so you don't overwrite any global styles)

- Can this instant answer return unsafe content (bad words, etc)
    - Did you set `is_unsafe` to true?

## Fathead

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

## Longtail

(Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)
