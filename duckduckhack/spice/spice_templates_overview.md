# Spice Templates

There are several built-in Spice templates (both `item` and `detail`) which can be used for any Spice. Most of these templates however have similar or related elements and work well together (i.e. pairings of `item` and `detail` templates). As a result, we have defined various **template groups** which **we highly recommend you use** because using a particular group tells the Spice system which built-in templates will be used for your Spice. Template groups also have various features enabled by default which you can easily modify using the `options` block.

For example, the `media` **template group** works well when your Spice is related to "thing" (e.g., recipe, tv show, movie, game) which has an image to display, a name, and a rating. It's likely that this template group will work for other types of results and we're here to help you determine which template group and features work best for your Spice instant answer.

The purpose of this page is to help you understand what each template group looks like and what content works best for it. Each group is accompanied by several examples of live Spice instant answers using that group. Each template is accompanied by similar examples, links to code and diagrams indicating what features exist for the template and what the template layout looks like.

## Index

- [**Template Groups**](#template-groups)
    - [Default Template Options](#default-template-options)
    - [text](#text)
    - [info](#info)
    - [products](#products)
    - [media](#media)
    - [icon](#icon)
    - [base](#base)
- [**Built-In Spice Templates**](#built-in-spice-templates)
    - [record](#record)
    - [icon_item](#iconitem)
    - [text_item](#textitem)
    - [text_detail](#textdetail)
    - [basic_image_item](#basicimageitem)
    - [products_item](#productsitem)
    - [products_detail](#productsdetail)
    - [products_item_detail](#productsitemdetail)
    - [basic_info_detail](#basicinfodetail)
    - [base_item](#baseitem)
    - [base_detail](#basedetail)
- [**Tile Variants**](#tile-variants)
    - [poster](#poster)
    - [narrow](#narrow)
    - [wide](#wide)
    - [xwide](#xwide)
    - [video](#video)
<!-- - [**Detail Variants**](#tile-variants)
    - [light](#light) -->

------

# Template Groups

There are several template groups to choose from:

- [text](#text)
- [info](#info)
- [products](#products)
- [media](#media)
- [icon](#icon)
- [base](#base)

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

## text

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

When you specify this template group, it is equivalent to setting the properties of the `templates` block as follows:

```javascript
// setting the template group to: 'text'
// does this for you!
templates: {
    item: 'text_item',
    detail: 'text_detail'
}
```

#### This template group is comprised of the following built-in templates:

- [text_item](#textitem)
- [text_detail](#textdetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'text' template group

- ["github duckduckgo"](https://duckduckgo.com/?q=github+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js))
- ["what rhymes with awesome"](https://duckduckgo.com/?q=what+rhymes+with+awesome) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js))
- ["reddit duckduckgo"](https://duckduckgo.com/?q=reddit+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js))

------

## info

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

#### This template group is comprised of the following built-in templates:

- [basic_image_item](#basicimageitem)
- [basic_info_detail](#basicinfodetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'info' template group

- ["green day band"](https://duckduckgo.com/?q=green+day+band) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/lastfm/artist/lastfm_artist.js))
- ["bitcoin price"](https://duckduckgo.com/?q=bitcoin+price) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js))
- ["gravatar matt"](https://duckduckgo.com/?q=gravatar+matt) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js))

------

## products

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

#### This template group is comprised of the following built-in templates:

- [products_item](#productsitem)
- [products_detail](#productsdetail)
- [products_item_detail](#productsitemdetail)
- [base_detail](#basedetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'products' template group

- ["buy batman lego"](https://duckduckgo.com/?q=buy+batman+lego) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js))
- ["flight tracking apps"](https://duckduckgo.com/?q=flight+tracking+apps) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js))
- ["octopart 1770019-2"](https://duckduckgo.com/?q=octopart%201770019-2) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js))

------

## media

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

#### This template group is comprised of the following built-in templates:

- [basic_image_item](#basicimageitem)
- [products_detail](#productsdetail)
- [products_item_detail](#productsitemdetail)
- [base_detail](#basedetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'media' template group

- ["lord of the rings movie"](https://duckduckgo.com/?q=lord+of+the+rings+movie) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js))
- ["watch a movie"](https://duckduckgo.com/?q=watch+a+movie) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/in_theaters/in_theaters.js))
- ["BBC schedule"](https://duckduckgo.com/?q=BBC+schedule) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js))

------

## icon

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

#### This template group is comprised of the following built-in templates:

- [icon_item](#iconitem)
- [products_detail](#productsdetail)
- [products_item_detail](#productsitemdetail)

In order for these templates to display correctly, you need to ensure that each of the template's **features**, which you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'icon' template group

- ["alternative to photoshop"](https://duckduckgo.com/?q=alternative+to+photoshop) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js))

------

## base

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

#### This template group is comprised of the following built-in templates:

- [base_item](#baseitem)
- [base_detail](#basedetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'base' template group

- ["gandhi quote"](https://duckduckgo.com/?q=gandhi+quote) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/brainy_quote/brainy_quote.js))
- ["cpan App::cpanminus"](https://duckduckgo.com/?q=cpan+App::cpanminus) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js))
- ["define indelible"](https://duckduckgo.com/?q=define+indelible) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dictionary/definition/dictionary_definition.js))

------

# Built-In Spice Templates

The list of built-in Spice templates includes:

- [record](#record)
- [icon_item](#iconitem)
- [text_item](#textitem)
- [text_detail](#textdetail)
- [basic_image_item](#basicimageitem)
- [products_item](#productsitem)
- [products_detail](#productsdetail)
- [products_item_detail](#productsitemdetail)
- [basic_info_detail](#basicinfodetail)
- [base_item](#baseitem)
- [base_detail](#basedetail)

------

## record

A special template that is ideal for key-value data. It generates a `<table>` where each row contains a key and value.

**\*\*Note:** This template **requires** that your `data` object has a `record_data` property, which should contain the key-value data to be displayed. All the properties of the `record_data` object will be used as the keys for the table. However, if you want to specify exactly which properties of the `record_data` object should be displayed, an optional `record_keys` property can be defined. It should be an array of *strings*, indicating the names of the **keys** to be included in the `<table>`.

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
        content: 'record'
    }
}
```

### Available Features

*none*

### Features Diagram

![record template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/record.png)

### Template groups using "record"

- *none by default*

### Instant answers using "record"

- [UrbanDictionary](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/urban_dictionary/urban_dictionary.js)
- [MetaCpan](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js)
- [CodeSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/code_search/code_search.js)

------

## icon_item

### Available Features

- icon
- title
- sub-title [optional]
- description
- footer [optional] *sub-template*

### Features Diagram

![icon template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/icon.png)

### Template groups using "icon_item"

- [icon](#icon)

### Instant answers using "icon"

- [AlternativeTo](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js)

------

## text_item

### Available Features

- url [optional]
- title
- subtitle
- description
- footer [optional] *sub-template*

### Features Diagram

![text_item template ](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/text_item.png)

### Template groups using "text_item"

- [text](#text)

### Instant answers using "text_item"

- [GitHub](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js)
- [RubyGems](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/ruby_gems/ruby_gems.js)
- [RedditSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js)

------

## text_detail

### Available Features

- title_content [optional] *sub-template*
- title [optional, replaces `title_content`]
- content [optional] *sub-template*

### Features Diagram

![text_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/text_detail.png)

### Template groups using "text_detail"

- [text](#text)

### Instant answers using "text_detail"

- [Rhymes](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js)
- [Thesaurus](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/thesaurus/thesaurus.js)

------

## basic_image_item

### Available Features

- link [optional]
- image
- title
- description [optional]
- rating [optional]
- ratingText [optional]

### Features Diagram

![basic_image_item template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_image_item.png)

### Template groups using "basic_image_item"

- [info](#info)
- [media](#media)

### Instant answers using "basic_image_item"

- [Gravatar](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js)
- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)
- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)

------

## products_item

### Available Features

- url [optional]
- img
- title
- price
- brand [optional]
- rating [optional]
- reviewCount [optional]

### Features Diagram

![products_item template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_item.png)

### Template groups using "products_item"

- [products](#products)

### Instant answers using "products_item"

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [CouponMountain](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

------

## products_detail

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

### Features Diagram

![products_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_detail.png)

### Template groups using "products_detail"

- [products](#products)
- [media](#media)
- [icon](#icon)

### Instant answers using "products_detail"

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [CouponMountain](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

------

## products_item_detail

### Available Features

- img_m [optional, replaces `img`]
- img
- url
- price [optional] 
- brand [optional]
- rating [optional]
- abstract
- action [optional] *sub-template*

### Features Diagram

![products_item_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_item_detail.png)

### Template groups using "products_item_detail"

- [products](#products)
- [media](#media)
- [icon](#icon)

### Instant answers using "products_item_detail"

- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)
- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)
- [CouponMountain](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)

------

## basic_info_detail

### Available Features

- image [optional]
- title [optional]
- description
- content [optional, replaces `description`] *sub-template*
- aux [optional] *sub-template*

### Features Diagram

![basic_info_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_info_detail.png)

### Example with Auxiliary Information Box:

![basic_info_detail_w_aux template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_info_detail_w_aux.png)

### Template groups using "basic_info_detail"

- [info](#info)

### Instant answers using "basic_info_detail"

- [Bitcoin](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js)
- [Gravatar](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js)
- [Drinks](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/drinks/drinks.js)

------

## base_item

### Available Features

- url [optional]
- content *sub-template*

### Features Diagram

![base_item template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_item.png)

### Complex Example

![base_item template (complex example)](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_item_complex.png)

### Template groups using "base_item"

- [base](#base)

### Instant answers using "base_item"

- [GithubJobs](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github_jobs/github_jobs.js)
- [Airlines](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/airlines/airlines.js)

------

## base_detail

### Available Features

- content *string* OR *sub-template*

### Features Diagram

![base_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_detail.png)

### Complex Example

![base_detail template (complex example)](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_detail_complex.png)

### Template groups using "base_detail"

- [base](#base)

### Instant answers using "base_detail"

- [FlashVersion](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/flash_version/flash_version.js)
- [NPM](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/npm/npm.js)
- [XKCD](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/xkcd/xkcd.js)

------


# Tile Variants

If the default tile dimensions are not perfect for your Spice result, you can choose from one of the following tile variants, each of which offer different dimensions (some wider, some taller):

- [poster](#poster)
- [narrow](#narrow)
- [wide](#wide)
- [xwide](#xwide)
- [video](#video)

------

## poster

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

### Examples

- ["the dark knight movie"](https://duckduckgo.com/?q=the+dark+knight+movie)
- ["currently in theaters"](https://duckduckgo.com/?q=currently+in+theaters)

------

## narrow

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

### Examples

- ["alarm clock apps"](https://duckduckgo.com/?q=alarm+clock+apps)
- ["pa representatives"](https://duckduckgo.com/?q=pa+representatives)

------

## wide

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

### Examples

none...*yet!*

------

## xwide

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

## video

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