# Spice Templates Reference

The basic building blocks of displaying Spice Instant Answers are the templates and variants. Below is a detailed reference of each template and its workings.

The reference is divided into two parts:

- [Spice Templates](#spice-templates)
- [Tile Variants](#tile-variants)

## Spice Templates

The list of built-in Spice templates includes:

- [`record`](#record-template)
- [`text_item`](#textitem-template)
- [`text_detail`](#textdetail-template)
- [`basic_image_item`](#basicimageitem-template)
- [`products_item`](#productsitem-template)
- [`products_detail`](#productsdetail-template)
- [`products_item_detail`](#productsitemdetail-template)
- [`basic_info_detail`](#basicinfodetail-template)
- [`places_item`](#placesitem-template)
- [`places_detail`](#placesdetail-template)
- [`list_detail`](#listdetail-template)
- [`base_item`](#baseitem-template)
- [`base_detail`](#basedetail-template)

------

<!-- /summary -->

## `record` Template

A special template that is ideal for key-value data. It generates a `<table>` where each row contains a key and value.

**Note:** This template **requires** that your `data` object has a `record_data` property, which should contain the key-value data to be displayed. All the properties of the `record_data` object will be used as the keys for the table. However, if you want to specify exactly which properties of the `record_data` object should be displayed, an optional `record_keys` property can be defined. It should be an array of *strings*, indicating the names of the **keys** to be included in the `<table>`.  An optional property called `rowHighlight` can be added to `options` to turn on alternating row highlighting.

<!-- /summary -->

For example this is how your Spice code should look when using the **record** template:

```javascript
data: {
    record_data: {
        name: 'Bob',
        phone: '123-456-7890',
        email: 'bob@bobstheman.com',
        address: '123 First Street'
    }
},
normalize: function(item){
    return {
        record_keys: ["name", "phone", "email"]
    }
},
templates: {
    group: 'base',
    options: {
        content: 'record',
        /* optional - highlight alternate rows */
        rowHighlight: true
    }
}
```

### Available Features

- `record_data` *object* (contains key-value pairs to display in table format)

### Template Diagram

![record template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Frecord.png&f=1)

### Template groups using the "record" template:

- Can be used as a sub-template by the [List](https://duck.co/duckduckhack/spice_templates_overview#list-template-group) template group (under the [`list_detail`](#listdetail-template) template)

### Example usage of the "record" template:

- [UrbanDictionary](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/urban_dictionary/urban_dictionary.js)
- [MetaCpan](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js)
- [CodeSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/code_search/code_search.js)
- [Whois](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js)

------

## `text_item` Template

### Available Features

- `icon` [optional] *url path to icon*
- `url` [optional]
- `title`
- `altSubtitle` [optional]
- `subtitle` [optional]
- `description`
- `footer` [optional] *sub-template*

### Template Diagram

![text_item template ](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Ftext_item.png&f=1)

```
+------------------+
icon
title, altSubtitle
subtitle
description
footer
+------------------+
```

### Template groups using the "text_item" template:

- [Text](https://duck.co/duckduckhack/spice_templates_overview#text-template-group)

### Example usage of the "text_item" template:

- [GitHub](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js)
- [RubyGems](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/ruby_gems/ruby_gems.js)
- [RedditSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js)
- [AlternativeTo](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js)

------

## `text_detail` Template

### Available Features

- `title_content` [optional] *sub-template*
- `title` [optional] (available only if `title_content` is not specified)
- `subtitle_content` [optional] *sub-template*
- `subtitle` [optional] (available only if `subtitle_content` is not specified)
- `content` [optional] *sub-template*

### Template Diagram

![text_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Ftext_detail.png&f=1)

```
+------------------+
title_content or title
subtitle_content or subtitle
content
+------------------+
```

### Template groups using the "text_detail" template:

- [Text](https://duck.co/duckduckhack/spice_templates_overview#text-template-group)

### Example usage of the "text_detail" template:

- [Rhymes](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js)
- [Thesaurus](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/thesaurus/thesaurus.js)

------

## `basic_image_item` Template

### Available Features

- `url` [optional]
- `image` *url path to image*
- `title`
- `description` [optional]
- `rating` [optional]
- `ratingText` [optional]

### Template Diagram

![basic_image_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_image_item.png&f=1)

### Template groups using the "basic_image_item" template:

- [Info](https://duck.co/duckduckhack/spice_templates_overview#info-template-group)
- [Media](https://duck.co/duckduckhack/spice_templates_overview#media-template-group)

### Example usage of the "basic_image_item" template:

- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)
- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)

------

## `products_item` Template

### Available Features

- `url` [optional]
- `img` *url path to image*
- `title`
- `price` [optional]
- `brand` [optional]
- `rating` [optional]
- `reviewCount` [optional]
- `url_review` [optional] *url path to reviews*

### Template Diagram

![products_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_item.png&f=1)

```
+------------------+
img
title
price
brand
rating
+------------------+
```

### Template groups using the "products_item" template:

- [Products](https://duck.co/duckduckhack/spice_templates_overview#products-template-group)

### Example usage of the "products_item" template:

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

------

## `products_detail` Template

### Available Features

- `img` [optional] *url path to image*
- `url` 
- `heading`
- `rating` [optional]
- `reviewCount` [optional]
- `price` [optional]
- `brand` [optional]
- `subtitle_content` [optional] *sub-template*
- `abstract`
- `buy` [optional] *sub-template*

### Template Diagram

![products_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_detail.png&f=1)

```
+------------------+
img
heading
rating
price
brand
subtitle_content
abstract
buy
+------------------+
```

### Template groups using the "products_detail" template:

- [Products](https://duck.co/duckduckhack/spice_templates_overview#products-template-group)
- [Media](https://duck.co/duckduckhack/spice_templates_overview#media-template-group)
- [Icon](https://duck.co/duckduckhack/spice_templates_overview#icon-template-group)

### Example usage of the "products_detail" template:

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

------

## `products_item_detail` Template

### Available Features

- `img_m` [optional]
- `url`
- `price` [optional]
- `brand` [optional]
- `subtitle_content` [optional] *sub-template*
- `rating` [optional]
- `reviewCount` [optional]
- `url_review` [optional] *url path to reviews*
- `abstract`
- `buy` [optional] *sub-template*

### Template Diagram

![products_item_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_item_detail.png&f=1)

### Template groups using the "products_item_detail" template:

- [Products](https://duck.co/duckduckhack/spice_templates_overview#products-template-group)
- [Media](https://duck.co/duckduckhack/spice_templates_overview#media-template-group)
- [Icon](https://duck.co/duckduckhack/spice_templates_overview#icon-template-group)

### Example usage of the "products_item_detail" template:

- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)
- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)

------

## `basic_info_detail` Template

### Available Features

- `url`
- `image` [optional] *url path to image*
- `title` [optional]
- `subtitle` [optional] (available only if `title` specified)
- `content` [optional] *sub-template*
- `description` (available and required only if `content` sub-template not specified)
- `aux` [optional] *sub-template*
- `auxTitle` (available and required only if `aux` specified)

### Template Diagram

![basic_info_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_info_detail.png&f=1)

```
+-----------------------------------------+
image
title
subtitle						auxTitle
content or description			aux
+-----------------------------------------+
```

### Example with Auxiliary Information Box:

![basic_info_detail_w_aux template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_info_detail_w_aux.png&f=1)

### Template groups using the "basic_info_detail" template:

- [Info](https://duck.co/duckduckhack/spice_templates_overview#info-template-group)

### Example usage of the "basic_info_detail" template:

- [Bitcoin](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js)
- [Gravatar](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js)
- [Drinks](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/drinks/drinks.js)

------

## `places_item` Template

The places item template is a slick way to display multiple location results on one map. Originally created for DuckDuckGo's built-in [local results](https://duckduckgo.com/?q=cafes+in+new+york), it's now available to instant answers as well.

Clicking a places item both indicates its location on a map, as well as 'flips' the item to display more detailed information. The `places_item` template can conceptually be divided into its 'front' and 'back'.

### Available Features

'Front' of each item:
- `image` [optional] *url path to image*
- `name`
- `title` (available only if `image` specified)
- `ratingImageURL` [optional]
- `rating` [optional] (available only if `ratingImageURL` not specified)
- `reviews` [optional]

'Back' of each item: (displayed upon click)
- `name`
- `url`
- `price` [optional]
- `address_lines` [optional]
- `address` [optional] (available only if `address_lines` not specified)
- `phone` [optional]

### Template Diagram

#### 'Front'

![DuckDuckGo search for "cafes near ann arbor"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flocal_results_front.png&f=1)
```
+--------------------+


		image


+--------------------+
name
ratingImageURL *or* rating
reviews
+--------------------+
```

#### 'Back'

This view is displayed when the 'front' is clicked, together with the map (below).

![DuckDuckGo search for "cafes near ann arbor"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flocal_results_back.png&f=1)

```
+--------------------+

name (url)

price

address_lines *or* address

phone

+--------------------+
```

#### Map View

This view is displayed when the 'front' is clicked, together with the 'back' (above).

![DuckDuckGo search for "cafes near ann arbor"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flocal_results_map.png&f=1)


### Template groups using the "places_item" template:

- [Places](https://duck.co/duckduckhack/spice_templates_overview#places-template-group)

### Example usage of the "places_item" template:

- [Parking Panda](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/parking/parking.js): search for [parking in new york](https://duckduckgo.com/?q=parking+in+new+york).
- Local results (built-in to DDG): search for [cafes near Ann Arbor](https://duckduckgo.com/?q=cafes+near+ann+arbor).

------

## `places_detail` Template

The places detail template nicely displays information about a single location with a map backdrop. Originally created for DuckDuckGo's built-in [local results](https://duckduckgo.com/?q=espresso+italiano+maui), it's now available to be used in instant answers.

### Available Features

- `url`
- `name`
- `image` [optional] *url path to image*
- `title` (required if using `image`)
- `hours` [optional] *array of objects* (each object specifies `day` and `hours` properties)
- `ratingImageURL` [optional]
- `rating` [optional] (available only if `ratingImageURL` not specified)
- `reviews` [optional]
- `price` [optional]
- `address_lines` [optional]
- `address` [optional] (available only if `address_lines` not specified)
- `phone` [optional]

### Template Diagram

![DuckDuckGo search for "espresso italiano maui"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flocal_results_detail.png&f=1)

```
+--------------------------------+------------+
|   name (url)                   |            |
|                                | image (url)|
|   ratingImageURL *or* rating   |            |
|   reviews                      |            |
|   price                        |            |
|   address_lines *or* address   |            |
|   phone                        |            |
|                                |            |
|                                |            |
+--------------------------------+            |
|                                |            |
|    hours                       |            |
|                                |            |
+--------------------------------+------------+
```


### Template groups using the "places_detail" template:

- [Places](https://duck.co/duckduckhack/spice_templates_overview#places-template-group)

### Example usage of the "places_detail" template:

- Local results (built-in to DDG): search for [a particular business](https://duckduckgo.com/?q=espresso+italiano+maui).

------

## `list_detail` Template

This template allows display of a title and subtitle above a bulleted list *or* a table of key-value pairs. 

To display a bulleted list, pass a sub-template to the `list_content` property. To display a table of key-value pairs, pass the [`record`](#record-template) template to the `content` property.

### Available Features

- `title` [optional]
- `subtitle` [optional]

#### If Displaying Table of Key-Value Pairs:

- `content` *sub-template* (set this value to 'record' to use the built-in [`record`](#record-template) template)
- `record_data` *object containing the key-value pairs to display*

#### If Displaying Bulleted List of Values:

- `list_content` *sub-template* (populates within each `li` element)
- `list` *array of objects* (each object contains the properties used by `list_content` sub-template)

**Note:** The simplest way to display a bulleted list of values would be to pass `list` an array of objects like `{value: 'foo'}` and specify `list_content` to be a sub-template which only reads `{{value}}`.

### Template Diagram

![DuckDuckGo search for "whois mozilla.org"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhois_results.png&f=1)

```
+-------------------+

title
subtitle
record_data *or* list

+-------------------+
```

### Template groups using the "list_detail" template:

- [List](https://duck.co/duckduckhack/spice_templates_overview#list-template-group)

### Example usage of the "list_detail" template:

- [Whois](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js) (search for ['whois mozilla.org'](https://duckduckgo.com/?q=whois+mozilla.org))


------

## `base_item` Template

### Available Features

- `url` [optional]
- `content` *sub-template*

### Template Diagram

![base_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_item.png&f=1)

<!-- /summary -->

### Complex Example

![base_item template (complex example)](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_item_complex.png&f=1)

### Template groups using the "base_item" template:

- [Base](https://duck.co/duckduckhack/spice_templates_overview#base-template-group)

### Example usage of the "base_item" template:

- [GithubJobs](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github_jobs/github_jobs.js)
- [Airlines](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/airlines/airlines.js)

------

## `base_detail` Template

### Available Features

- `content` *string* or *sub-template*

### Template Diagram

![base_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_detail.png&f=1)

<!-- /summary -->

### Complex Example

![base_detail template (complex example)](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_detail_complex.png&f=1)

### Template groups using the "base_detail" template:

- [Base](https://duck.co/duckduckhack/spice_templates_overview#base-template-group)

### Example usage of the "base_detail" template:

- [FlashVersion](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/flash_version/flash_version.js)
- [NPM](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/npm/npm.js)
- [XKCD](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/xkcd/xkcd.js)

------

## Tile Variants

If the default tile dimensions are not perfect for your Spice result, you can choose from one of the following tile variants, each of which offer different dimensions (some wider, some taller):

- [poster](#poster-variant)
- [narrow](#narrow-variant)
- [wide](#wide-variant)
- [xwide](#xwide-variant)
- [video](#video-variant)

------

## `poster` Tile Variant

Tall and thin, like a movie poster.

### Usage

```javascript
templates: {
    ...
    options: {
        ...
        variant: 'poster'
    }
}
```

<!-- /summary -->

### Examples

- ["the dark knight movie"](https://duckduckgo.com/?q=the+dark+knight+movie)
- ["currently in theaters"](https://duckduckgo.com/?q=currently+in+theaters)

------

## `narrow` Tile Variant

Narrower tile width, normal height.

### Usage

```javascript
templates: {
    ...
    options: {
        ...
        variant: 'narrow'
    }
}
```

<!-- /summary -->

### Examples

- ["alarm clock apps"](https://duckduckgo.com/?q=alarm+clock+apps)
- ["pa representatives"](https://duckduckgo.com/?q=pa+representatives)

------

## `wide` Tile Variant

Increased width, normal height.

### Usage

```javascript
templates: {
    ...
    options: {
        ...
        variant: 'wide'
    }
}
```

<!-- /summary -->

### Examples

none...*yet!*

------

## `xwide` Tile Variant

Super wide, normal height.

### Usage

```javascript
templates: {
    ...
    options: {
        ...
        variant: 'xwide'
    }
}
```

### Examples

- ["flight aa102"](https://duckduckgo.com/?q=flight+aa102)

------

## `video` Variant

Shorter height, increased width.

### Usage

```javascript
templates: {
    ...
    options: {
        ...
        variant: 'video'
    }
}
```

### Examples

none...*yet!*

<!--

TODO: Unhide this once live

------

# Detail Variants

## `light` Detail Variant

Gives the detail area a lighter (white) background. This is ideally used when the detail pane is displaying images with white backgrounds, such as products or logos.

### Usage

```javascript
templates: {
    ...
    options: {
        ...
        detailVariant: 'light'
    }
}
```

### Examples

- ["electronics coupons"](https://duckduckgo.com/?q=electronics+coupons)

-->