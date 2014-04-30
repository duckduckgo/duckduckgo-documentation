# Spice Templates

There are several built-in Spice templates (both `item` and `detail`) which can be used for any Spice. Most of these templates however have similar or related elements and work well together (i.e. pairings of `item` and `detail` templates) As a result, we have defined various **template groups** which can be chosen to automatically use a built-in collection of templates for your spice which have various components enabled by default.

For example the `products_simple` **template group** works well when your Spice is related to a product, or "thing" which may have an image to display, a brand, a rating or review. This template group may verywell work for some other type of result and we're here to help you determine which template group and components work best for your Spice instant answer.


# Templates Groups

There are several template groups to choose from:

- [base](#base)
- [info](#info)
- [products](#products)
- [products_simple](#products_simple)

------

## base

<!-- Description -->

### Default Templates:

- item: *'base_item'*

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

## info

<!-- Description -->

### Default Templates

- item: *'basic_item'*
- item_detail: *'basic_info_item_detail'*
- detail: *'basic_info_detail'*
- wrap_detail: *'base_detail'*

### Default Options: {

- moreAt: *true*
- infoBox: *false*

### Example

<!-- Image -->

------

## products

<!-- Description -->

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

<!-- Description -->

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

# Built-In Spice Templates

The list of built-in Spice templates includes:
- [base_item](#base_item)
- [base_detail](#base_detail)
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
- descripion

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