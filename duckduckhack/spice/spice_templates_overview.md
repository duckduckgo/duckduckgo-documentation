# Spice Templates

##Spice Template Summary

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
    - [text](#text-template-group)
    - [info](#info-template-group)
    - [products](#products-template-group)
    - [media](#media-template-group)
    - [icon](#icon-template-group)
    - [base](#base-template-group)
- [**Built-In Spice Templates**](#builtin-spice-templates)
    - [record](#record-template)
    - [icon_item](#iconitem-template)
    - [text_item](#textitem-template)
    - [text_detail](#textdetail-template)
    - [basic_image_item](#basicimageitem-template)
    - [products_item](#productsitem-template)
    - [products_detail](#productsdetail-template)
    - [products_item_detail](#productsitemdetail-template)
    - [basic_info_detail](#basicinfodetail-template)
    - [base_item](#baseitem-template)
    - [base_detail](#basedetail-template)
- [**Tile Variants**](#tile-variants)
    - [poster](#poster-variant)
    - [narrow](#narrow-variant)
    - [wide](#wide-variant)
    - [xwide](#xwide-variant)
    - [video](#video-variant)

<!--
[**Detail Variants**](#tile-variants)
    - [light](#light)
-->

------
## Template Groups

There are several template groups to choose from:

- [text](#text-template-group)
- [info](#info-template-group)
- [products](#products-template-group)
- [media](#media-template-group)
- [icon](#icon-template-group)
- [base](#base-template-group)
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

## text template group

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

- [text_item](#textitem-template)
- [text_detail](#textdetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'text' template group

- ["github duckduckgo"](https://duckduckgo.com/?q=github+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js))
    ![DuckDuckGo search for "github duckduckgo"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgithub_duckduckgo.png&f=1)

- ["what rhymes with awesome"](https://duckduckgo.com/?q=what+rhymes+with+awesome) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js))
    ![DuckDuckGo search for "what rhymes with awesome"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhat_rhymes_with_awesome.png&f=1)

- ["reddit duckduckgo"](https://duckduckgo.com/?q=reddit+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js))
    ![DuckDuckGo search for "reddit duckduckgo"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Freddit_duckduckgo.png&f=1)


------

## info template group

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

- [basic_image_item](#basicimageitem-template)
- [basic_info_detail](#basicinfodetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'info' template group

- ["green day band"](https://duckduckgo.com/?q=green+day+band) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/lastfm/artist/lastfm_artist.js))
    ![DuckDuckGo search for "green day band"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgreen_day_band.png&f=1)

- ["bitcoin price"](https://duckduckgo.com/?q=bitcoin+price) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js))
    ![DuckDuckGo search for "bitcoin price"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbitcoin_price.png&f=1)

- ["gravatar matt"](https://duckduckgo.com/?q=gravatar+matt) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js))
    ![DuckDuckGo search for "gravatar matt"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgravatar_matt.png&f=1)


------

## products template group

Best used to showcase products with an image, rating, review, brand and/or price. To give you a better idea, this template was initially created for the Amazon Spice. An optional `action` sub-template can be used to provide a compelling call-to-action (i.e. button).

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
        brand: true,
        priceAndBrand: true
    }
}
```

#### Default templates used in the 'products' group:

- [products_item](#productsitem-template)
- [products_detail](#productsdetail-template)
- [products_item_detail](#productsitemdetail-template)
- [base_detail](#basedetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'products' template group

- ["buy batman lego"](https://duckduckgo.com/?q=buy+batman+lego) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js))
    ![DuckDuckGo search for "buy batman lego"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbuy_batman_lego.png&f=1)

- ["flight tracking apps"](https://duckduckgo.com/?q=flight+tracking+apps) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js))
    ![DuckDuckGo search for "flight tracking apps"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fflight_tracking_apps.png&f=1)

- ["octopart 1770019-2"](https://duckduckgo.com/?q=octopart%201770019-2) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js))
    ![DuckDuckGo search for "octopart 1770019-2"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Foctopart_1770019-2.png&f=1)


------

## media template group

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
        priceAndBrand: false,
        rating: false,
        ratingText: true
    }
}
```

#### Default templates used in the 'media' group:

- [basic_image_item](#basicimageitem-template)
- [products_detail](#productsdetail-template)
- [products_item_detail](#productsitemdetail-template)
- [base_detail](#basedetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'media' template group

- ["lord of the rings movie"](https://duckduckgo.com/?q=lord+of+the+rings+movie) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js))
    ![DuckDuckGo search for "lord of the rings movie"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flord_of_the_rings_movie.png&f=1)

- ["movies"](https://duckduckgo.com/?q=movies) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/in_theaters/in_theaters.js))
    ![DuckDuckGo search for "movies"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fmovies.png&f=1)

- ["BBC schedule"](https://duckduckgo.com/?q=BBC+schedule) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js))
    ![DuckDuckGo search for "BBC schedule"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbbc_schedule.png&f=1)


------

## icon template group

This template is similar to the **text** group, however, it allows the use of a small icon image in the tile view.

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
    item: 'icon_item',
    detail: 'products_detail',
    item_detail: 'products_item_detail'
}
```

#### Default templates used in the 'icon' group:

- [icon_item](#iconitem-template)
- [products_detail](#productsdetail-template)
- [products_item_detail](#productsitemdetail-template)

In order for these templates to display correctly, you need to ensure that each of the template's **features**, which you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'icon' template group

- ["alternative to photoshop"](https://duckduckgo.com/?q=alternative+to+photoshop) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js))
    ![DuckDuckGo search for "alternative to photoshop"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Falternative_to_photoshop.png&f=1)


------

## base template group

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
        priceAndBrand: false,
        rating: false,
        ratingText: false,
        moreAt: false
    }
}
```

#### Default templates used in the 'base' group:

- [base_item](#baseitem-template)
- [base_detail](#basedetail-template)

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

- [record](#record-template)
- [icon_item](#iconitem-template)
- [text_item](#textitem-template)
- [text_detail](#textdetail-template)
- [basic_image_item](#basicimageitem-template)
- [products_item](#productsitem-template)
- [products_detail](#productsdetail-template)
- [products_item_detail](#productsitemdetail-template)
- [basic_info_detail](#basicinfodetail-template)
- [base_item](#baseitem-template)
- [base_detail](#basedetail-template)

------

<!-- /summary -->

## record template

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

*none*

### Template Diagram

![record template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Frecord.png&f=1)

### Template groups using the "record" template:

- *none by default*

### Example usage of the "record" template:

- [UrbanDictionary](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/urban_dictionary/urban_dictionary.js)
- [MetaCpan](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js)
- [CodeSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/code_search/code_search.js)

------

## icon_item template

### Available Features

- icon
- title
- sub-title [optional]
- description
- footer [optional] *sub-template*

### Template Diagram

![icon template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Ficon.png&f=1)

<!-- /summary -->

### Template groups using the "icon_item" template:

- [icon](#icon-template-group)

### Example usage of the "icon" template:

- [AlternativeTo](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js)

------

## text_item template

### Available Features

- url [optional]
- title
- subtitle
- description
- footer [optional] *sub-template*

### Template Diagram

![text_item template ](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Ftext_item.png&f=1)

<!-- /summary -->

### Template groups using the "text_item" template:

- [text](#text-template-group)

### Example usage of the "text_item" template:

- [GitHub](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js)
- [RubyGems](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/ruby_gems/ruby_gems.js)
- [RedditSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js)

------

## text_detail template

### Available Features

- title_content [optional] *sub-template*
- title [optional, replaces `title_content`]
- content [optional] *sub-template*

### Template Diagram

![text_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Ftext_detail.png&f=1)

<!-- /summary -->

### Template groups using the "text_detail" template:

- [text](#text-template-group)

### Example usage of the "text_detail" template:

- [Rhymes](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js)
- [Thesaurus](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/thesaurus/thesaurus.js)

------

## basic_image_item template

### Available Features

- link [optional]
- image
- title
- description [optional]
- rating [optional]
- ratingText [optional]

### Template Diagram

![basic_image_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_image_item.png&f=1)

<!-- /summary -->

### Template groups using the "basic_image_item" template:

- [info](#info-template-group)
- [media](#media-template-group)

### Example usage of the "basic_image_item" template:

- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)
- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)

------

## products_item template

### Available Features

- url [optional]
- img
- title
- price
- brand [optional]
- rating [optional]
- reviewCount [optional]

### Template Diagram

![products_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_item.png&f=1)

<!-- /summary -->

### Template groups using the "products_item" template:

- [products](#products-template-group)

### Example usage of the "products_item" template:

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [CouponMountain](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

------

## products_detail template

### Available Features

- img [optional]
- url
- heading
- price [optional]
- priceAndBrand [optional]
- brand [optional]
- rating [optional]
- reviewCount [optional]
- abstract
- action [optional] *sub-template*

### Template Diagram

![products_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_detail.png&f=1)

<!-- /summary -->

### Template groups using the "products_detail" template:

- [products](#products-template-group)
- [media](#media-template-group)
- [icon](#icon-template-group)

### Example usage of the "products_detail" template:

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [CouponMountain](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

------

## products_item_detail template

### Available Features

- img_m [optional, replaces `img`]
- img
- url
- price [optional]
- brand [optional]
- rating [optional]
- abstract
- action [optional] *sub-template*

### Template Diagram

![products_item_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fproducts_item_detail.png&f=1)

<!-- /summary -->

### Template groups using the "products_item_detail" template:

- [products](#products-template-group)
- [media](#media-template-group)
- [icon](#icon-template-group)

### Example usage of the "products_item_detail" template:

- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)
- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)
- [CouponMountain](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)

------

## basic_info_detail template

### Available Features

- image [optional]
- title [optional]
- description
- content [optional, replaces `description`] *sub-template*
- aux [optional] *sub-template*

### Template Diagram

![basic_info_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_info_detail.png&f=1)

<!-- /summary -->

### Example with Auxiliary Information Box:

![basic_info_detail_w_aux template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbasic_info_detail_w_aux.png&f=1)

### Template groups using the "basic_info_detail" template:

- [info](#info-template-group)

### Example usage of the "basic_info_detail" template:

- [Bitcoin](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js)
- [Gravatar](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js)
- [Drinks](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/drinks/drinks.js)

------

## base_item template

### Available Features

- url [optional]
- content *sub-template*

### Template Diagram

![base_item template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_item.png&f=1)

<!-- /summary -->

### Complex Example

![base_item template (complex example)](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_item_complex.png&f=1)

### Template groups using the "base_item" template:

- [base](#base-template-group)

### Example usage of the "base_item" template:

- [GithubJobs](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github_jobs/github_jobs.js)
- [Airlines](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/airlines/airlines.js)

------

## base_detail template

### Available Features

- content *string* OR *sub-template*

### Template Diagram

![base_detail template](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_detail.png&f=1)

<!-- /summary -->

### Complex Example

![base_detail template (complex example)](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fbase_detail_complex.png&f=1)

### Template groups using the "base_detail" template:

- [base](#base-template-group)

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

## poster variant

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

## narrow variant

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

## wide variant

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

## xwide variant

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

## video variant

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

## light

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
