# Developer Checklist

Before submitting your Instant Answer, please go over this checklist to make sure everything is ready and has been done correctly.

## General Questions

- Did you write any custom CSS?
    - Did you namespace the CSS? Every Instant Answer should be contained in a `<div>` with a unique id. This id should be used to target your styles and avoid overwriting any global styles.

## Goodie

- Can this Instant Answer return unsafe content (bad words, etc.)
    - Did you set `is_unsafe` to true?

- Can this Instant Answer return an HTML response?
    - Have you guaranteed that the response does not contain unsanitized user-supplied strings (e.g., the query string) which could lead to [cross-site scripting attacks](https://duckduckgo.com/Cross-site_scripting?ia=about)?

## Spice

- Can this Instant Answer return unsafe content (bad words, etc.)
    - Did you set `is_unsafe` to true?
