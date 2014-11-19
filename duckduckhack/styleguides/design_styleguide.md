# Instant Answer Design Style Guide

### Important Terms

Before we begin, please take a moment to familiarize yourself with these terms. They will be used throughout the documentation:

- #### Instant Answer Box

  The box above the results that contains Instant Answers

- #### SERP - Search Engine Results Page

  The entire DuckDuckGo results page. Including the header, Instant Answer Box, all result links and the sidebar areas.

---

## Style Guide Key Concepts

When designing an Instant Answer there are a few key concepts to keep in mind:

- [Continuity](#continuity)
- [Simplicity](#simplicity)
- [Flexibility](#flexibility)
- [Space](#space)
<!-- /summary -->

## Continuity

All Instant Answers, regardless of their type (Spice, Goodie, Fathead or Longtail) should maintain visual design continuity. This means that the styling and placement of the Instant Answer Box elements should be the same for all Instant Answers. The following design elements should remain consistent across all Instant Answers:

<!-- /summary -->

- #### Instant Answer Width

  The width of Instant Answers is automatically calculated based on the users screen size and should not be modified. Individual users are able to change the width of the SERP by modifying their settings.

- #### Minimize Button

  The minimize/maximize button should not be altered or moved.

- #### Borders

  The Instant Answer Box should maintain a `1px solid #c9c9c9` border.

- #### Background Colors

  The background color of every Instant Answer should match the SERP background color, `#FDFDFD`.

- #### Font-Family

  Instant answer headers and abstracts should use the DuckDuckGo font stack: `'Helvetica Neue', 'Segoe UI', 'Nimbus Sans L', 'Liberation Sans', 'Open Sans', FreeSans, Arial, sans-serif`.

- #### Font-Size

  A `14px` font-size should be used for the Instant Answer's body text. Smaller font sizes may also be used, we recommend the use of `<small>` tags. Fonts should be no smaller than `11px`.

- #### Font Color

  All text should be colored black, `#000000`, unless otherwise necessary. Coloring text grey, `#808080` is also a good way to emphasize/differentiate text. However, **no bolded text is allowed**. We reserve bolding to highlight exact matches in our results. Furthermore, **all links** should be colored blue, `#1168CE`.

- #### Rollover / Hover

  Upon hovering, all links should have `text-decoration: underline` and `cursor: pointer`.

## Simplicity

Aside from continuity, all Instant Answers should also be designed with simplicity in mind. The information an Instant Answer provides is the most important part, which means that it should be:

<!-- /summary -->

- #### Easy to Find

  Instant answers should be easy to find, which is why we keep them at the top of the page and the actual answer to the question, whether it's text, an image, a table, etc., should be easy to find within the Instant Answer Box. An Instant Answer's content should be succinct and to-the-point. Sentence form is preferred when feasible; however, large paragraphs of text should be avoided.

- #### Easy to Read

  Although most Instant Answers are textual and in sentence form, this isn't always the case. Sometime tables are needed or other visual elements such as pictures or diagrams. Regardless of the answer's format, it should be easy to read. Fonts should be legible and both colored and sized appropriately. We ask that you use our standard fonts and colours to ensure this is always the case. As well proper use of language and grammar is essential. Use of jargon or abbreviations should be avoided or explained.

- #### Easy to Understand

  Instant answers should also be easy to understand and should provide enough context for the user to understand what question is being answered. If the user can't tell what they are looking at, the answer might be disregarded or worse, misunderstood.

## Flexibility

Instant answers must be compatible with **all platforms, operating systems and browsers**. This means that care must be taken to ensure any special CSS has backwards compatibility or graceful degradation (eg. border-radius). This also means that all Instant Answers should look and function correctly on both mobile devices (small screens) and desktop environments (larger screens). For some Instant Answer types (ie. Fatheads, Longtail) this is easily achieved because they most often return text. However, for other Instant Answers (ie. Spice) which use JavaScript and CSS, this will require a little more effort on the developer's part to ensure everything works properly.

## Space

Vertical space is of utmost importance with regards to Instant Answers. The space an Instant Answer occupies is very valuable (it would otherwise be used for links!) and so it's important that developers keep this in mind when designing their Instant Answers. Only the most important information should be displayed in an Instant Answer but if a user wants to see more information, most Instant Answers include a **"More at ..."** link, which users can follow for more detailed information.

For more detailed guidelines specific to individual Instant Answers please see the Instant Answer Specific Design Style Guides:
- [Goodies](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/styleguides/goodie_styleguide.md)
- [Spice](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/styleguides/spice_styleguide.md)
- [Fathead](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/styleguides/fathead_styleguide.md)
- [Longtail](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/styleguides/longtail_styleguide.md)