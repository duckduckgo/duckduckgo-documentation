# Spice Templates

## Spice Template Summary

There are several built-in Spice templates (both item and detail) which can be used for any Spice.  For more information see the following pages:

- [Template Groups](#template-groups)  Defines the main type of view for the Instant Answer
- [Built-In Spice Templates](#builtin-spice-templates)  Different views and options for each template
- [Tile Variants](#tile-variants)  Used to modify width of the tiles

There are several built-in Spice templates (both `item` and `detail`) which can be used for any Spice. Most of these templates however have similar or related elements and work well together (i.e. pairings of `item` and `detail` templates). As a result, we have defined various **template groups** which **we require that you use** because using a particular group tells the Spice system which built-in templates will be used for your Spice. Template groups also have various features enabled by default which you can easily modify using the `options` block.

If you cannot use an available template for your Instant Answer, please e-mail us at open@duckduckgo.com so we can help you out. We may find that a custom template is necessary and we'll work with you to create an awesome one!

<!-- /summary -->

For example, the `media` **template group** works well when your Spice is related to "thing" (e.g., recipe, tv show, movie, game) which has an image to display, a name, and a rating. It's likely that this template group will work for other types of results and we're here to help you determine which template group and features work best for your Spice Instant Answer.

The purpose of this page is to help you understand what each template group looks like and what content works best for it. Each group is accompanied by several examples of live Spice Instant Answers using that group. Each template is accompanied by similar examples, links to code and diagrams indicating what features exist for the template and what the template layout looks like.

## Index of Spice Templates

- [**Template Groups**](#template-groups)
    - [Default Template Options](#default-template-options)
    - [Text](#text-template-group)
    - [Info](#info-template-group)
    - [Products](#products-template-group)
    - [Media](#media-template-group)
    - [Icon](#icon-template-group)
	- [Places](#places-template-group)
	- [List](#list-template-group)
    - [Base](#base-template-group)
- [**Built-In Spice Templates**](#builtin-spice-templates)
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
- [**Tile Variants**](#tile-variants)
    - [`poster`](#poster-variant)
    - [`narrow`](#narrow-variant)
    - [`wide`](#wide-variant)
    - [`xwide`](#xwide-variant)
    - [`video`](#video-variant)

<!--
[**Detail Variants**](#tile-variants)
    - [`light`](#light-detail-variant)
-->

------
## Template Groups

There are several template groups to choose from:

- [Text](#text-template-group)
- [Info](#info-template-group)
- [Products](#products-template-group)
- [Media](#media-template-group)
- [Icon](#icon-template-group)
- [Base](#base-template-group)

<!-- /summary -->

### Default Template Options

**When no `templates.options` are specified and no template `group` has been selected, the `options` are implicity set as follows:**

```javascript
    options: {
        price: true,
        brand: true,
        priceAndBrand: true,
        rating: true,
        ratingText: true,
        moreAt: true,
        content: false
    }
```

------

## Text Template Group

Best used for simple, text-only results. This template offers a title, description and footer.

### Usage

**Note:** Before using this template please read the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the proper usage of the `templates` block and the `options` block. Understanding these is crucial to using Spice templates properly and effectively.

------

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'text'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'text'
// does this for you!
templates: {
    item: 'text_item',
    detail: 'text_detail'
}
```

#### Default templates used in the 'text' group:

- [`text_item`](#textitem-template)
- [`text_detail`](#textdetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'text' template group

- ["github duckduckgo"](https://duckduckgo.com/?q=github+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js))
    ![DuckDuckGo search for "github duckduckgo"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgithub_duckduckgo.png&f=1)

- ["what rhymes with awesome"](https://duckduckgo.com/?q=what+rhymes+with+awesome) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js))
    ![DuckDuckGo search for "what rhymes with awesome"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhat_rhymes_with_awesome.png&f=1)

- ["reddit duckduckgo"](https://duckduckgo.com/?q=reddit+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js))
    ![DuckDuckGo search for "reddit duckduckgo"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Freddit_duckduckgo.png&f=1)


------

## Info Template Group

Best used for results with more detailed information including an image, title, and a description or arbitrary content. This template also allows you to provide an auxiliary information box (to the right) and a "More At" link.

### Usage

**Note:** Before using this template please read the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the proper usage of the `templates` block and the `options` block. Understanding these is crucial to using Spice templates properly and effectively.

------

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'info'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'info'
// does this for you!
templates: {
    item: 'basic_image_item',
    detail: 'basic_info_detail',
    options: {
        moreAt: true,
        aux: false
    }
}
```

#### Default templates used in the 'info' group:

- [`basic_image_item`](#basicimageitem-template)
- [`basic_info_detail`](#basicinfodetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'info' template group

- ["green day band"](https://duckduckgo.com/?q=green+day+band) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/lastfm/artist/lastfm_artist.js))
    ![DuckDuckGo search for "green day band"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgreen_day_band.png&f=1)

- ["bitcoin price"](https://duckduckgo.com/?q=bitcoin+price) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js))
    ![DuckDuckGo search for "bitcoin price"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbitcoin_price.png&f=1)

- ["gravatar matt"](https://duckduckgo.com/?q=gravatar+matt) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js))
    ![DuckDuckGo search for "gravatar matt"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgravatar_matt.png&f=1)


------

## Products Template Group

Best used to showcase products with an image, rating, review, brand and/or price. To give you a better idea, this template was initially created for the Amazon Spice. An optional `buy` sub-template can be used to provide a compelling call-to-action (i.e. button).

### Usage

**Note:** Before using this template please read the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the proper usage of the `templates` block and the `options` block. Understanding these is crucial to using Spice templates properly and effectively.

------

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'products'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'products'
// does this for you!
templates: {
	item: 'products_item',
	detail: 'products_detail',
	item_detail: 'products_item_detail',
	wrap_detail: 'base_detail',
	options: {
	    rating: true,
	    price: true,
	    brand: true
	}
}
```

#### Default templates used in the 'products' group:

- [`products_item`](#productsitem-template)
- [`products_detail`](#productsdetail-template)
- [`products_item_detail`](#productsitemdetail-template)
- [`base_detail`](#basedetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'products' template group

- ["buy batman lego"](https://duckduckgo.com/?q=buy+batman+lego) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js))
    ![DuckDuckGo search for "buy batman lego"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbuy_batman_lego.png&f=1)

- ["flight tracking apps"](https://duckduckgo.com/?q=flight+tracking+apps) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js))
    ![DuckDuckGo search for "flight tracking apps"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fflight_tracking_apps.png&f=1)

- ["octopart 1770019-2"](https://duckduckgo.com/?q=octopart%201770019-2) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js))
    ![DuckDuckGo search for "octopart 1770019-2"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Foctopart_1770019-2.png&f=1)


------

## Media Template Group

Best used for simple results that have a picture (essentially a simplified version of the **products** group). This template group provides a basic `item` template, which includes an image, title, and description. It also uses the same `detail` template as the **products** group.

### Usage

**Note:** Before using this template please read the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the proper usage of the `templates` block and the `options` block. Understanding these is crucial to using Spice templates properly and effectively.

------

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'media'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'media'
// does this for you!
templates: {
    item: 'basic_image_item',
    detail: 'products_detail',
    item_detail: 'products_item_detail',
    wrap_detail: 'base_detail',
    options: {
	    price: false,
	    brand: false,
	    rating: false,
	    ratingText: true
    }
}
```

#### Default templates used in the 'media' group:

- [`basic_image_item`](#basicimageitem-template)
- [`products_detail`](#productsdetail-template)
- [`products_item_detail`](#productsitemdetail-template)
- [`base_detail`](#basedetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'media' template group

- ["lord of the rings movie"](https://duckduckgo.com/?q=lord+of+the+rings+movie) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js))
    ![DuckDuckGo search for "lord of the rings movie"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flord_of_the_rings_movie.png&f=1)

- ["movies"](https://duckduckgo.com/?q=movies) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/in_theaters/in_theaters.js))
    ![DuckDuckGo search for "movies"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fmovies.png&f=1)

- ["BBC schedule"](https://duckduckgo.com/?q=BBC+schedule) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js))
    ![DuckDuckGo search for "BBC schedule"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbbc_schedule.png&f=1)


------

## Icon Template Group

This template is similar to the **text** group, however, the detail view is better suited to displaying an icon image.

### Usage

**Note:** Before using this template please read the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the proper usage of the `templates` block and the `options` block. Understanding these is crucial to using Spice templates properly and effectively.

------

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'icon'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'icon'
// does this for you!
templates: {
    item: 'text_item',
    detail: 'basic_icon_detail',
    item_detail: 'products_item_detail'
}
```

#### Default templates used in the 'icon' group:

- [`text_item`](#textitem-template)
- [`products_detail`](#productsdetail-template)
- [`products_item_detail`](#productsitemdetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's **features**, which you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'icon' template group

- ["alternative to photoshop"](https://duckduckgo.com/?q=alternative+to+photoshop) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js))
    ![DuckDuckGo search for "alternative to photoshop"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Falternative_to_photoshop.png&f=1)


------
## Places Template Group

This template group is ideal for displaying results where location is an important factor to the searcher. The Places template group makes it easy for searchers to view a map showing all results, or highlighting a particular item without leaving the search page.

### Usage

**Note:** Before using this template please read the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the proper usage of the `templates` block and the `options` block. Understanding these is crucial to using Spice templates properly and effectively.

------

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'places'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'places'
// does this for you!
templates: {
    item: 'places_item',
    detail: 'places_detail'
}
```

#### Default templates used in the 'places' group:

- [`places_item`](#placesitem-template)
- [`places_detail`](#placesdetail-template)

#### Places Model and View

The Places template group works together with the Places **model** and Places **view**. The Places model and view enable special map functionality and behaviors that make instant answers using Places valuable and delightful.

The model and view are specified alongside the template group property when you call `Spice.add()`. You can see how this is done under the [Model and View section](https://duck.co/duckduckhack/spice_displaying#views) of the [Spice Displaying](https://duck.co/duckduckhack/spice_displaying) page.

To work correctly, the places model requires **additional values** passed that do not appear directly in the templates. Make sure that each item includes the [attributes required by the places model](https://duck.co/duckduckhack/spice_displaying#place-attributes). Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example use of the 'places' template group

- ["parking panda"](https://duckduckgo.com/?q=parking+in+philadelphia) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/parking/parking.js))
    ![DuckDuckGo search for "parking in philadelphia"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fparking_panda.png&f=1)

------

## List Template Group

The List template group was designed for displaying a list of properties **of one item**. This can either come in the form of a bulleted list of properties, *or* a table of key-value pairs. 

Multiple items are displayed using the same `text_item` template used by Text and Icon template groups. As a result, this template group is mainly useful for instant answers designed to **return a single item** with detailed properties.

### Usage

**Note:** Before using this template please read the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the proper usage of the `templates` block and the `options` block. Understanding these is crucial to using Spice templates properly and effectively.

------

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'list'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'list'
// does this for you!
templates: {
    item: 'text_item',
    detail: 'list_detail'
}
```

#### Default templates used in the 'list' group:

- [`text_item`](#textitem-template)
- [`list_detail`](#listdetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example use of the 'list' template group

- ["whois"](https://duckduckgo.com/?q=whois+mozilla.org) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js))
	![DuckDuckGo search for "whois mozilla.org"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhois_results.png&f=1)

------

## Base Template Group

This is the most rudimentary template group. It provides a minimal container template which is intended to be used when your Spice requires highly customized mark-up. **Using this template should be a last resort if other templates don't suffice.**

### Usage

**Note:** Before using this template please read the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the proper usage of the `templates` block and the `options` block. Understanding these is crucial to using Spice templates properly and effectively.

------

Using this template requires that that you set the `group` property of the `templates` block like so:

```javascript
templates: {
    group: 'base'
}
```

<!-- /summary -->

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'base'
// does this for you!
templates: {
    item: 'base_item',
	detail: 'base_detail',
	options: {
	    price: false,
	    brand: false,
	    rating: false,
	    ratingText: false,
	    rowHighlight: false,
	    keySpacing: false,
	    moreAt: false
	}
}
```

#### Default templates used in the 'base' group:

- [`base_item`](#baseitem-template)
- [`base_detail`](#basedetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'base' template group

- ["gandhi quote"](https://duckduckgo.com/?q=gandhi+quote) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/brainy_quote/brainy_quote.js))
    ![DuckDuckGo search for "gandhi quote"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgandhi_quote.png&f=1)

- ["cpan App::cpanminus"](https://duckduckgo.com/?q=cpan+App::cpanminus) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js))
    ![DuckDuckGo search for "cpan App::cpanminus"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fcpan_app_cpanminus.png&f=1)

- ["define indelible"](https://duckduckgo.com/?q=define+indelible) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dictionary/definition/dictionary_definition.js))
    ![DuckDuckGo search for "define indelible"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fdefine_indelible.png&f=1)


------

## Built-In Spice Templates

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

- Can be used as a sub-template by the [List](#list-template-group) template group (under the [`list_detail`](#listdetail-template) template)

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

- [Text](#text-template-group)

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

- [Text](#text-template-group)

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

- [Info](#info-template-group)
- [Media](#media-template-group)

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

- [Products](#products-template-group)

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

- [Products](#products-template-group)
- [Media](#media-template-group)
- [Icon](#icon-template-group)

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

- [Products](#products-template-group)
- [Media](#media-template-group)
- [Icon](#icon-template-group)

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

- [Info](#info-template-group)

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

- [Places](#places-template-group)

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

- [Places](#places-template-group)

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

- `content` (set this value to 'record' to use the built-in [`record`](#record-template) template)
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

- [List](#list-template-group)

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

- [Base](#base-template-group)

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

- [Base](#base-template-group)

### Example usage of the "base_detail" template:

- [FlashVersion](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/flash_version/flash_version.js)
- [NPM](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/npm/npm.js)
- [XKCD](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/xkcd/xkcd.js)

------

# Spice Variants

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

- `light` - gives the detail area a lighter (white) background, ideally when displaying images with white backgrounds.

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
- `media_item` template

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

When [variants](#spice-variants) don't suffice, you can directly choose classes based on the [DDG style guide](https://duckduckgo.com/styleguide) through the `elClass` property of `templates`, in your call to `Spice.add()`. This feature is mainly used for specifying text size and color.

Classes can be directly specified to the same elements as [Variants](#spice-variants); the locations are identical. If you are specifying both `variants` and `elClass`, both will be applied together.

### Applicable Templates

Because `elClass` properties apply to the same properties as `variants`, its properties are applicable to the respective templates. For example, if you are directly specifying a class for [`tileFooter`](#tilefooter-variants), then the applicable templates are `text_item` and `media_item`.

### Options

The values that can be used in the elClass are found in the [Text and Colors](https://duckduckgo.com/styleguide#txt-n-color) section of the DuckDuckGo Style Guide. Currently, you can pass the following types of classes:

- Precision font sizes (classes which begin with `.tx--`, such as `.tx--25`)
- Text colors (classes which begin with `.tx-clr--`, such as `.tx-clr--dk`)

### Usage

`elClass` is parallel to `variants` in syntax, and both options can be specified under `templates` simultaneously. The properties are the same as those documented as [Variants](#spice-variants).

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

