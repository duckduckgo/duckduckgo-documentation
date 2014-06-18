# Instant Answer Design Style Guide

### Important Terms

Before we begin, please take a moment to familiarize yourself with these terms. They will be used throughout the documentation:

- #### Instant Answer Box
  
  The box above the results that contains instant answers

- #### SERP - Search Engine Results Page
  
  The entire DuckDuckGo results page. Including the header, Instant Answer Box, all result links and the sidebar areas.

---

## Key Concepts

When designing an instant answer there are a few key concepts to keep in mind:

- [Continuity](#continuity)
- [Simplicity](#simplicity)
- [Flexibility](#flexibility)
- [Space](#space)

## Continuity

All instant answers, regardless of their type (Spice, Goodie, Fathead or Longtail) should maintain visual design continuity. This means that the styling and placement of the Instant Answer Box elements should be the same for all instant answers. The following design elements should remain consistent across all instant answers:

- #### Instant Answer Width
  
  The width of instant answers is automatically calculated based on the users screen size and should not be modified. Individual users are able to change the width of the SERP by modifying their settings.

- #### Minimize Button
  
  The minimize/maximize button should not be altered or moved.

- #### Borders
  
  The Instant Answer Box should maintain a `1px solid #c9c9c9` border.

- #### Background Colors
  
  The background color of every instant answer should match the SERP background color, `#FDFDFD`.

- #### Font-Family
  
  Instant answer headers and abstracts should use the DuckDuckGo font stack: `'Helvetica Neue', 'Segoe UI', 'Nimbus Sans L', 'Liberation Sans', 'Open Sans', FreeSans, Arial, sans-serif`.

- #### Font-Size
  
  A `14px` font-size should be used for the instant answer's body text. Smaller font sizes may also be used, we recommend the use of `<small>` tags. Fonts should be no smaller than `11px`.

- #### Font Color
  
  All text should be colored black, `#000000`, unless otherwise necessary. Coloring text grey, `#808080` is also a good way to emphasize/differentiate text. However, **no bolded text is allowed**. We reserve bolding to highlight exact matches in our results. Furthermore, **all links** should be colored blue, `#1168CE`.

- #### Rollover / Hover
  
  Upon hovering, all links should have `text-decoration: underline` and `cursor: pointer`.

## Simplicity

Aside from continuity, all instant answers should also be designed with simplicity in mind. The information an instant answer provides is the most important part, which means that it should be:

- #### Easy to Find
  
  Instant answers should be easy to find, which is why we keep them at the top of the page and the actual answer to the question, whether it's text, an image, a table, etc., should be easy to find within the Instant Answer Box. An instant answer's content should be succinct and to-the-point. Sentence form is preferred when feasible; however, large paragraphs of text should be avoided.

- #### Easy to Read
  
  Although most instant answers are textual and in sentence form, this isn't always the case. Sometime tables are needed or other visual elements such as pictures or diagrams. Regardless of the answer's format, it should be easy to read. Fonts should be legible and both colored and sized appropriately. We ask that you use our standard fonts and colours to ensure this is always the case. As well proper use of language and grammar is essential. Use of jargon or abbreviations should be avoided or explained.

- #### Easy to Understand
  
  Instant answers should also be easy to understand and should provide enough context for the user to understand what question is being answered. If the user can't tell what they are looking at, the answer might be disregarded or worse, misunderstood.

## Flexibility

Instant answers must be compatible with **all platforms, operating systems and browsers**. This means that care must be taken to ensure any special CSS has backwards compatibility or graceful degradation (eg. border-radius). This also means that all instant answers should look and function correctly on both mobile devices (small screens) and desktop environments (larger screens). For some instant answer types (ie. Fatheads, Longtail) this is easily achieved because they most often return text. However, for other instant answers (ie. Spice) which use JavaScript and CSS, this will require a little more effort on the developer's part to ensure everything works properly.

## Space

Vertical space is of utmost importance with regards to instant answers. The space an instant answer occupies is very valuable (it would otherwise be used for links!) and so it's important that developers keep this in mind when designing their instant answers. Only the most important information should be displayed in an instant answer but if a user wants to see more information, most instant answers include a **"More at ..."** link, which users can follow for more detailed information.

For more detailed guidelines specific to individual instant answers please see the [instant answer Specific Design Style Guide](https://github.com/duckduckgo/DuckDuckGo-Documentation/tree/master/DuckDuckHack/Styleguide/instant answer-Specific-Design-Style-Guide)
