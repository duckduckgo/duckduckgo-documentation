# What's New in the DuckDuckHack Platform

**May 2014**

The new version of DuckDuckGo has launched into public beta!  This document highlights changes to the Instant Answer platform.


## Highlights

- AnswerBar: many Instant Answers can display on the page at once
- Wider: Instant Answers can fill the width of the page in certain cases
- New views for Instant Answers: Tile view with grid mode, Interactive maps, Image view
- New templates and layouts: Text, Info, Products with variations and feature flags
- Automated api result relevancy checking and data sorting

Most of the changes to instant answers apply only to the [Spice][Spice] instant answer type (external API),but these abilities will be brought soon to the [Goodies][Goodies] type.


## AnswerBar

The AnswerBar display instant answers in tabs. Because many IAs can load together, they need to play well together now. For example, they can't arbitrarily name CSS or helper functions arbitrary names as there is a chance of conflict.

![AnswerBar](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/coffee.png)

In this example:

- About: Wikipedia or [Fathead][Fathead] result
- Images and Video results
- Meanings: disambiguation (*meanings of 'coffee'*)
- Recipes: a Spice Instant Answer
- Dictionary Definition: a Spice Instant Answer
- Products: a Spice instant answer

DuckDuckGo's internal processes determined the About, Images, Video, and Meanings results.

The others, Spice Instant Answers, individually define a query space with their [triggers][triggers]. In the above example, Recipes, Dictionary and Products have already received data from their respective external APIs and have determined that the data is actually relevant to the user's query.


## Answers

Instant answers are of two fundamental types: single- and multi-item. Below is a single item, the dictionary definition Spice instant answer:

![Single item, detail view](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/coffee_definition.png)

This is a single item displayed using the detail template defined by the instant answer.


## Tile View

When an Instant Answer has multiple items, they are generally shown in the Tile View. It's very flexible, supports different tile size variations, grid mode, and provides a detail view for each individual item.

![Multiple items in a Tile View](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/coffee_recipes.png)

Each *tile* is a container that displays an item, which is rendered with a template as defined by the instant answer. The term *item* refers to the single unit of data as defined by the IA - in these examples, a definition or single recipe is an item.

The item can also be shown with its detail template:

![Tile View with Detail](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/coffee_recipes_detail.png)



## Templates and Layouts

Instant Answers (Spice only, for now) provide templates to allow the AnswerBar to display their data in different contexts - as tiles, or as detail, or both. DuckDuckHack provides several built-in types to cover common general cases, with the ability to make substitutions and turn features on and off as desired.

Templates can be named individually, and they have been organized into named groups for convenience, with default feature options set appropriately. For instance, `products_simple` is just `products` with the brand and price turned off; an individual IA could further turn off the rating, or other items to reuse the basic structure. See the InTheaters example below.

Template groups:

- base: empty container
- text: title and description
- icon: text with small inset image
- info: structured expandable text with auxiliary box
- products: product information with icons, rating, price
- products_simple: less structured variation of products

### Text template group

Tiles support title, subtitle, and content and footer sub templates which the IA can provide.

![github using text group, showing tiles](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/github_duckduckgo.png)

[github](https://github.com/duckduckgo/zeroclickinfo-spice/tree/bttf/share/spice/github) using the text template group with a custom footer


![dictionary definition using text group, showing detail](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/coffee_definition.png)

------

[dictionary definition](https://github.com/duckduckgo/zeroclickinfo-spice/tree/bttf/share/spice/dictionary/definition) uses a custom template for the title in detail view.

### Products

The products template group consists of templates for tiles and detail that are structured for items to buy. Rating, brand, price, etc. There is a second group called `products_simple` which is similar but with the price and brand turned off by default, and a slightly simpler tile structure.

![amazon using the products group](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/products_detail.png)

------

![Tile comparison: variations of 'products'](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/tile_comparison.png)

Recipes, on the left, is using the products_simple tile, and amazon on the right is using the products tile.

InTheaters uses the products_simple template group, but simplifies the tile even more by turning off all the tile's features except the image. Additionally it sets the tile to use the 'poster' variant, shaped like a movie poster.

![in_theaters using the products_simple template group](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/movies.png)

[InTheaters](https://github.com/duckduckgo/zeroclickinfo-spice/tree/bttf/share/spice/in_theaters) substitutes a custom template for the rating line in the products detail template (to conform to the Rotten Tomatoes way of rating things) and provides its own "buy" template for the button "Reviews and Showtimes". In the tiles it turns off the title, rating and ratingText so the image occupies the entirety of the tile.


### Info

Info is a sophisticated template for showing summary information with an optional image and embedded auxiliary box. Both the text and auxiliary box are expandable, by default showing four lines of text in height. Both the text and the auxiliary box can contain arbitrary content by using an IA-defined template.

![Last.fm using the info template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/artist.png)

The info template also supports an embedded auxiliary box on the right.
There's an [open issue for Last.fm](https://github.com/duckduckgo/zeroclickinfo-spice/issues/684) to display the artist's top tracks in the auxiliary box.

![Info template with embedded auxiliary box, no image](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/drinks-infobox.png)

Here [Drinks](https://github.com/duckduckgo/zeroclickinfo-spice/tree/bttf/share/spice/drinks) uses the auxiliary box for its ingredients list. By default the info template only shows the part of the box that fits within the default template height. Here it's shown in the open state.

Because Drinks doesn't have an image, it's not shown and the text is aligned left to fill the space. Since the text already fits within four lines, no "Show More" expander button is displayed.


## Data Mapping with normalize()

Because APIs define their data in their own ways, instant answers that use built-in templates must provide a `normalize()` function that maps data to the field names required by a built-in template. For example, the Yummly API used by Recipes returns an array of images called `imageUrlsBySize`, so Recipes sets `image` required by the products template group with one of these.


[Spice]: https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_overview.md
[Goodies]: https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_overview.md
[Fathead]: https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/fathead/fathead_overview.md
[triggers]:https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/spice_triggers.md