# Spice Templates

There are several built-in Spice templates (both `item` and `detail`) which can be used for any Spice. Most of these templates however have similar or related elements and work well together (i.e. pairings of `item` and `detail` templates). As a result, we have defined various **template groups** which **we highly recommend you use** as they will automatically determine which built-in templates will be used for your Spice. Template groups also have various features enabled by default which you can easily modify using the `options` block.

For example the `media` **template group** works well when your Spice is related to "thing" (e.g., recipe, tv show, movie, game) which has an image to display, a name, and a rating. It's likely that this template group will work for other types of results and we're here to help you determine which template group and features work best for your Spice instant answer.


# Templates Groups

There are several template groups to choose from:

- [text](#text)
- [info](#info)
- [products](#products)
- [media](#media)
- [icon](#icon)
- [base](#base)
- [Default Template Options (When no template group selected)](#default-template-options-when-no-template-group-selected)

------

## text

Best used for simple, text-only results. This template offers a title, description and footer.

### Usage

Specify the template group like this:

```javascript
templates: {
    group: 'text'
}
```

which is equivalent to this:

```javascript
templates: {
    item: 'text_item',
    detail: 'text_detail'
}
```

### Examples

- ["github duckduckgo"](https://duckduckgo.com/?q=github+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js))
- ["what rhymes with awesome"](https://duckduckgo.com/?q=what+rhymes+with+awesome) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js))
- ["reddit duckduckgo"](https://duckduckgo.com/?q=reddit+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit/reddit.js))

------

## info

Best used for results with more detailed information including an image, title, and a description or arbitrary content. This template also allows you to provide an auxiliary information box (to the right) and a "More At" link.

### Usage

Specify the template group like this:

```javascript
templates: {
    group: 'info'
}
```

which is equivalent to this:

```javascript
templates: {
    item: 'basic_image_item',
    detail: 'basic_info_detail',
    options: {
        moreAt: true,
        aux: false
    }
}
```

### Examples

- ["green day band"](https://duckduckgo.com/?q=green+day+band) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/lastfm/artist/lastfm_artist.js))
- ["bitcoin price"](https://duckduckgo.com/?q=bitcoin+price) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js))
- ["gravatar matt"](https://duckduckgo.com/?q=gravatar+matt) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js))

------

## products

Best used to showcase products with an image, rating, review, brand and/or price. To give you a better idea, this template was initially created for the Amazon Spice. An optional `action` sub-template can be used to provide a compelling call-to-action (i.e. button).

### Usage

Specify the template group like this:

```javascript
templates: {
    group: 'products'
}
```

which is equivalent to this:

```javascript
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

### Examples

- ["buy batman lego"](https://duckduckgo.com/?q=buy+batman+lego) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js))
- ["flight tracking apps"](https://duckduckgo.com/?q=flight+tracking+apps) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js))
- ["octopart 1770019-2"](https://duckduckgo.com/?q=octopart%201770019-2) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js))

------

## media

Best used for simple results that have a picture (essentially a simplified version of the **products** group). This template group provides a basic `item` template, which includes an image, title, and description. It also uses the same `detail` template as the **products** group.

### Usage

Specify the template group like this:

```javascript
templates: {
    group: 'media'
}
```

which is equivalent to this:

```javascript
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

### Examples

- ["lord of the rings movie"](https://duckduckgo.com/?q=lord+of+the+rings+movie) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js))
- ["watch a movie"](https://duckduckgo.com/?q=watch+a+movie) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/in_theaters/in_theaters.js))
- ["BBC schedule"](https://duckduckgo.com/?q=BBC+schedule) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js))

------

## icon

This template is similar to the **text** group, however, it allows the use of a small icon image in the tile view.

### Usage

Specify the template group like this:

```javascript
templates: {
    group: 'icon'
}
```

which is equivalent to this:

```javascript
templates: {
    item: 'icon_item',
    detail: 'products_detail',
    item_detail: 'products_item_detail'
}
```

### Examples

- ["alternative to photoshop"](https://duckduckgo.com/?q=alternative+to+photoshop) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js))

------

## base

This is the most rudimentary template group. It provides a minimal container template which is intended to be used when your Spice requires highly customized mark-up. Using this template should be a last resort if other templates don't suffice.

### Usage

Specify the template group like this:

```javascript
templates: {
    group: 'base'
}
```

which is equivalent to this:

```javascript
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

### Examples

- ["gandhi quote"](https://duckduckgo.com/?q=gandhi+quote) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/brainy_quote/brainy_quote.js))
- ["cpan App::cpanminus"](https://duckduckgo.com/?q=cpan+App::cpanminus) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js))
- ["define indelible"](https://duckduckgo.com/?q=define+indelible) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dictionary/definition/dictionary_definition.js))

------

## Default Template Options (When no template group selected)

When no `templates.options` are specified **and** no template `group` has been selected, the `options` are implicity set as follows:

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

# Built-In Spice Templates

The list of built-in Spice templates includes:

- [record](#record)
- [icon](#icon)
- [text_item](#text_item)
- [text_detail](#text_detail)
- [basic_image_item](#basic_image_item)
- [products_item](#products_item)
- [products_detail](#products_detail)
- [products_item_detail](#products_item_detail)
- [basic_info_detail](#basic_info_detail)
- [base_item](#base_item)
- [base_detail](#base_detail)

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

## icon

### Available Features

- icon
- title
- sub-title [optional]
- description
- footer [optional] *sub-template*

### Features Diagram

![icon template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/icon.png)

### Template groups using "icon"

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