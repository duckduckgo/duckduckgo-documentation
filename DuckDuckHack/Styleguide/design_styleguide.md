#DuckDuckHack - Plugin Design Style Guide

### Important Terms
Before we begin, please take a moment to familiarize yoursel with these terms. They will be used throughout the documentation:

* **ZCI Box - Zero-Click Info Box**  
    The box above the results, which plugins fill to display their instant answer

* **SERP - Search Engine Results Page**  
    The entire DuckDuckGo results page. Including the header, ZCI Box, all result links and the side areas.

---

##Key Concepts
When designing a plugin there are a few key concepts to keep in mind:

* Continuity
* Simplicity
* Usability
* Flexibility
* Space

##Continuity
All plugins, regardless of their plugin type (Spice, Goodie, Fathead or Longtail) should maintain visual design continuty. This means that the styling and placement of the ZCI Box elements should be the same for all plugins. The following design elements should be consistant across all plugins:

### Plugin Width
The width of plugins is automatically calculated based on the users screen size and should not be modified. Individual users are able to change the width of the SERP by modifying their settings.

### Minimze Button
The minimize/maximize button should not be altered or moved.

### Borders
The Zero Click Box should maintain a `1px solid #c9c9c9` border.

### Background colors
The background color of all plugins should match the SERP background color, `#FDFDFD`. 

### Text

**Font-Family** - Plugin headers and abstracts should use the DuckDuckGo font stack: `'Helvetica Neue', 'Segoe UI', 'Nimbus Sans L', 'Liberation Sans', 'Open Sans', FreeSans, Arial, sans-serif`.

**Font-Size** - A `14px` font-size should be used for text inside the **Zero-Click Abstract**. Smaller font sizes may also be used, we recommend the use of `<small>` tags. Fonts should be no smaller than `11px`.

**Font Color** - All text should be colored black, `#000000`, unless otherwise necessary. Coloring text grey, `#808080` is also a good way to emphasize/differentiate text, however **no bolded text is allowed**. We reserve bolding to highlight exact matches in our results. Furthermore, **all links** should be colored the blue, `#1168CE`.

## Simplicity


## Usability


## Flexibility
Plugins should be able to work across **all platforms, operating systems and browsers** seamlessly. This means that care must be taken to ensure any special CSS has backwards compatibility or graceful degredation (eg. border-radius). This also means that all plugins should look and function perfectly on both mobile devices (small screens) and desktop environments (larger screens)

## Space-ibility

---

# Plugin-Type Specific Design Style Guide
##Goodies

##Spice
- Templates should not be modified.

Carousel
    -  don't change any aspects of the pagination
    -  don't change rollover
    -  don't change selected highlight


##Fathead

##Longtail