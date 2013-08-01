# DuckDuckHack - Plugin Design Style Guide

### Important Terms
Before we begin, please take a moment to familiarize yourself with these terms. They will be used throughout the documentation:

* **ZCI Box - Zero-Click Info Box**  
    The box above the results, which plugins fill to display their instant answer

* **SERP - Search Engine Results Page**  
    The entire DuckDuckGo results page. Including the header, ZCI Box, all result links and the side areas.

---

## Key Concepts
When designing a plugin there are a few key concepts to keep in mind:

* Continuity
* Simplicity
* Flexibility
* Space

## Continuity
All plugins, regardless of their plugin type (Spice, Goodie, Fathead or Longtail) should maintain visual design continuty. This means that the styling and placement of the ZCI Box elements should be the same for all plugins. The following design elements should remain consistant across all plugins:

### Plugin Width
The width of plugins is automatically calculated based on the users screen size and should not be modified. Individual users are able to change the width of the SERP by modifying their settings.

### Minimze Button
The minimize/maximize button should not be altered or moved.

### Borders
The Zero Click Box should maintain a `1px solid #c9c9c9` border.

### Background Colors
The background color of every plugin should match the SERP background color, `#FDFDFD`.

### Typography

#### Font-Family
Plugin headers and abstracts should use the DuckDuckGo font stack: `'Helvetica Neue', 'Segoe UI', 'Nimbus Sans L', 'Liberation Sans', 'Open Sans', FreeSans, Arial, sans-serif`.

#### Font-Size
A `14px` font-size should be used for text inside the **Zero-Click Abstract**. Smaller font sizes may also be used, we recommend the use of `<small>` tags. Fonts should be no smaller than `11px`.

#### Font Color
All text should be colored black, `#000000`, unless otherwise necessary. Coloring text grey, `#808080` is also a good way to emphasize/differentiate text, however **no bolded text is allowed**. We reserve bolding to highlight exact matches in our results. Furthermore, **all links** should be colored the blue, `#1168CE`.

### Rollover / Hover
Upon hovering, all links should have `text-decoration: underline` and `cursor: pointer`.

## Simplicity
Aside from continutity all plugins should also be designed with simplicity in mind. The purpose of a Zero-Click Info plugin is to give the user an instant answer without them clicking even once. The information a plugin provides is therefore the most important part, which also means that a plugin's answer should be:
* easy to find
* easy to read
* and easy to understand

### Easy to Find
The answer a plugin provides should be easy to find within the ZCI Box. The answer should be succint and to-the-point. Large paragraphs of text should be avoided.

### Easy to Read
Although most plugins provide textual answers in sentence form, this isn't always the case. Sometime tables are needed or other visual elements such as pictures or digrams. Regardless of the answer's format, it should be easy to read (eg. not too small, not too bright, easy to read fonts)

### Easy to Understand
Plugin answers should also be easy to understand and should provide enough context for the user to understand what question is being answered. If the user can't tell what they are looking at, the answer might be disregarded or worse, misunderstood.

## Flexibility
Plugins must be compatible across **all platforms, operating systems and browsers**. This means that care must be taken to ensure any special CSS has backwards compatibility or graceful degredation (eg. border-radius). This also means that all plugins should look and function correctly on both mobile devices (small screens) and desktop environments (larger screens). For some plugin types (ie. Fatheads, Longtail) this is easily achieved because they simply return text. However, for other plugins (ie. Spice) which use JavaScript and CSS, this will require a little more effort on the developer's part to ensure everything works properly.

## Space
Vertical space is of utmost importance with regards to instant answers. The space a plugin occupies is very valuable (it would otherwise be used for links!) and so it's important that developers keep this in mind when designing their plugins. Only the most important information should be displayed in an instant answer. If a user wants to see more information, most plugins includes at "More at ..." link, which they can follow for more detailed information.

---

# Plugin-Type Specific Design Style Guide

## Goodies
(tbd)

## Spice
(tbd)
- Templates should not be modified.

Carousel
    -  don't change any aspects of the pagination
    -  don't change rollover
    -  don't change selected highlight


## Fathead
(tbd)

## Longtail
(tbd)
