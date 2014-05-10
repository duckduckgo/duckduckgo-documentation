# What's New in the DuckDuckHack Platform

**May 2014**

The new verison of DuckDuckGo has launched into public beta!  This document highlights changes to the Instant Answer platform.

## Highlights

- AnswerBar: many Instant Answers can display on the page at once
- Wider: Instant Answers can fill the width of the page in certain cases
- New views for Instant Answers: Tile view with grid mode, Interactive maps, Image view
- New templates and layouts: Text, Info, Products with variations and feature flags
- Automated api result relevancy checking and data sorting

## AnswerBar

The AnswerBar display instant answers in tabs. Because many IAs can load together, they need to play well together now. For example, they can't arbitrarily name CSS or helper functions arbitrary names as there is a chance of conflict.


![AnswerBar](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/coffee.png)

In this example we see:

- About (Wikipedia result)
- Images and Video results
- Meanings (Disambiguation)
- Recipes Instant Answer (Spice)
- Dictionary Definition answer (Spice)
- Products instant answer

## Tile View

Instant answers are of two fundamental types: single- and multi-item. below is a single item, the dictionary definition:

![Single item](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/coffee_definition.png)

And here is a multi-item instant answer


![multi-item Tile View](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/coffee_recipes.png)

These are multiple items displayed as tiles in the Tile View. The term 'item' refers to the data; here it is being displayed in a Tile, using the 'products' layout. Below is one selected item shown in more detail

![Tile View with Detail](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/coffee_recipes_detail.png)

## Templates and Layouts


## Anatomy of an IA



