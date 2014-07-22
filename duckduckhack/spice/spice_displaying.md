# Adding Your Spice to the AnswerBar
<!--
<h2 class='summary' moreat='spice_displaying'>Spice adding to the AnswerBar</h2>
<div markdown="1" class="summary-text">
`Spice.add()` is the most important Spice function and it's used to add your Spice to the AnswerBar. However, this function is capable of much more than simply showing your Spice result. For example, it can also help you ensure the relevancy and order of results and it enables you to configure the templates your Spice will use. This document provides an in-depth overview of how you can use `Spice.add()` to make sure your instant answer is excellent.
</div>
-->
`Spice.add()` is the most important Spice function and it's used to add your Spice to the AnswerBar. However, this function is capable of much more than simply showing your Spice result. For example, it can also help you ensure the relevancy and order of results and it enables you to configure the templates your Spice will use. This document provides an in-depth overview of how you can use `Spice.add()` to make sure your instant answer is excellent.

## Spice.add Properties Overview

```javascript
Spice.add({

    id: String,
    name: String,
    data: Object,

    meta: {

        hidden: boolean,
        searchTerm: String,
        itemType: String,

        primaryText: String,
        secondaryText: String,

        sourceName: String,
        sourceLogo: String,
        sourceUrl: String (url),
        sourceIcon: Boolean,
        sourceIconUrl: String (url),
    },

    normalize: Function,

    relevancy: {
        type: String,
        skip_words: [, String],
        primary: [, Object],
        dup: String,
    },

    templates: {
        group: String,

        item: String|Function,
        item_custom: String|Function,
        item_mobile: String|Function,

        detail: String|Function,
        detail_custom: String|Function,
        detail_mobile: String|Function,
        item_detail: String|Function,

        options: Object
    },

    sort_fields: Object,
    sort_default: Object,

    onItemSelect: Function,
    onItemUnselect: Function,
    onShow: Function,
    onHide: Function

  });
```

