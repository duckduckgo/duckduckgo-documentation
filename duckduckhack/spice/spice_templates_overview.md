# Spice Templates
<h2 class="summary" moreAt="spice_templates_overview">Spice Template Summary</h2>
<!--
<p class="summary-text">There are several built-in Spice templates (both item and detail) which can be used for any Spice.  For more information see the following pages:</p>
-->
<li class="summary-text"><a  href="http://duck.co/duckduckhack/spice_templates_overview#template-groups">Template Groups</a>- Defines the main type of view for the instant answer</li>
<li class="summary-text"><a  href="http://duck.co/duckduckhack/spice_templates_overview#built-in-spice-templates">Built-In Spice Templates</a>- Different views and options for each template</li>
<li class="summary-text"><a  href="http://duck.co/duckduckhack/spice_templates_overview#tile-variants">Tile Variants</a>- Used to modify width of the tiles</li>

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

<!--
[**Detail Variants**](#tile-variants)
    - [light](#light)
-->

------
<!--
<h2 class='summary' moreat='spice_templates_overview#template-groups'>Spice Template Groups</h2>
<li class='summary-text'><a href='http://duck.co/duckduckhack/spice_templates_overview#text'>text</a>- basic template to display text-only data in detail or tile views</li>
<li class='summary-text'><a href='http://duck.co/duckduckhack/spice_templates_overview#info'>info</a>- detailed results with image, description, and title</li>
<li class='summary-text'><a href='http://duck.co/duckduckhack/spice_templates_overview#products'>products</a>- used for products with an image, rating, review, brand/price</li>
<li class='summary-text'><a href='http://duck.co/duckduckhack/spice_templates_overview#media'>media</a>- simple results with an image (simplified version of the products group)</li>
<li class='summary-text'><a href='http://duck.co/duckduckhack/spice_templates_overview#icon'>icon</a>- similar to text group but with a small icon in the tile</li>
<li class='summary-text'><a href='http://duck.co/duckduckhack/spice_templates_overview#base'>base</a>- minimal container for highly customized mark-up</li>
-->
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

#### Default templates used in the 'text' group:

- [text_item](#textitem)
- [text_detail](#textdetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.
<!--
<h2 class='summary' moreAt="spice_templates_overview#text">Spice text template</h2>
<p class='summary-text'>The text group has both a tile and detail view and is used for displaying basic text-only results. See the <a href="http://duck.co/duckduckhack/spice_templates_overview#text">Text Template</a> page.</p>
<p class='summary-text'>Example use:<a href="https://duckduckgo.com/?q=github+duckduckgo"> "github duckduckgo"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/github/github.js">(code)</a></p>
<a class="summary-text" href="https://duckduckgo.com/?q=github+duckduckgo"><img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/github_duckduckgo.png'></img></a>
-->

### Example uses of the 'text' template group

- ["github duckduckgo"](https://duckduckgo.com/?q=github+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js))
    ![DuckDuckGo search for "github duckduckgo"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/github_duckduckgo.png)

- ["what rhymes with awesome"](https://duckduckgo.com/?q=what+rhymes+with+awesome) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js))
    ![DuckDuckGo search for "what rhymes with awesome"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/what_rhymes_with_awesome.png)

- ["reddit duckduckgo"](https://duckduckgo.com/?q=reddit+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js))
    ![DuckDuckGo search for "reddit duckduckgo"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/reddit_duckduckgo.png)


------
<!--
<h2 class='summary' moreAt="spice_templates_overview#info">Spice info template</h2>
<p class='summary-text'>
Best used for results with more detailed information including an image, title, and a description or arbitrary content. This template also allows you to provide an auxiliary information box (to the right) and a "More At" link.
</p>
<p class='summary-text'>Example use:<a href="https://duckduckgo.com/?q=green+day+band"> "green day band"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/lastfm/artist/lastfm_artist.js">(code)</a></p>
<a class="summary-text" href="https://duckduckgo.com/?q=green+day+band"><img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/green_day_band.png'></img></a>
-->
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

#### Default templates used in the 'info' group:

- [basic_image_item](#basicimageitem)
- [basic_info_detail](#basicinfodetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'info' template group

- ["green day band"](https://duckduckgo.com/?q=green+day+band) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/lastfm/artist/lastfm_artist.js))
    ![DuckDuckGo search for "green day band"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/green_day_band.png)

- ["bitcoin price"](https://duckduckgo.com/?q=bitcoin+price) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js))
    ![DuckDuckGo search for "bitcoin price"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/bitcoin_price.png)

- ["gravatar matt"](https://duckduckgo.com/?q=gravatar+matt) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js))
    ![DuckDuckGo search for "gravatar matt"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/gravatar_matt.png)


------
<!--
<h2 class='summary' moreAt="spice_templates_overview#products">Spice products template</h2>
<p class='summary-text'>
Best used to showcase products with an image, rating, review, brand and/or price. To give you a better idea, this template was initially created for the Amazon Spice. An optional `action` sub-template can be used to provide a compelling call-to-action (i.e. button).
</p>
<p class='summary-text'>Example use:<a href="https://duckduckgo.com/?q=github+duckduckgo"> "flight tracking apps"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/quixey/quixey.js">(code)</a></p>
<a class="summary-text" href="https://duckduckgo.com/?q=flight+tracking+apps"><img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/flight_tracking_apps.png'></img></a>
-->
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

#### Default templates used in the 'products' group:

- [products_item](#productsitem)
- [products_detail](#productsdetail)
- [products_item_detail](#productsitemdetail)
- [base_detail](#basedetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'products' template group

- ["buy batman lego"](https://duckduckgo.com/?q=buy+batman+lego) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js))
    ![DuckDuckGo search for "buy batman lego"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/buy_batman_lego.png)

- ["flight tracking apps"](https://duckduckgo.com/?q=flight+tracking+apps) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js))
    ![DuckDuckGo search for "flight tracking apps"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/flight_tracking_apps.png)

- ["octopart 1770019-2"](https://duckduckgo.com/?q=octopart%201770019-2) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js))
    ![DuckDuckGo search for "octopart 1770019-2"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/octopart_1770019-2.png)


------
<!--
<h2 class="summary" style="display: none" moreAt="spice_templates_overview#media">Spice media template</h2>
<p class='summary-text'>
Best used for simple results that have a picture (essentially a simplified version of the **products** group). This template group provides a basic `item` template, which includes an image, title, and description. It also uses the same `detail` template as the **products** group.
</p>
<p class='summary-text'>Example use:<a href="https://duckduckgo.com/?=bbc+schedule"> "BBC schedule"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/bbc/bbc.js">(code)</a></p>
<a class="summary-text" href="https://duckduckgo.com/?q=bbc+schedule"><img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/bbc_schedule.png'></img></a>
-->

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

#### Default templates used in the 'media' group:

- [basic_image_item](#basicimageitem)
- [products_detail](#productsdetail)
- [products_item_detail](#productsitemdetail)
- [base_detail](#basedetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'media' template group

- ["lord of the rings movie"](https://duckduckgo.com/?q=lord+of+the+rings+movie) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js))
    ![DuckDuckGo search for "lord of the rings movie"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/lord_of_the_rings_movie.png)

- ["movies"](https://duckduckgo.com/?q=movies) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/in_theaters/in_theaters.js))
    ![DuckDuckGo search for "movies"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/movies.png)

- ["BBC schedule"](https://duckduckgo.com/?q=BBC+schedule) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js))
    ![DuckDuckGo search for "BBC schedule"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/bbc_schedule.png)


------
<!--
<h2 class='summary' moreAt="spice_templates_overview#icon">Spice icon template</h2>
<p class='summary-text'>
This template is similar to the **text** group, however, it allows the use of a small icon image in the tile view.
</p>
<p class='summary-text'>Example use:<a href="https://duckduckgo.com/?=alternative+to+photoshop"> "alternative to photoshop"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/alternative_to/alternative_to.js">(code)</a></p>
<a class="summary-text" href="https://duckduckgo.com/?q=bbc+schedule"><img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/alternative_to_photoshop.png'></img></a>
-->
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

#### Default templates used in the 'icon' group:

- [icon_item](#iconitem)
- [products_detail](#productsdetail)
- [products_item_detail](#productsitemdetail)

In order for these templates to display correctly, you need to ensure that each of the template's **features**, which you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'icon' template group

- ["alternative to photoshop"](https://duckduckgo.com/?q=alternative+to+photoshop) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js))
    ![DuckDuckGo search for "alternative to photoshop"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/alternative_to_photoshop.png)


------
<!--
<h2 class='summary' moreAt="spice_templates_overview#base">Spice base template</h2>
<p class='summary-text'>
This is the most rudimentary template group. It provides a minimal container template which is intended to be used when your Spice requires highly customized mark-up. **Using this template should be a last resort if other templates don't suffice.**
</p>
<p class='summary-text'>Example use:<a href="https://duckduckgo.com/?=define+indelible"> "define indelible"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/dictionary/definition/dictionary_definition.js">(code)</a></p>
<a class="summary-text" href="https://duckduckgo.com/?q=bbc+schedule"><img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/define_indelible.png'></img>
-->
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

#### Default templates used in the 'base' group:

- [base_item](#baseitem)
- [base_detail](#basedetail)

In order for these templates to display correctly, you need to ensure that each of the template's features you are using, are defined in your `data` object. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example uses of the 'base' template group

- ["gandhi quote"](https://duckduckgo.com/?q=gandhi+quote) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/brainy_quote/brainy_quote.js))
    ![DuckDuckGo search for "gandhi quote"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/gandhi_quote.png)

- ["cpan App::cpanminus"](https://duckduckgo.com/?q=cpan+App::cpanminus) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js))
    ![DuckDuckGo search for "cpan App::cpanminus"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/cpan_app_cpanminus.png)

- ["define indelible"](https://duckduckgo.com/?q=define+indelible) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dictionary/definition/dictionary_definition.js))
    ![DuckDuckGo search for "define indelible"](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/template_groups/define_indelible.png)


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
<!-- 
<h2 class="summary" moreat="spice_templates_overview#record">Spice record template</h2>
<p class="summary-text">A special template that is ideal for key-value data. It generates a table where each row contains a key and value.</p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=cpan+Moose"> "metacpan Moose"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/record.png'></img>
</span>
-->
## record

A special template that is ideal for key-value data. It generates a `<table>` where each row contains a key and value.

**\*\*Note:** This template **requires** that your `data` object has a `record_data` property, which should contain the key-value data to be displayed. All the properties of the `record_data` object will be used as the keys for the table. However, if you want to specify exactly which properties of the `record_data` object should be displayed, an optional `record_keys` property can be defined. It should be an array of *strings*, indicating the names of the **keys** to be included in the `<table>`.  An optional property called `rowHighlight` can be added to `options` to turn on alternating row highlighting. 

For example this is how your Spice code should look when using the **record** template:

'''javascript
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
'''
### Available Features

*none*

### Template Diagram

![record template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/record.png)

### Template groups using the "record" template:

- *none by default*

### Example usage of the "record" template:

- [UrbanDictionary](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/urban_dictionary/urban_dictionary.js)
- [MetaCpan](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js)
- [CodeSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/code_search/code_search.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#iconitem">Spice icon item template</h2>
<p class="summary-text">A tile template used to display basic text content with an icon</p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=cpan+Moose"> "alternative to vim"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/icon.png'></img>
</span>
-->

## icon_item

### Available Features

- icon
- title
- sub-title [optional]
- description
- footer [optional] *sub-template*

### Template Diagram

![icon template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/icon.png)

### Template groups using the "icon_item" template:

- [icon](#icon)

### Example usage of the "icon" template:

- [AlternativeTo](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#textitem">Spice text item template</h2>
<p class="summary-text">A basic tile used to display text-only content</p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=github+duckduckgo"> "github duckduckgo"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/text_item.png'></img>
</span>
-->

## text_item

### Available Features

- url [optional]
- title
- subtitle
- description
- footer [optional] *sub-template*

### Template Diagram

![text_item template ](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/text_item.png)

### Template groups using the "text_item" template:

- [text](#text)

### Example usage of the "text_item" template:

- [GitHub](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js)
- [RubyGems](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/ruby_gems/ruby_gems.js)
- [RedditSearch](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#textdetail">Spice text detail template</h2>
<p class="summary-text">A detail view used to display basic text-only content</p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=synonym+of+eye"> "synonym of eye"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/thesaurus/thesaurus.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/text_detail.png'></img>
</span>
-->

## text_detail

### Available Features

- title_content [optional] *sub-template*
- title [optional, replaces `title_content`]
- content [optional] *sub-template*

### Template Diagram

![text_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/text_detail.png)

### Template groups using the "text_detail" template:

- [text](#text)

### Example usage of the "text_detail" template:

- [Rhymes](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js)
- [Thesaurus](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/thesaurus/thesaurus.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#basicimageitem">Spice basic image item template</h2>
<p class="summary-text"></p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=bbc+schedule"> "BBC schedule"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_image_item.png'></img>
</span>
-->

## basic_image_item

### Available Features

- link [optional]
- image
- title
- description [optional]
- rating [optional]
- ratingText [optional]

### Template Diagram

![basic_image_item template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_image_item.png)

### Template groups using the "basic_image_item" template:

- [info](#info)
- [media](#media)

### Example usage of the "basic_image_item" template:

- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)
- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#productsitem">Spice products item template</h2>
<p class="summary-text"></p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=star+wars+lego"> "star wars lego"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_item.png'></img>
</span>
-->

## products_item

### Available Features

- url [optional]
- img
- title
- price
- brand [optional]
- rating [optional]
- reviewCount [optional]

### Template Diagram

![products_item template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_item.png)

### Template groups using the "products_item" template:

- [products](#products)

### Example usage of the "products_item" template:

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [CouponMountain](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#productsdetail">Spice products detail template</h2>
<p class="summary-text"></p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=star+wars+lego"> "star wars lego"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_detail.png'></img>
</span>
-->

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

### Template Diagram

![products_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_detail.png)

### Template groups using the "products_detail" template:

- [products](#products)
- [media](#media)
- [icon](#icon)

### Example usage of the "products_detail" template:

- [Amazon](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js)
- [CouponMountain](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)
- [Octopart](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#productsitemdetail"></h2>
<p class="summary-text"></p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=the+hobbit"> "the hobbit" - see products detail view</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_item_detail.png'></img></a>
</span>
-->

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

### Template Diagram

![products_item_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/products_item_detail.png)

### Template groups using the "products_item_detail" template:

- [products](#products)
- [media](#media)
- [icon](#icon)

### Example usage of the "products_item_detail" template:

- [BBC](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js)
- [Movie](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js)
- [CouponMountain](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#basicinfodetail">Spice basic info detail template</h2>
<p class="summary-text"></p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=mix+a+tom+colins"> "mix a tom colins"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/drinks/drinks.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_info_detail_w_aux.png'></img>
</span>
-->

## basic_info_detail

### Available Features

- image [optional]
- title [optional]
- description
- content [optional, replaces `description`] *sub-template*
- aux [optional] *sub-template*

### Template Diagram

![basic_info_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_info_detail.png)

### Example with Auxiliary Information Box:

![basic_info_detail_w_aux template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/basic_info_detail_w_aux.png)

### Template groups using the "basic_info_detail" template:

- [info](#info)

### Example usage of the "basic_info_detail" template:

- [Bitcoin](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js)
- [Gravatar](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js)
- [Drinks](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/drinks/drinks.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#baseitem">Spice base item template</h2>
<p class="summary-text"></p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=aa+102"> "aa102"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/airlines/airlines.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_item_complex.png'></img>
</span>
-->

## base_item

### Available Features

- url [optional]
- content *sub-template*

### Template Diagram

![base_item template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_item.png)

### Complex Example

![base_item template (complex example)](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_item_complex.png)

### Template groups using the "base_item" template:

- [base](#base)

### Example usage of the "base_item" template:

- [GithubJobs](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github_jobs/github_jobs.js)
- [Airlines](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/airlines/airlines.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#basedetail">Spice base detail template</h2>
<p class="summary-text"></p>
<span class="summary-text">
<p>Template Diagram:<a href="https://duckduckgo.com/?q=flash+version"> "flash version"</a><a href="https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/flash_version/flash_version.js"> (code)</a></p>
<img src='https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_detail.png'></img></a>
</span>
-->

## base_detail

### Available Features

- content *string* OR *sub-template*

### Template Diagram

![base_detail template](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_detail.png)

### Complex Example

![base_detail template (complex example)](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/diagrams/base_detail_complex.png)

### Template groups using the "base_detail" template:

- [base](#base)

### Example usage of the "base_detail" template:

- [FlashVersion](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/flash_version/flash_version.js)
- [NPM](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/npm/npm.js)
- [XKCD](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/xkcd/xkcd.js)

------
<!-- 
<h2 class="summary" moreat="spice_templates_overview#tile-variants">Spice tile variants</h2>
<span class="summary-text">
<ul>
	<li><a href="https://duck.co/duckduckhack/spice_templates_overview#poster">poster </a> Tall and thin, like a movie poster </li>
	<li><a href="https://duck.co/duckduckhack/spice_templates_overview#narrow">narrow </a> Narrower tile width, normal height </li>
	<li><a href="https://duck.co/duckduckhack/spice_templates_overview#poster">wide </a> Increased width, normal height  </li>
	<li><a href="https://duck.co/duckduckhack/spice_templates_overview#poster">xwide </a> Super wide, normal height </li>
	<li><a href="https://duck.co/duckduckhack/spice_templates_overview#poster">video </a> Shorter height, increased width </li>
</ul>
</span>
-->


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
