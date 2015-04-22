# Spice Templates Overview

<<<<<<< HEAD
When your Instant Answer returns its awesome and delightful result(s), the information is rendered at the top of the DuckDuckGo search results page. The way your results appear and behave is decided by the Spice templates you choose.
=======
## Spice Template Summary
>>>>>>> spice-templates-updates

![DuckDuckGo search for "garlic steak recipes"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fgarlic_steak_recipes.png&f=1)

## Why Templates Are Great

Templates save a lot of work: they allow contributors to focus on great results. Many Instant Answer frontends can be created entirely by setting various display options and item data, with little or no HTML/CSS coding.

Additionally, Instant Answers that use templates are automatically compatible with future design improvements, with zero extra work.

## How Templates Work

Templates are handlebars files which render in the context of **one item** returned by the Instant Answer.

The Spice framework provides you with a wide choice of templates to use. The built-in templates' options, variables, and [variants](https://duck.co/duckduckhack/spice_templates_reference#tile-variants) are documented in the [Spice Templates Reference](https://duck.co/duckduckhack/spice_templates_reference) section.

### Specifying `item` and `detail` Templates

Spice Instant Answers can return either a **single result** or **multiple results**. To provide the best experience, these two cases can be displayed with different templates.

On the [Spice frontend](https://duck.co/duckduckhack/spice_displaying) you can specify two separate templates:

- `item` template
- `detail` template

Below is an example of multiple results being returned. Each result is displayed using the template specified for `item`: 

![DuckDuckGo search for "seafood maui"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fseafood_maui.png&f=1)

Below is an example of the same Instant Answer returning a single result. This uses the template specified for `detail`:

![DuckDuckGo search for "longhi's maui"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Flonghis_maui.png&f=1)

### Specifying an `item_detail` Template

Additionally, when displaying multiple results, you might sometimes allow users to drill down without leaving the page. For that, you might optionally specify a third template:

- `item_detail` template

This feature is used by fewer Instant Answers, but it can be very useful. Below is an example of what happens after clicking a particular product. This shows more detail by displaying the template specified in `item_detail`:

![DuckDuckGo search for "amazon pogs"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Famazon_pogs.png&f=1)

### When Each Template Is Shown

The Spice framework automatically chooses which template to display based on how many results there are to show and user behavior. Here is the default logic for showing templates:

```
          Instant Answer result      
                   +                     
                   |  
 multiple results  |  single result      
                   |  
         +---------+----------+          
         |                    |          
         |                    |   
         |                    |          
+--------v--------+  +--------v---------+
|                 |  |                  |
|      item       |  |      detail      |
|                 |  |                  |
+-------+---------+  +------------------+                              
        |                                
        | click an item                   
        |                                
+-------v---------+                      
|                 |                      
|   item_detail   |                      
|  (if specified) |
|                 |                     
+-----------------+                      

```

Of course, you can specify template options to modify this; for example, you may want to prevent a particular template from appearing. For example, you might set `detail: false` to make sure your Instant Answer always displays results with the `item` template.

## Template Groups (required)

[Template groups](#template-groups) are preset properties for `template` and its `options` that work well together. In most cases at least one group will be a good fit for your Instant Answer.

**We strongly recommend using a template group in your Instant Answer.** Of course, if you cannot use an available template for your Instant Answer, definitely let us know. E-mail us at open@duckduckgo.com and we'll help you. We may find that a custom template is necessary, and we'll work with you to create an awesome one. (Who knows, your idea may inspire the next official template group!)

### How Template Groups Work

Setting a template group automatically sets the `item` and `detail` templates. Some template groups also set an `item_detail` template and a few default `options`. 

You can easily customize the appearance of the template group by overriding the default `options` in your Spice frontend code. Of course, the appearance will also be affected by which data is returned with each item.

### Picking a Template Group

The best template group for your instant answer depends on what your Instant Answer is returning. Below are a few suggestions to help you narrow down your options.

A quick way to get a feel for the different template groups is to [browse the Instant Answer directory](https://duck.co/ia). You can filter by the template group used on the right of the page.

#### My Spice returns "things" where visuals are important 

The [Media](#media-template-group) template group works well when an image is a significant part of the display of an item, as might be a title and a rating. 

Examples that make a great fit for `media` include:

- TV shows/[Movies](https://duckduckgo.com/?q=currently+in+theaters)
- Games
- [Courses](https://duckduckgo.com/?q=computer+science+online+course)

#### My Spice returns detailed "lookup" information

The [Info](#info-template-group) template group is designed for Instant Answers that feature in-depth information about one item. It also provides an auxiliary section to display further detail in table or list format. 

Examples include:

- [Recipes](https://duckduckgo.com/?q=how+to+mix+a+tom+collins&ia=recipes)
- [Cards](https://duckduckgo.com/?q=mtg+Boros+Reckoner&ia=magicthegathering)
- [Books](https://duckduckgo.com/?q=book+reviews+moonwalking+with+einstein&ia=books)
- [Bands](https://duckduckgo.com/?q=weezer+band)
- [Addresses](https://duckduckgo.com/?q=1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa)
- [Characters](https://duckduckgo.com/?q=bulbasaur+pokemon)

The [List](#list-template-group) template group works well for lookups that don't need an image; this group is excellent for displaying attributes in just a list or table format. Take a look at the following example:

- [WhoIs](https://duckduckgo.com/?q=whois+google.com)

#### My Spice results are mainly text, with a possible icon or logo

The [Text](#text-template-group) and [Icon](#icon-template-group) template groups are simple templates for presenting text results. They both share the same `item` template, while the Icon group's `detail` template is better suited to displaying an icon image. 

These results fit this format well:

- [Software](https://duckduckgo.com/?q=alternative+to+notepad&ia=software)
- [Code blocks](https://duckduckgo.com/?q=Fizz+Buzz+in+C&ia=codesnippet)
- [Jobs](https://duckduckgo.com/?q=perl+jobs+in+san+francisco&ia=jobs)
- [Records](https://duckduckgo.com/?q=bugid+234&ia=launchpad)
- [Simple answers](https://duckduckgo.com/?q=namecheap+http%3A%2F%2Finstantanswerparty.com&ia=domain)
- [Long blocks of text](https://duckduckgo.com/?q=baconipsum+4&ia=baconipsum)

#### My Spice returns products with prices, ratings, and brands/authors/artists

The [Products](#product-template-group) is great for items characterized by a price, brand, and rating. This is a good template group where images are important. 

Examples of results that work well with the Products template group include:

- [Magazines issues](https://duckduckgo.com/?q=newint&ia=magazines)
- [Parts](https://duckduckgo.com/?q=ne555+specs&ia=parts)
- [Apps](https://duckduckgo.com/?q=tiny+piano+for+iphone&ia=apps)
- [Events](https://duckduckgo.com/?q=live+show+weezer&ia=concerts)
- [Books](https://duckduckgo.com/?q=amazon+ray+bradbury&ia=products)
- [Physical products](https://duckduckgo.com/?q=amazon+ninja+costume&ia=products)

#### My Spice returns location-based results

The [Places](#places-template-group) template group is perfect for results where location is an important aspect. This template group displays single and multiple items on a map.

Results that would make a good fit for the Places template group include:

- [Parking](https://duckduckgo.com/?q=parking+in+philadelphia&ia=parking)
- [Local businesses](https://duckduckgo.com/?q=restaurant+in+laguna+beach)
- Hiking trails
- Historical sites
- Surf spots
- Shark GPS locations

#### My Spice is amazingly unique and existing template groups won't meet my needs

We encourage you to think hard about using an existing template group. For example, many `detail` templates accept custom handlebars sub-templates. Additionally, many template features can be turned off. 

If working within existing template groups feels too constraining, we're happy to help you figure out how your vision could be accomplished using existing templates. E-mail us at open@duckduckgo.com and we'll work with you to find the best way to express your idea.

In this context, the [Base](#base-template-group) template group is a minimal container template that accepts totally custom markup. Because of this, the Base template group is at a disadvantage because of the amount of work up front, and more involved maintenance over time.

Examples of Instant Answers that do not fit into any template groups:

- [Ducksay](https://duckduckgo.com/?q=ducksay+quack!&ia=ducksay)
- [Flight itineraries](https://duckduckgo.com/?q=Jetblue+Boston+to+Los+Angeles&ia=route)
- [Site functionality](https://duckduckgo.com/?q=is+reddit.com+working%3F&ia=answer)
- [Nutrition facts](https://duck.co/ia/view/nutrition)
- [Webcomics](https://duck.co/ia/view/xkcd_display)

------

## Template Groups

This page will help you understand what each template group looks like and what content works best for it. Each group is accompanied by several examples of live Spice Instant Answers using that group. Each template is accompanied by similar examples, links to code and diagrams indicating what features exist for the template and what the template layout looks like.

There are several template groups to choose from:

- [Text](#text-template-group)
- [Info](#info-template-group)
- [Products](#products-template-group)
- [Media](#media-template-group)
- [Icon](#icon-template-group)
- [Base](#base-template-group)

<!-- /summary -->

### A Note on Default Template Options

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

## Important Notes

1. Before using these templates in your code, please familiarize yourself with the [Spice Displaying](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_displaying.md) document to understand the **proper usage of both the `templates` block and the `options` block**.

2. Specifically, in order for each of the templates to display correctly, you need to ensure that each of the template's features, which you are using, **are defined in your `data` object**. Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

Understanding these is crucial to implementing Spice templates properly and effectively.

------

## Text Template Group

This template group is best used for results which are mostly text, where any images are icons or small logos. This template offers a title, description and footer.

### Usage

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

- [`text_item`](https://duck.co/duckduckhack/spice_templates_reference#textitem-template)
- [`text_detail`](https://duck.co/duckduckhack/spice_templates_reference#textdetail-template)

See the **[important notes](#important-notes)** before implementing this template group.

### Example uses of the 'text' template group

- ["github duckduckgo"](https://duckduckgo.com/?q=github+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/github/github.js))
    ![DuckDuckGo search for "github duckduckgo"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgithub_duckduckgo.png&f=1)

- ["what rhymes with awesome"](https://duckduckgo.com/?q=what+rhymes+with+awesome) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rhymes/rhymes.js))
    ![DuckDuckGo search for "what rhymes with awesome"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhat_rhymes_with_awesome.png&f=1)

- ["reddit duckduckgo"](https://duckduckgo.com/?q=reddit+duckduckgo) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js))
    ![DuckDuckGo search for "reddit duckduckgo"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Freddit_duckduckgo.png&f=1)


------

## Info Template Group

The `info` template group is designed for Instant Answers that feature in-depth information about one item. This includes an image, title, and a description or arbitrary content. It also provides an auxiliary section to display further detail in table or list format (to the right).

### Usage

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

- [`basic_image_item`](https://duck.co/duckduckhack/spice_templates_reference#basicimageitem-template)
- [`basic_info_detail`](https://duck.co/duckduckhack/spice_templates_reference#basicinfodetail-template)

See the **[important notes](#important-notes)** before implementing this template group.

### Example uses of the 'info' template group

- ["green day band"](https://duckduckgo.com/?q=green+day+band) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/lastfm/artist/lastfm_artist.js))
    ![DuckDuckGo search for "green day band"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgreen_day_band.png&f=1)

- ["bitcoin price"](https://duckduckgo.com/?q=bitcoin+price) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bitcoin/bitcoin.js))
    ![DuckDuckGo search for "bitcoin price"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbitcoin_price.png&f=1)

- ["gravatar matt"](https://duckduckgo.com/?q=gravatar+matt) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/gravatar/gravatar.js))
    ![DuckDuckGo search for "gravatar matt"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgravatar_matt.png&f=1)


------

## Products Template Group

Best used to showcase products with an image, rating, review, brand and/or price. An optional `buy` sub-template can be used to provide a compelling call-to-action (i.e. button).

### Usage

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

- [`products_item`](https://duck.co/duckduckhack/spice_templates_reference#productsitem-template)
- [`products_detail`](https://duck.co/duckduckhack/spice_templates_reference#productsdetail-template)
- [`products_item_detail`](https://duck.co/duckduckhack/spice_templates_reference#productsitemdetail-template)
- [`base_detail`](https://duck.co/duckduckhack/spice_templates_reference#basedetail-template)

See the **[important notes](#important-notes)** before implementing this template group.

### Example uses of the 'products' template group

- ["buy batman lego"](https://duckduckgo.com/?q=buy+batman+lego) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/amazon/amazon.js))
    ![DuckDuckGo search for "buy batman lego"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbuy_batman_lego.png&f=1)

- ["flight tracking apps"](https://duckduckgo.com/?q=flight+tracking+apps) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js))
    ![DuckDuckGo search for "flight tracking apps"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fflight_tracking_apps.png&f=1)

- ["octopart 1770019-2"](https://duckduckgo.com/?q=octopart%201770019-2) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/octopart/octopart.js))
    ![DuckDuckGo search for "octopart 1770019-2"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Foctopart_1770019-2.png&f=1)


------

## Media Template Group

The `media` template group works well when an image is a significant part of the display of an item. Items can also have a title and a rating. 

The `item` template is essentially a simplified version of the Products template group. It also uses the same `detail` template as the Products template group.

### Usage

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

- [`basic_image_item`](https://duck.co/duckduckhack/spice_templates_reference#basicimageitem-template)
- [`products_detail`](https://duck.co/duckduckhack/spice_templates_reference#productsdetail-template)
- [`products_item_detail`](https://duck.co/duckduckhack/spice_templates_reference#productsitemdetail-template)
- [`base_detail`](https://duck.co/duckduckhack/spice_templates_reference#basedetail-template)

See the **[important notes](#important-notes)** before implementing this template group.

### Example uses of the 'media' template group

- ["lord of the rings movie"](https://duckduckgo.com/?q=lord+of+the+rings+movie) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/movie/movie.js))
    ![DuckDuckGo search for "lord of the rings movie"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Flord_of_the_rings_movie.png&f=1)

- ["movies"](https://duckduckgo.com/?q=movies) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/in_theaters/in_theaters.js))
    ![DuckDuckGo search for "movies"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fmovies.png&f=1)

- ["BBC schedule"](https://duckduckgo.com/?q=BBC+schedule) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/bbc/bbc.js))
    ![DuckDuckGo search for "BBC schedule"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fbbc_schedule.png&f=1)


------

## Icon Template Group

This template is similar to the **text** group, since it uses the same `item` template. However, the detail view is better suited to displaying an icon image.

### Usage

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

- [`text_item`](https://duck.co/duckduckhack/spice_templates_reference#textitem-template)
- [`products_detail`](https://duck.co/duckduckhack/spice_templates_reference#productsdetail-template)
- [`products_item_detail`](https://duck.co/duckduckhack/spice_templates_reference#productsitemdetail-template)

See the **[important notes](#important-notes)** before implementing this template group.

### Example uses of the 'icon' template group

- ["alternative to photoshop"](https://duckduckgo.com/?q=alternative+to+photoshop) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js))
    ![DuckDuckGo search for "alternative to photoshop"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Falternative_to_photoshop.png&f=1)


------
## Places Template Group

This template group is ideal for displaying results where location is an important factor to the searcher. The Places template group makes it easy for searchers to view a map showing all results, or highlighting a particular item without leaving the search page.

### Usage

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

- [`places_item`](https://duck.co/duckduckhack/spice_templates_reference#placesitem-template)
- [`places_detail`](https://duck.co/duckduckhack/spice_templates_reference#placesdetail-template)

#### Places Model and View

The Places template group works together with the Places **model** and Places **view**. The Places model and view enable special map functionality and behaviors that make instant answers using Places valuable and delightful.

The model and view are specified alongside the template group property when you call `Spice.add()`. You can see how this is done under the [Model and View section](https://duck.co/duckduckhack/spice_displaying#views) of the [Spice Displaying](https://duck.co/duckduckhack/spice_displaying) page.

To work correctly, the places model requires **additional values** passed that do not appear directly in the templates. Make sure that each item includes the [attributes required by the places model](https://duck.co/duckduckhack/spice_displaying#place-attributes). Generally these are set by your `normalize` function if they do not already exist in your `api_result`.

### Example use of the 'places' template group

- ["parking panda"](https://duckduckgo.com/?q=parking+in+philadelphia) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/parking/parking.js))
    ![DuckDuckGo search for "parking in philadelphia"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fparking_panda.png&f=1)

------

## List Template Group

The List template group was designed for displaying in-depth attributes of one item. These attributes can be displayed as either a bulleted list of properties, *or* a table of key-value pairs. 

Multiple items are displayed using the same `text_item` template used by Text and Icon template groups. As a result, this template group is mainly useful for instant answers designed to **return a single item** with detailed properties.

### Usage

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

- [`text_item`](https://duck.co/duckduckhack/spice_templates_reference#textitem-template)
- [`list_detail`](https://duck.co/duckduckhack/spice_templates_reference#listdetail-template)

See the **[important notes](#important-notes)** before implementing this template group.

### Example use of the 'list' template group

- ["whois"](https://duckduckgo.com/?q=whois+mozilla.org) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/whois/whois.js))
	![DuckDuckGo search for "whois mozilla.org"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fwhois_results.png&f=1)

------

## Base Template Group

This is the most rudimentary template group. It provides a minimal container template which is intended to be used when your Spice requires highly customized mark-up. **Using this template should be a last resort if other templates don't suffice.**

### Usage

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

- [`base_item`](https://duck.co/duckduckhack/spice_templates_reference#baseitem-template)
- [`base_detail`](https://duck.co/duckduckhack/spice_templates_reference#basedetail-template)

See the **[important notes](#important-notes)** before implementing this template group.

### Example uses of the 'base' template group

- ["gandhi quote"](https://duckduckgo.com/?q=gandhi+quote) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/brainy_quote/brainy_quote.js))
    ![DuckDuckGo search for "gandhi quote"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fgandhi_quote.png&f=1)

- ["cpan App::cpanminus"](https://duckduckgo.com/?q=cpan+App::cpanminus) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js))
    ![DuckDuckGo search for "cpan App::cpanminus"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fcpan_app_cpanminus.png&f=1)

- ["define indelible"](https://duckduckgo.com/?q=define+indelible) ([code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dictionary/definition/dictionary_definition.js))
    ![DuckDuckGo search for "define indelible"](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftemplate_groups%2Fdefine_indelible.png&f=1)