# Essential Properties
<!--
<h2 class='summary' moreat='spice_displaying'>Spice add function</h2>
<div markdown="1" class="summary-text">
Used to add your Spice to the AnswerBar and has the following required properties:
- ['id'](http://duck.co/duckduckhack/spice_displaying#id-codestringcode-required) A unique identifier for your Spice. The `id` should match the name of your callback function
- ['name'](http://duck.co/duckduckhack/spice_displaying#name-codestringcode-required) The name that will be used for your Spice's AnswerBar tab
- ['data'](http://duck.co/duckduckhack/spice_displaying#data-codestringcode-required) The object containing the data to be used by your templates

Other properties and fuctions of `spice.add()`
- [`meta`](http://duck.co/duckduckhack/spice_displaying#instant-answer-metadata) Used to define elements of the **MetaBar** including the "More at" link
- [`normalize`](http://duck.co/duckduckhack/spice_displaying#data-normalization) This allows you to normalize the `data` object (or array of items) before it is passed on to the template
- [`templates`](http://duck.co/duckduckhack/spice_displaying#templates) Used to specify the template group and all other templates that are being used
- ['relevancy'](http://duck.co/duckduckhack/spice_displaying#relevancy) Used to ensure the relevancy of your Spice's result
</div>
-->
### id `string` [required]

A unique identifier for your Spice. The `id` should match the name of your callback function. For example, if your callback function is named `ddg_spice_name`, your `id` should be `spice_name`.

### name `string` [required]

The name that will be used for your Spice's AnswerBar tab. The Spice system will determine the final tab name, but it's best to provide a category or topic that describes the kind of information your Spice provides. Here are some examples:

<table>
    <thead>
        <tr>
            <th>Spice IA</th>
            <th><pre>name</pre></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>GitHub</td>
            <td>'Software'</td>
        </tr>
        <tr>
            <td>Last.fm</td>
            <td>'Music'</td>
        </tr>
        <tr>
            <td>HackerNews</td>
            <td>'News'</td>
        </tr>
        <tr>
            <td>Twitter</td>
            <td>'Social'</td>
        </tr>
        <tr>
            <td>Amazon</td>
            <td>'Products'</td>
        </tr>
    </tbody>
</table>

### data `object` [required]

The object containing the data to be used by your templates. In most cases, it is best to pass along `api_result` to `data`, so that all of your API response is accessible to your templates.


# Instant Answer Metadata

The following options are used to define elements of the **MetaBar** including the "More at" link. They are all properties of the `meta: {}` property.

- ### searchTerm `string`

    The key term or subject in the search query. The `searchTerm` is used to describe the `itemType` and it can be determined by removing any skip words from the original query. For example, searching "coupons for electronics", will display the phrase "Showing 15 **electronics** Coupons" in the MetaBar. In this case, the word "electronics" is the `searchTerm`.

- ### itemType `string`

    The type of item being shown (e.g., Videos, Images, Recipes). `itemType` is used by the MetaBar to describe the current result. Using the previous example, in the phrase, "Showing 15 **electronics** Coupons", the word "Coupons" is the `itemType`.

------

- ### primaryText `string`

    If defined, this text will replace the MetaBar's "Showing **n** Items" text. For example, the Forecast Spice uses this to display "Weather for New York, NY" in the MetaBar.

- ### secondaryText `string`

    This is an optional text label that will be displayed to the left of the "More at" link. For example, the Forecast Spice uses this to indicate the current temperature unit being used: "Temperatures in F&deg;".

------

- ### sourceName `string` [required]

    The name of the source as it should be shown in the "More at" link. For example, in "More at Quixey", "Quixey" is the `sourceName`.

- ### sourceLogo `string` (url)

    If defined, the image provided will replace the `sourceName` with a logo. Generally this should not be necessary, but in rare cases, API providers require that a specific image be used to represent their brand and so this can be used.

- ### sourceUrl `string` (url) [required]

    The URL to follow when the "More at" link is clicked. This value will become the `href` of the "More at" link. It is preferred that **https\:\/\/** be used when possible.

- ### sourceIcon `boolean`

    A boolean flag that determines if a favicon should be shown for the "More at" link. When a `sourceUrl` is given, this will default to `true`. This should only be set to `false` when no favicon exists for the `sourceUrl` domain.

- ### sourceIconUrl `string` (url)

    If the `sourceUrl` domain has no favicon (or if a different favicon is preferred), the link provided here will be used as the source for the "More at" link's favicon. This will replace any favicons from the `sourceUrl` domain.


# Data Normalization

- ### normalize `function` [required depending on template and data]

    This allows you to normalize the `data` object (or array of items) before it is passed on to the template, by adding or modifying properties that are used by your templates. When dealing with multiple items, the normalize function iterates over each `item` so they can be individually normalized.

    This function uses jQuery's `$.extend()` method, so it will modify your `data` object by adding any returned properties that don't already exist, or simply overwrite the ones that do, i.e., a shallow copy is made

    If you are using a built-in template (e.g., **basic_image_item**), it expects that certain properties will be present (e.g `title`, `image`) and so the normalized function should be used to provide those or normalize their values if the already exist in your `api_result`.

    For example, if you have a `data` object that looks like this:

    ```javascript
    // original data object from API
    {
        heading: "My awesome title",
        image:   "http://website.com/image.png"
    }
    ```

    You will likely want to use the `heading` property as the `title` for the **basic_image_item** template, so your `normalize` function would need to look like this:

    ```javascript
    normalize: function(item){
        return {
            title: item.heading
        };
    }
    ```

    This would result in your `data` object looking like this once it gets passed along to the template:

    ```javascript
    // normalized data object
    {
        heading: "My awesome title",
        image:   "http://website.com/image.png",
        title:   "My awesome title"
    }
    ```

    Now, your object has all the required properties for the **basic_image_item** template and everything will be displayed as expected.

    ---

    #### exactMatch `boolean` & boost `boolean`

    Two special properties, `exactMatch` and `boost`, can also be set for the current item to add them to the list of exact matches or boosted items. When the tile view displays, the **exact match** items will come **first**, followed by the **boosted** items and then the rest of the items.

    Example:

    ```javascript
    normalize: function(item) {
        if (item.name === DDG.get_query()){
            item.exactMatch = true;
        } else if (item.developer.name === DDG.get_query()) {
            item.boost = true;
        }

        return { ... }
    }
    ```


# Templates

A `templates: {}` property should be used to specify the template group and all other templates that are being used. Template options can also be provided to enable or disable features depending on the chosen template group.

- ### group `string` [required unless `item` or `detail` is specified]

    Used to specify the base template (layout) to be used. Each template `group` is composed of several features. The various options for this will be explained later in the [template overview](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_templates_overview.md).

    This will tell the template system that the templates belonging to the given group will be used for the `item`, `detail`, etc. **unless otherwise specified**.

    For example, `group: 'info'` will implicitly set:

    ```javascript
    item: 'basic_item',
    item_detail: 'basic_info_item_detail',
    detail: 'basic_info_detail'
    ```

- ### item `string|function` [required for **multiple item** results when no `group` is specified]

    The template to be used for the body of each tile in a tile view.

    **\*\*Note:** The `item` template is only used when your Spice instant answer returns multiple items (like the recipe or app instant answers), meaning the object given to `data` is an *`array`* with more than 1 elements.

    - Generally, a *`string`* is provided to indicate the name of the built-in Spice template to be used, e.g., "products_item"

    - Alternatively, a **function** can be provided when a custom template is necessary, e.g., `Spice.quixey.item`, which references the file "**/share/spice/quixey/item.handlebars**".

- ### item_mobile `string|function`

    An alternative `item` template to be used when displaying on smaller screens, such as mobile and hand-held devices.

------

- ### detail `string|function` [required for **single item** results when no `group` is specified]

    The template to be used for the detail area.

    *For multiple items*, the detail area will be located below the tiles, and will display when a tile is clicked. If your Spice returns multiple items, the `detail` template is **optional**.

    *For a single item*, the detail area will be right below the AnswerBar and will display instantly. If your Spice always returns a single item, only a `detail` template is **required**.

    **\*\*Note:** The `detail` templates is **optional for a tile view** and should only be used to provide additional information for each tile.

- ### detail_mobile `string|function`

    An alternative `detail` template to be used when displaying on smaller screens, such as mobile and hand-held devices.

------

- ### item_detail `string|function`

    An alternative `detail` template to be used when a tile view contains a **single** tile.

------

- ### options `object`

    Allows you to explicitly disable or enable features of a template, as well as specify any sub-templates when applicable (e.g., the `content` feature of the `'info'` template). Depending on the templates being used, the features will vary. For example, the `'info'` template doesn't have a `brand` feature, so attempting to enable or disable that feature will have no effect.

    ### Tile Variants

    Sometimes the default height or width of the tile might not be perfect for your Spice result. If you need a wider or perhaps taller tile, you can specify a tile `variant` to adjust their dimensions. A list of the tile variants availble can be found in the [Templates Overview](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_templates_overview.md#tile-variants) document

    **\*\*Note:** If you intend to use a feature that is disabled by default, it **must** be enabled in the `options` for it to display. Even if the property exists in the `data` object, the template system will ignore it if the feature is disabled. For example:

    ```javascript
    normalize: function(item){
        return {
            // these won't work! 
            rating: item.customerRating,
            brand: item.brandname
        };
    },
    templates: {
        group: 'products_simple'
    }
    ```

    Will ***not*** display the `rating` or `brand` as they are **disabled** by default in the `products_simple` group. Only once they are enabled in an `options` object will they work:

    ```javascript
    normalize: function(item){
        return {
            // now they'll show, because they're enabled
            rating: item.customerRating,
            brand: item.brandname
        };
    },
    templates: {
        group: 'products_simple',
        options: {
            rating: true,
            brand: true
        }
    }
    ```

# Relevancy

If you want to ensure the relevancy of your Spice's result (usually when dealing with multiple items), the `relevancy: {}` property can be used to ensure the relevancy of each individual item. It can also be used to de-duplicate the returned items if desired.

In most cases you will only need to specify relevancy properties for the, **primary** relevancy block. If your Spice is capable of dealing with different types of queries though, where different relevancy checks are necessary, you can supply additional relevancy blocks. For example, the Quixey (Apps) Spice handles two distinct types of app searches, being **categorical** searches, such as "social networking apps", or more specific, named searches such as "free angry birds apps". When dealing with **categorical** searches, the name of the app doesn't need to be checked against the query for relevancy. However, the app's category does need to be checked and so two separate relevancy blocks, `primary` and `category`, are used to define the different relevancy constraints.

### Relevancy Blocks

A relevancy block is comprised of an array of simple objects. For each object, the properties are used to indicate certain constraints. The concept of a relevancy block is best explained with an example:

```javascript
// First we provide the name for the relevancy block, "primary"
primary: [

    { required: 'icon_url' },
    // "required" means the item must have a defined property matching the
    // given name, in this case and "icon_url" must be defined for each Quixey
    // item
    //
    // Note: "required" only ensures the presence of a property. It does NOT
    // perform a relevancy check

    { key: 'name', strict: true },
    // "key" indicates a property which will be checked for relevancy. If
    // the given key is determined to be relevant, the item as a whole is
    // considered relevant and no other keys in the relevancy block are
    // checked for the current item
    //
    // The "strict" key allows you to turn on the "strict mode"
    // for DDG.isRelevant

    { key: 'short_desc' }
    // this is an extra "key" which servers as a fallback. This means if
    // either the 'name' or 'short_desc' or relevant the item is considered
    // relevant
],

// here we provide a secondary relevancy block with a chosen name of "category"
category: [
    { required: 'icon_url' },
    { key: 'name' },
    { key: 'short_desc' },
    { key: 'custom.features.category', match: category_regexp }
    // the "match" key allows you to specify a regular expression which the
    // given "key" must match
    //
    // Note: "match" only ensures the property matches the given regex. It
    // does NOT perform a relevancy check
],
```

**\*\*Note:** The relevancy checking is done using the `DDG.isRelevant()` function.

- ### type `string`

    The name of the relevancy block to use. If no value is provided, the default `primary` block will be used.

    For example, the Quixey spice determines the `type` based on the query. If the query matches against our category regex (i.e. the query contains a category word), we set `type` to "category", otherwise we use "primary".

- ### skip_words `array`

    A list of words to ***skip*** when comparing the specified text against the current query. Generally these words should include any trigger words for your Spice. The skip words list is **not** dependent on the chosen relevancy block.

- ### primary `array` [required when using relevancy]

    The list of relevancy terms for this particular relevancy block

- ### <additional_relevancy_block> `array`

    An additional list of relevancy terms, using the same format as `primary`. This object (and other relevancy blocks) can be named arbitrarily.

- ### dup `string`

    This indicates which property should be used to check for de-duplication. The given string supports dot path formatting, e.g., "item.foo.bar"


# Sorting

In some cases, the order of the tiles is important (e.g., price, rating, popularity) and you can use the sorting properties to specify the default ordering of the tiles. As well, you can specify additional sorting fields that will allow users to re-order the tiles using a different sort method.

### sort_fields `object`

This object specifies sorting fields (e.g., name, price, rating, reviews) and their respective comparison functions, which will be passed along to JavaScript's `sort()` method.

Example:

```javascript
sort_fields: {
    name: function(a,b) {
        return a.name < b.name ? -1 : 1;
    },
    rating: function(a,b) {
        return a.rating < b.rating ? -1 : 1;
    }
}
```


### sort_default `string|object`

A string specifying the default `sort_field` to be used for initial sorting of the tiles.

If you have used **more than one** relevancy block, `sort_default` can be given an `object` specifying the default `sort_field` for each relevancy block.

For example, if we had two relevancy blocks named `primary` and `category` our `default_sort` could look like this:

```javascript
sort_default: {
    primary: 'name',
    category: 'rating'
}
```


# Events

If you need to fire off an event handler when a tile is clicked or when your Spice's tab initially opens, the following properties can be used to define a callback function.

### onItemSelect `function`

This event occurs each time a tile is selected.

Example:

```javascript
onItemSelected: function(item) {
   player.play(item);
}
```

**\*\*Note:** If a tile-view result returns a single result, this event will also fire when the tab is opened/clicked, so you don't need to use both `onItemSelected` and `onShow` to handle the case of a single-result tile view

### onItemUnselect `function`

This event occurs each time a tile is unselected.

**\*\*Note:** If a tile-view result returns a single result, this event will also fire when the tab is closed, so you don't need to use both `onItemSelected` and `onShow` to handle the case of a single-result tile view

### onShow `function`

This event occurs when a Spice tab initially opens.

### onHide `function`

This event occurs when a Spice tab is closed i.e. when another tab is selected.