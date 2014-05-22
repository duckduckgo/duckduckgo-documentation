# Spice Templates

There are several built-in Spice templates (both `item` and `detail`) which can be used for any Spice. Most of these templates however have similar or related elements and work well together (i.e. pairings of `item` and `detail` templates). As a result, we have defined various **template groups** which **we highly recommend you use** as they will automatically determine which built-in templates will be used for your Spice. Template groups also have various features enabled by default which you can easily modify using the `options` block.

For example the `media` **template group** works well when your Spice is related to "thing" (e.g., recipe, tv show, movie, game) which has an image to display, a name, and a rating. It's likely that this template group will work for other types of results and we're here to help you determine which template group and features work best for your Spice instant answer.


# Templates Groups

There are several template groups to choose from:

- [text](#text)
- [info](#info)
- [products](#products)
- [media](#media)
- [base](#base)
- [Default Template Options (When no template group selected)](#default-template-options-when-no-template-group-selected)

------

## text

A basic template group for simple, text-only results. This template offers a title, description and footer.

### Default Templates & Options

```javascript
templates: {
    item: 'text_item',
    detail: 'text_detail',
    options: { /* none */ }
}
```

-------

## info

A template group best used for more detailed information including an image, title, and a description or arbitrary content. This template also allows you to provide an auxiliary information box (to the right) and a "More At" link.

### Default Templates & Options

```javascript
templates: {
    item: 'basic_image_item',
    item_detail: 'basic_info_item_detail',
    detail: 'basic_info_detail',
    options: {
        moreAt: true,
        aux: false
    }
}
```

------

## products

A template group best used to showcase products with an image, rating, review, brand and/or price. To give you a better idea, this template was initially created for the Amazon Spice. An optional `buy` sub-template can be used to provide a compelling call-to-action (i.e. button).

### Default Templates & Options

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

------

## media

A simplified version of the **products** group. This provides a basic `item` template, which includes an image, title and description, but uses the same `detail` template as the **products** group.

### Default Templates & Options

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

------

## base

This is the most rudimentary template group. It provides a minimal container template which is intended to be used when your Spice requires highly customized mark-up. Using this template should be a last resort if other templates don't suffice.

### Default Templates & Options

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

------

## Default Template Options (When no template group selected)

When no `templates.options` are specified **and** no template `group` has been selected, the default options are as follows:

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

A special template that is ideal for key-value data. It generates a `<table>` where each row contains the key and value.

**\*\*Note:** This template **requires** that your data to be displayed is contained in a `record_data` object.  The `record_keys` property is optional and should be created in `normalize: {}`. The `record_keys` array should provide a list of *strings* indicating the names of the keys to be included in the `<table>`.  If `record_keys` is not provided then all of the data contained in `record_data` will be displayed.  

For example this is how your `normalize` and `templates` should look when using the **record** template:

```javascript
data: { record_data: {
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

### Example

![record template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/record.png)

------

## icon

### Available Features

- icon
- title
- sub-title [optional]
- description
- footer [optional] *sub-template*

### Example

![icon template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/icon.png)

------

## text_item

### Available Features

- url [optional]
- title
- subtitle
- description
- footer [optional] *sub-template*

### Example

![text_item template ](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/icon.png)

------

## text_detail

### Available Features

- title_content [optional] *sub-template*
- title [optional, replaces `title_content`]
- content [optional] *sub-template*

### Example

![text_detail template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/ext_detail.png)

------

## basic_image_item

### Available Features

- link [optional]
- image
- title
- description [optional]
- rating [optional]
- ratingText [optional]

### Example

![basic_image_item template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_image_item.png)

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

### Example

![products_item template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_item.png)

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
- buy [optional] *sub-template*

### Example

![products_detail template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_detail.png)

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
- buy [optional] *sub-template*

### Example

![products_item_detail template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_item_detail.png)

------

## basic_info_detail

### Available Features

- image [optional]
- title [optional]
- description
- content [optional, replaces `description`] *sub-template*
- aux [optional] *sub-template*

### Example

![basic_info_detail template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_info_detail.png)

### Example with Auxiliary Information Box:

![basic_info_detail_w_aux template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_info_detail_w_aux.png)

------

## base_item

### Available Features

- url [optional]
- content *sub-template*

### Example

![base_item template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_item_simple.png)

### Complex Example

![base_item template (complex example)](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_item_complex.png)

------

## base_detail

### Available Features

- content *string* OR *sub-template*

### Example

![base_detail template](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_detail_simple.png)

### Complex Example

![base_detail template (complex example)](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_detail_complex.png)

------


# Tile Variants

If the default tile dimensions are not perfect for your Spice result, you can choose from one of the following tile variants which each offer tiles with different dimensions (some wider, some taller):

- [narrow](#narrow)
- [poster](#poster)
- [wide](#wide)
- [xwide](#xwide)
- [video](#video)

------

## narrow

Narrower tile width, normal height.

### Example

<!-- Image -->

------

## poster

Tall and thin, like a movie poster.

### Example

<!-- Image -->

------

## wide

Increased width, normal height.

### Example

<!-- Image -->

------

## xwide

Super wide, normal height.

### Example

<!-- Image -->

------

## video

Shorter height, increased width.

### Example

<!-- Image -->