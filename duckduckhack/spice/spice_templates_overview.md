# Spice Templates

There are several built-in Spice templates (both `item` and `detail`) which can be used for any Spice. Most of these templates however have similar or related elements and work well together (i.e. pairings of `item` and `detail` templates). As a result, we have defined various **template groups** which can be chosen to automatically use a built-in collection of templates for your spice which have various components enabled by default.

For example the `products_simple` **template group** works well when your Spice is related to a product, or "thing" which may have an image to display, a brand, a rating or review. This template group may very well work for some other type of result and we're here to help you determine which template group and components work best for your Spice instant answer.


# Templates Groups

There are several template groups to choose from:

- [base](#base)
- [text](#text)
- [info](#info)
- [products](#products)
- [products_simple](#products_simple)
- [Default Template Options (No Template Group Selected)](#default-template-options-no-template-group-selected)

------

## base

This is the most rudimentary template group. It provides a minimal container template which is intended to be used when your Spice requires highly customized mark-up. Using this template should be a last resort if other templates don't suffice.

### Default Templates:

- item: *'base_item'*
- detail: *'base_detail'*

### Default Options

- price: *false*
- brand: *false*
- priceAndBrand: *false*
- rating: *false*
- ratingText: *false*
- moreAt: *false*

### Example

<!-- Image -->

------

## text

A basic template for simple, text-only results. This template offers a title, description and footer.

### Default Templates

- item: *'text_item'*

### Default Options

*none*

### Example

<!-- Image -->

-------

## info

A template best used for more detailed information including an image, title, and a description or arbitrary content. This template also allows you to provide an infobox and a "More At" link.

### Default Templates

- item: *'basic_item'*
- item_detail: *'basic_info_item_detail'*
- detail: *'basic_info_detail'*

### Default Options: {

- moreAt: *true*
- infoBox: *false*

### Example

<!-- Image -->

------

## products

A template best used to showcase products with an image, rating, review, brand and/or price. To give you a better idea, this template was initially created for the Amazon Spice. An optional `buy` sub-template can be used to provide a compelling call-to-action (i.e. button).

### Default Templates

- item: *'products_item'*
- detail: *'products_detail'*
- item_detail: *'products_item_detail'*
- wrap_detail: *'base_detail'*

### Default Options

- rating: *true*
- price: *true*
- brand: *true*
- priceAndBrand: *true*

### Example

<!-- Image -->

------

## products_simple

A simplified version of the **products** group. This provides a basic `item` template, which includes an image, title and description, but uses the same `detail` template as the **products** group.

### Default Templates

-item: *'basic_image_item'*
-detail: *'products_detail'*
-item_detail: *'products_item_detail'*
-wrap_detail: *'base_detail'*
  
### Default Options

- price: *false*
- brand: *false*
- priceAndBrand: *false*
- rating: *false*
- ratingText: *true*

### Example

<!-- Image -->

------

## Default Template Options (No Template Group Selected)

When no `templates.options` are specified **and** no template `group` has been selected, the default options are as follows:

- price: *true*
- brand: *true*
- priceAndBrand: *true*
- rating: *true*
- ratingText: *true*
- moreAt: *true*
- content: *false*

------

# Built-In Spice Templates

The list of built-in Spice templates includes:
- [base_item](#base_item)
- [base_detail](#base_detail)
- [text_item](#text_item)
- [basic_item](#basic_item)
- [basic_image_item](#basic_image_item)
- [basic_image_detail](#basic_image_detail)
- [products_item](#products_item)
- [products_detail](#products_detail)
- [products_item_detail](#products_item_detail)
- [basic_info_detail](#basic_info_detail)
- [record](#record)

------

## base_item

### Components

- url [optional]
- content

### Example

<!-- todo -->

------

## base_detail

### Components

- content

### Example

<!-- todo -->

------

## text_item

### Components

- url [optional]
- title
- subtitle
- description
- footer [optional] *sub-template*

### Example

<!-- todo -->

------

## basic_item

### Components

- content

### Example

<!-- todo -->

------

## basic_image_item

### Components

- link [optional]
- image
- title
- description [optional]
- rating [optional]
- ratingText [optional]

### Example

<!-- todo -->

------

## basic_image_detail

### Components

- image [optional]
- title
- content

### Example

<!-- todo -->

------

## products_item

### Components

- url [optional]
- img
- title
- price
- brand [optional]
- rating [optional]
- reviewCount [optional]

### Example

<!-- todo -->

------

## products_detail

### Components

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

<!-- todo -->

------

## products_item_detail

### Components

- img_m [optional, replaces `img`]
- img
- url
- price [optional] 
- brand [optional]
- rating [optional]
- abstract
- buy [optional] *sub-template*

### Example

<!-- todo -->

------

## basic_info_detail

### Components

- image [optional]
- title [optional]
- content [optional, replaces `description`] *sub-template*
- description

### Example

<!-- todo -->

------

## record

### Components

- record_keys *array*
    + key
    + value

### Example

<!-- todo -->