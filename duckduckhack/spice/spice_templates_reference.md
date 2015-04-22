# Spice Templates Reference

The basic building blocks of displaying Spice Instant Answers are the templates and variants. Below is a detailed reference of each template and its workings.

The reference is divided into two parts:

- [Spice Templates](#spice-templates)
- [Tile Variants](#tile-variants)

## Important Note

Before using these templates please read the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the proper usage of both the `templates` block and the `options` block. 

Understanding these is crucial to implementing Spice templates properly and effectively.

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

A special template that is ideal for key-value data. It generates a `<table>` where each row contains a key and value. Often used as a sub-template, for example by the [`list`](#list-template) template.

### Template Diagram

![record template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Frecord.png&f=1)

### Available Features

- `record_data` *object* (contains key-value pairs to display in table format)

### Usage

This template requires that a `record_data` property, which should contain the key-value data to be displayed. All the properties of the `record_data` object will be used as the keys for the table. 

However, if you want to specify exactly which properties of the `record_data` object should be displayed, you can define an optional `record_keys` property. This is an array of strings, specifying which key-value pairs of `record_data` will be included.

An optional property called `rowHighlight` can be added to `options` to turn on alternating row highlighting.

### Sample Code

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

### Example usage of the `record` template:

- [UrbanDictionary](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/urban_dictionary/urban_dictionary.js)
- [MetaCpan](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js)
- [CodeSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/code_search/code_search.js)
- [Whois](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js)

### Template groups using the `record` template:

- Can be used as a sub-template by the [List](https://duck.co/duckduckhack/spice_templates_overview#list-template-group) template group (under the [`list_detail`](#listdetail-template) template)

------

## `text_item` Template

Template for displaying textual information tiles, each with an optional icon.

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

### Available Features

- `icon` [optional] *url path to icon*
- `url` [optional]
- `title`
- `altSubtitle` [optional]
- `subtitle` [optional]
- `description`
- `footer` [optional] *sub-template*

### Example usage of the "text_item" template:

- [GitHub](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js)
- [RubyGems](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/ruby_gems/ruby_gems.js)
- [RedditSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js)
- [AlternativeTo](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js)

### Template groups using the "text_item" template:

- [Text](https://duck.co/duckduckhack/spice_templates_overview#text-template-group)

------

## `text_detail` Template

A template for displaying textual information detail, with no image or icon.

### Template Diagram

![text_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Ftext_detail.png&f=1)

```
+------------------+
title_content or title
subtitle_content or subtitle
content
+------------------+
```

### Available Features

- `title_content` [optional] *sub-template*
- `title` [optional] (available only if `title_content` is not specified)
- `subtitle_content` [optional] *sub-template*
- `subtitle` [optional] (available only if `subtitle_content` is not specified)
- `content` [optional] *sub-template*

### Example usage of the "text_detail" template:

- [Rhymes](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js)
- [Thesaurus](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/thesaurus/thesaurus.js)

### Template groups using the "text_detail" template:

- [Text](https://duck.co/duckduckhack/spice_templates_overview#text-template-group)

------

## `basic_image_item` Template

A tile template where images are the main feature, accompanied by text.

### Template Diagram

![basic_image_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_image_item.png&f=1)

### Available Features

- `url` [optional]
- `image` *url path to image*
- `title`
- `description` [optional]
- `rating` [optional]
- `ratingText` [optional]

### Example usage of the "basic_image_item" template:

- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)
- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)

### Template groups using the "basic_image_item" template:

- [Info](https://duck.co/duckduckhack/spice_templates_overview#info-template-group)
- [Media](https://duck.co/duckduckhack/spice_templates_overview#media-template-group)

------

## `products_item` Template

A tile item template where images are emphasized, with features suited for items that can be purchased.

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

### Available Features

- `url` [optional]
- `img` *url path to image*
- `title`
- `price` [optional]
- `brand` [optional]
- `rating` [optional]
- `reviewCount` [optional]
- `url_review` [optional] *url path to reviews*

### Example usage of the "products_item" template:

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

### Template groups using the "products_item" template:

- [Products](https://duck.co/duckduckhack/spice_templates_overview#products-template-group)

------

## `products_detail` Template

A detail template where image is emphasized, suited to feature for an item that can be purchased.

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

### Example usage of the "products_detail" template:

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

### Template groups using the "products_detail" template:

- [Products](https://duck.co/duckduckhack/spice_templates_overview#products-template-group)
- [Media](https://duck.co/duckduckhack/spice_templates_overview#media-template-group)
- [Icon](https://duck.co/duckduckhack/spice_templates_overview#icon-template-group)

------

## `products_item_detail` Template

A template for drilling-down into a particular item on the same page. Emphasizes an image, and suited to feature for an item that can be purchased. This template features an optional call-to-action.

### Template Diagram

![products_item_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_item_detail.png&f=1)

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

### Example usage of the "products_item_detail" template:

- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)
- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)

### Template groups using the "products_item_detail" template:

- [Products](https://duck.co/duckduckhack/spice_templates_overview#products-template-group)
- [Media](https://duck.co/duckduckhack/spice_templates_overview#media-template-group)
- [Icon](https://duck.co/duckduckhack/spice_templates_overview#icon-template-group)

------

## `basic_info_detail` Template

A detail template which shows in-depth information. This template includes an auxiliary area for listing properties.

### Template Diagram

![basic_info_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_info_detail.png&f=1)

![basic_info_detail_w_aux template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_info_detail_w_aux.png&f=1)

```
+-----------------------------------------+
image
title
subtitle						auxTitle
content or description			aux
+-----------------------------------------+
```

### Available Features

- `url`
- `image` [optional] *url path to image*
- `title` [optional]
- `subtitle` [optional] (available only if `title` specified)
- `content` [optional] *sub-template*
- `description` (available and required only if `content` sub-template not specified)
- `aux` [optional] *sub-template*
- `auxTitle` (available and required only if `aux` specified)

### Example usage of the "basic_info_detail" template:

- [Bitcoin](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js)
- [Gravatar](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js)
- [Drinks](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/drinks/drinks.js)

### Template groups using the "basic_info_detail" template:

- [Info](https://duck.co/duckduckhack/spice_templates_overview#info-template-group)

------

## `places_item` Template

An item template which displays multiple location results on one map.

Clicking a places item both indicates its location on a map, as well as 'flips' the item to display more detailed information. The `places_item` template can conceptually be divided into its 'front' and 'back'.

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

### Available Features

#### 'Front' of each item:
- `image` [optional] *url path to image*
- `name`
- `title` (available only if `image` specified)
- `ratingImageURL` [optional]
- `rating` [optional] (available only if `ratingImageURL` not specified)
- `reviews` [optional]

#### 'Back' of each item: (displayed upon click)
- `name`
- `url`
- `price` [optional]
- `address_lines` [optional]
- `address` [optional] (available only if `address_lines` not specified)
- `phone` [optional]

#### Map View

This view is displayed when the 'front' is clicked, together with the 'back' (above).

![DuckDuckGo search for "cafes near ann arbor"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flocal_results_map.png&f=1)

### Example usage of the "places_item" template:

- [Parking Panda](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/parking/parking.js): search for [parking in new york](https://duckduckgo.com/?q=parking+in+new+york).
- Local results (built-in to DDG): search for [cafes near Ann Arbor](https://duckduckgo.com/?q=cafes+near+ann+arbor).

### Template groups using the "places_item" template:

- [Places](https://duck.co/duckduckhack/spice_templates_overview#places-template-group)

------

## `places_detail` Template

A detail template for displaying information about a single location on a map backdrop.

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

### Example usage of the "places_detail" template:

- Local results (built-in to DDG): search for [a particular business](https://duckduckgo.com/?q=espresso+italiano+maui).

### Template groups using the "places_detail" template:

- [Places](https://duck.co/duckduckhack/spice_templates_overview#places-template-group)

------

## `list_detail` Template

A detail template for displaying of a title and subtitle above a bulleted list, or a table of key-value pairs. 

### Template Diagram

![DuckDuckGo search for "whois mozilla.org"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhois_results.png&f=1)

```
+-------------------+

title
subtitle
record_data *or* list

+-------------------+
```

### Available Features

- `title` [optional]
- `subtitle` [optional]

#### If Displaying Table of Key-Value Pairs:

- `content` *sub-template* (set this value to 'record' to use the built-in [`record`](#record-template) template)
- `record_data` *object containing the key-value pairs to display*

#### If Displaying Bulleted List of Values:

- `list_content` *sub-template* (populates within each `li` element)
- `list` *array of objects* (each object contains the properties used by `list_content` sub-template)

### Usage 

To display a bulleted list, pass a sub-template to the `list_content` property. To display a table of key-value pairs, pass the [`record`](#record-template) template to the `content` property.

When displaying a bulleted list, the simplest case would be to pass `list` an array of objects like `{value: 'foo'}` and specify `list_content` to be a sub-template which only reads `{{value}}`.

### Example usage of the "list_detail" template:

- [Whois](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js) (search for ['whois mozilla.org'](https://duckduckgo.com/?q=whois+mozilla.org))

### Template groups using the "list_detail" template:

- [List](https://duck.co/duckduckhack/spice_templates_overview#list-template-group)

------

## `base_item` Template

An item template for containing fully customized markup.

### Template Diagram

![base_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_item.png&f=1)

<!-- /summary -->

### Available Features

- `url` [optional]
- `content` *sub-template*

### Example usage of the "base_item" template:

- [GithubJobs](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github_jobs/github_jobs.js)
- [Airlines](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/airlines/airlines.js)

### Complex Example

![base_item template (complex example)](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_item_complex.png&f=1)

### Template groups using the "base_item" template:

- [Base](https://duck.co/duckduckhack/spice_templates_overview#base-template-group)

------

## `base_detail` Template

A detail template for containing fully customized markup.

### Template Diagram

![base_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_detail.png&f=1)

### Available Features

- `content` *string* or *sub-template*

### Example usage of the "base_detail" template:

- [FlashVersion](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/flash_version/flash_version.js)
- [NPM](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/npm/npm.js)
- [XKCD](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/xkcd/xkcd.js)

### Complex Example

![base_detail template (complex example)](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_detail_complex.png&f=1)

### Template groups using the "base_detail" template:

- [Base](https://duck.co/duckduckhack/spice_templates_overview#base-template-group)

------

# Spice Variants Reference

If you'd like to modify a template to fit your needs, the Spice framework offers preset options called Variants. Variants are passed as the `variants` property of `templates`, in your call to `Spice.add()`. 

Variants correspond to pre-determined css classes (or combinations of classes) from the [DDG style guide](https://duckduckgo.com/styleguide) that work particularly well in each context.

*We strongly recommend using variants since they make it easy to quickly customize the appearance in a standardized way. However, if variants do not meet your needs, you may consider [directly specifying classes](#directly-specifying-classes).*

## `tile` Variants

If the default tile dimensions are not perfect for your Spice result, you can use tile variants to modify the containers of your `item` template.

![tile variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftile_variant.png&f=1)

### Applicable Templates

- `base_item` template
- `basic_image_item` template
- `products_item` template

### Options

- `narrow` - narrower tile width, normal height (["alarm clock apps"](https://duckduckgo.com/?q=alarm+clock+apps), ["pa representatives"](https://duckduckgo.com/?q=pa+representatives))
- `wide` - increased width, normal height
- `xwide` - super wide, normal height (["flight aa102"](https://duckduckgo.com/?q=flight+aa102))
- `video` - shorter height, increased width
- `poster` - tall and thin, like a movie poster (["the dark knight movie"](https://duckduckgo.com/?q=the+dark+knight+movie), ["currently in theaters"](https://duckduckgo.com/?q=currently+in+theaters))

### `tile` Preset Options

The following four values for `tile` variant act as presets for [`tileTitle`](#tiletitle-variants) and [`tileSnippet`](#tilesnippet-variants) variant. These are combinations that our design team has found to work particularly well together.

- `basic1` - equivalent to setting `tileTitle: '2line'` and `tileSnippet: 'small'` (["rubygems cucumber"](https://duckduckgo.com/?q=rubygems+cucumber))
- `basic2` - equivalent to setting `tileTitle: '3line-small'` and `tileSnippet: 'large'`
- `basic3` - equivalent to setting `tileTitle: '3line-large'` and `tileSnippet: 'small'`
- `basic4` - equivalent to setting `tileTitle: '1line-large'` and `tileSnippet: 'large'` (["github zeroclickinfo"](https://duckduckgo.com/?q=github+zeroclickinfo))

### Usage

```javascript
templates: {
	...
	variants: {
		tile: 'poster'
	}
 }
```

------

## `detail` Variants

This variant allows you to modify the `detail` template of your Instant Answer. Currently there is only one detail variant outside the default styling.

### Applicable Templates

- All tile containers (which wrap `item` templates)

### Options

- `light` - gives the detail area a lighter (white) background, ideally when displaying images with white backgrounds (["electronics coupons"](https://duckduckgo.com/?q=electronics+coupons))

#### Usage

```javascript
templates: {
	...
	variants: {
		detail: 'light'
	}
 }
```

------

## `tileTitle` Variants

This variant changes the size of the title element, if it exists in the chosen template.

![tileTitle variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftiletitle_variant.png&f=1)

### Applicable Templates

- `text_item` template

### Options

- `1line`
- `1line-large`
- `2line` - (["perl jobs in san francisco"](https://duckduckgo.com/?q=perl+jobs+in+san+francisco&ia=jobs))
- `3line`
- `3line-small` - (["reddit baking"](https://duckduckgo.com/?q=reddit+baking&ia=social))
- `3line-large`

Another way to set a `tileTitle` variant is to use [`tile` preset options](#tile-preset-options). These are combinations of `tileTitle` and `tileSnippet` values that our design team has found to work particularly well together.

### Usage

```javascript
templates: {
	...
	variants: {
		tileTitle: '1line'
	}
 }
```

------

## `iconTitle` Variants

This variant changes the size of the title element, specifically for the `basic_icon_detail` template.

### Applicable Templates

- `basic_icon_detail` template

### Options

- `large`

### Usage

```javascript
templates: {
	...
	variants: {
		iconTitle: 'large'
	}
 }
```

------

## `tileSubtitle` Variants

This variant changes the amount of lines available in the subtitle element, for the `text_item` template.

### Applicable Templates

- `text_item` template

### Options

- `2line`

### Usage

```javascript
templates: {
	...
	variants: {
		tileSubtitle: '2line'
	}
 }
```

------

## `tileSnippet` Variants

This variant changes the amount of space used for the description or content sub-template, if it exists in the chosen template.

![tileSnippet diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftilesnippet_variant.png&f=1)

### Applicable Templates

- `text_item` template

### Options

- `small`
- `large` (["global mobile data usage"](https://duckduckgo.com/?q=global+mobile+data+usage&ia=answer), ["rubygems cucumber"](https://duckduckgo.com/?q=rubygems+cucumber&ia=software))

Another way to set a `tileSnippet` variant is to use [`tile` preset options](#tile-preset-options). These are combinations of `tileTitle` and `tileSnippet` values that our design team has found to work particularly well together.

### Usage

```javascript
templates: {
	...
	variants: {
		tileSnippet: 'small'
	}
 }
```

------

## `tileFooter` Variants

This variant changes the amount of space allowed for the footer sub-template, if it exists in the chosen template.

![tileFooter variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftilefooter_variant.png&f=1)

### Applicable Templates

- `text_item` template

### Options

- `2line` (["reddit baking"](https://duckduckgo.com/?q=reddit+baking&ia=social))
- `3line` (["people in space"](https://duckduckgo.com/?q=people+in+space&ia=answer))
- `4line` (["live shows in london"](https://duckduckgo.com/?q=live+shows+in+london&ia=concerts))

### Usage

```javascript
templates: {
	...
	variants: {
		tileFooter: '2line'
	}
 }
```

------

## `tileRating` Variants

This variant sets the css float direction of the star rating element, if it exists in the template. As you can see in the examples, it only affects the float behavior of the stars themselves - not any accompanying elements.

![tileRating variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ftilerating_variant.png&f=1)

### Applicable Templates

- `basic_image_item`

### Options

- `starsLeft` (["amazon ninja costume"](https://duckduckgo.com/?q=amazon+ninja+costume&ia=products))
- `starsRight` (["recipes quinoa"](https://duckduckgo.com/?q=recipes+quinoa&ia=recipes))

### Usage

```javascript
templates: {
	...
	variants: {
		tileRating: 'starsLeft'
	}
 }
```

------

## `iconImage` Variants

For templates containing an icon element, this variant sets its size.

![iconImage variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ficonimage_variant.png&f=1)

### Applicable Templates

- `basic_icon_detail` template

### Options

- `small` (["alternative to emacs"](https://duckduckgo.com/?q=alternative+to+emacs&ia=software))
- `medium`
- `large`

### Usage

```javascript
templates: {
	...
	variants: {
		iconImage: 'small'
	}
 }
```

------

## `iconBadge` Variants

For templates containing an icon badge (an inline colored container with text), this variant sets its size. 

![iconBadge variant diagram](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvariant_diagrams%2Ficonbadge_variant.png&f=1)

### Applicable Templates

- `basic_icon_detail` template

### Options

- `small`
- `medium` (["UV Index"](https://duckduckgo.com/?q=UV+index), US searches only)
- `large`

### Usage

```javascript
templates: {
	...
	variants: {
		iconBadge: 'small'
	}
 }
```

------

# Directly Specifying Classes

When [variants](#spice-variants-reference) don't suffice, you can directly choose classes based on the [DDG style guide](https://duckduckgo.com/styleguide) through the `elClass` property of `templates`, in your call to `Spice.add()`. This feature is mainly used for specifying text size and color.

Classes can be directly specified to the same elements as [Variants](#spice-variants-reference); the locations are identical. If you are specifying both `variants` and `elClass`, both will be applied together.

### Applicable Templates

Because `elClass` properties apply to the same properties as `variants`, its properties are applicable to the respective templates. For example, if you are directly specifying a class for [`tileFooter`](#tilefooter-variants), then the only applicable template is `text_item`.

### Options

The values that can be used in the elClass are found in the [Text and Colors](https://duckduckgo.com/styleguide#txt-n-color) section of the DuckDuckGo Style Guide. Currently, you can pass the following types of classes:

- Precision font sizes (classes which begin with `.tx--`, such as `.tx--25`)
- Text colors (classes which begin with `.tx-clr--`, such as `.tx-clr--dk`)

### Usage

`elClass` is parallel to `variants` in syntax, and both options can be specified under `templates` simultaneously. The properties are the same as those documented as [Variants](#spice-variants-reference).

```javascript
templates: {
	...
	elClass: {
		tileSubtitle: 'tx--25',
		tileFooter: 'tx--11',
		...
	}
 }
```

### Example

- Tor Node: ["tor node 198.96.155.3"](https://duckduckgo.com/?q=tor+node+198.96.155.3&ia=tornode)  ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/zaahir/tor-node-refine/share/spice/tor_node/tor_node.js#L185))