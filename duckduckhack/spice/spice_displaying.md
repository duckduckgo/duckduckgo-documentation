# Using Spice.add()

As previously mentioned, `Spice.add()` is the crucial Spice function, which is used to display your Spice. However, this function is capable of much more than simply showing your Spice result. For example, it also helps you ensure the relevancy and order of results and allows you to provide various templates for different scenarios (e.g. mobile templates).

Here, we will outline in more detail all the possible parameters that can be set for `Spice.add()`:


# Essential Attributes

## id {string} [required]

A unique identifier for your Spice. Generally the `id` should match the name of your callback function. For example, if your callback function is named `ddg_spice_name`, your `id` should be `spice_name`.

## name {string} [required]

The name that will be used for your Spice's AnswerBar tab. Generally it can be a more formal version of your `id` or the API source name. For example, if your `id` is `lastfm_artist`, your `name` could be `Last.fm`.

## data {object} [required]

The object containing the data to be used by your templates. In most cases, it is best to pass along `api_result` to `data`, so that all of your API response is accessible to your templates.


# Instant Answer Meta Data

The following options are used to define elements of the **MetaBar** including the "More at" link. They are all attributes of the `meta: {}` object.

## searchTerm {string}

The term(s) that were searched, stripped of skip words (e.g. "cat videos" would be "cat"). This will be used for the MetaBar wording where it reads, for example, "Showing 15 **Electronics** Coupons". In this case "Electronics" is the `searchTerm`.

## itemType {string}

The type of item being shown (e.g. Videos, Images, Recipes). Again using the example "Showing 15 **Electronics** Coupons", "Coupons" is the `itemType`.

------

## primaryText {string}

If defined, this text will replace the MetaBar's "Showing **n** Items" text. For example, the Forecast Spice uses this to display "Weather for New York, NY" in the MetaBar.

------

## sourceName {string} [required]

The name of the source as it should be shown in the "More at" link. For example, in "More at Quixey", "Quixey" is the `sourceName`.

## sourceLogo {string - url}

If defined, the image provided will replace the `sourceName` with a logo. Generally this should not be necessary, however in rare cases, API providers require that a specific image be used to represent their brand and so this can be used.

## sourceUrl {string - url} [required]

The URL to follow when the "More at" link is clicked. This value will become the `href` of the "More at" link. It is preferred that **https\:\/\/** be used when possible.

## sourceIcon {boolean}

A boolean flag that determines if a favicon should be shown for the "More at" link. When a `sourceUrl` is given, this will default to `true`. This should only be set to `false` when no favicon exists for the `sourceUrl` domain.

## sourceIconUrl {string - url}

If the `sourceUrl` domain has no favicon (or if a different favicon is preferrd), the link provided here will be used as the source for the "More at" link's favicon. This will replace any favicons from the `sourceUrl` domain.

------

## secondaryText {string}

This is additional text label that will be displayed to the left of the "More at" link. For example, the Forecast Spice uses this to indicate the current temperature unit being used: "Temperatures in F&deg;".


# Data Normalization

## normalize {function} [required depending on template and data]

This allows you to provide a function which takes an object as input (the object given to `data`) and returns an anonymous object with normalized attribute names, which are required by any predefined templates.

This function uses jQuery's `$.extend()` method, so only the missing attributes need to be returned in the normalized object, which will then extend the original object that the function is operating on.

If you are using a pre-defined template (e.g. **basic_image_item**), it expects that certain attributes will be present (e.g `title`, `image`) and so the normalized function should be used to provide those or normalize their values if the already exist in your `api_result`.

For example, if you have a `data` object that looks like this:

```javascript
// original data object
{
    heading: "My awesome title",
    image:   "http://website.com/image.png"
}
```

You will likely want to use the `heading` attribute as the `title` for the **basic_image_item** template, so your `normalize` function would need to look like this:

```javascript
normalize: function(o){
    return {
        title: o.heading
    }
}
```

This would result in your `data` object looking like this once it gets passed along to the template:

```javascript
// normalized data object
{
    heading: "My awesome title",
    image:   "http://website.com/image.png",
    title:   "My awesome title",
}
```

Now, you object has all the required attributes for the **basic_image_item** template and everything will displayed as expected.


# Templates and Template Groups

## template_group {string}

Used to specify the base template (layout) to be used. Each `template_group` is composed of several components. The various options for this will be explained later, in the [template overview](#)

------

## templates {object} [required]

An object with multiple attributes, used to specify which sub-templates or custom templates are to be used. As well for each template, any **template options** may be provided or disabled depending on the chosen `template_group`.

## item {string|function} [required for *multiple* item result]

The template to be used for the body of each tile in a tile view.

**\*\*Note:** This will only display when your Spice instant answer returns multiple items (e.g. Jobs, Recipes, Apps)

- Generally, a **string** is provided to indicate the name of the pre-defined Spice template to be used, e.g. "products_item"
- Alternatively, a **function** can be provided when a custom template is necessary, e.g. `Spice.quixey.item`, which references the file "**/share/spice/quixey/item.handlebars**".

## item_custom {function}

Ssh. This doesn't exist...

## item_mobile {string|function}

An alternatve `item` template to be used when displaying on smaller screens, such as mobile and handheld devices.

## detail {string|function} [required for *single* item result]

The template to be used for the larger "detail" area, located below the tiles, in a tile view (i.e. a Spice that returns multiple items).

**\*\*Note:** The `detail` templates is **optional** and should only be used to provide additional information for each tile. If no additional information is needed, the tiles will become links and when clicked will redirect the used. For example, the Hacker News Spice does not use a `detail` template.

*Alternatively*, when dealing with a Spice that returns a **single** item (e.g. NPM, Is It Up), the `detail` will be displayed by default instead of a tile view. **If your Spice always returns a single item, only a `detail` template is required**.

## detail_custom {string}

Ssh. This doesn't exist either...

## detail_mobile {string|function}

An alternatve `detail` template to be used when displaying on smaller screens, such as mobile and handheld devices.

## item_detail {string|function}

An alternatve `detail` template to be used when a tile view contains a **single** tile.


# Relevancy

If you want to ensure the relevancy of your Spice's result (usually when dealing with multiple items), the relevancy attribute can be used to ensure the relevancy of each individual item. It can also be used to de-duplicate the returned items if desired.

In most cases you will only need to specify relevancy properties for the, **primary** relevancy block. However, if your Spice is capable of dealing with differnt types of queries, where different relevany checks are necessary, you can supply additional relevancy blocks. For example, the Quixey (Apps) Spice handles two distinct types of app searches, being **categorical** searches, such as "social networking apps", or more specific, named searches such as "free angry birds apps". When dealing with **categorical** searches, the name of the app doesn't need to be checked against the query for relevancy, however the app's category does and so two separate relevancy blocks, `primary` and `category` are used to define the different relevancy constraints.

## Relevancy Blocks

A relevancy block is comprised of an array of simple objects. For each object, the attributes are used to indicate certain constraints. The concept of a relevancy block is best explained with an example:

```javascript
// First we provide the name for the relevancy block, "primary"
primary: [

    { required: 'icon_url' },
    // "required" means the item must have a defined attribute matching the
    // given name, in this case and "icon_url" must be defined for each Quixey
    // item
    //
    // Note: "required" only ensures the presence of an attribute. It does NOT
    // perform a relevancy check

    { key: 'name', strict: true },
    // "key" indicates an attribute which will be checked for relevancy. If
    // the given key is determined to be relevant, the item as a whole is
    // considered relevant and no other keys in the relevancy block are
    // checked for the current item
    //
    // The "strict" key allows you to turn on the "strict mode"
    // for DDG.isRelevant

    { key: 'short_desc' }
    // this is an extra "key" which servers as a fallback. This means if
    // either the 'name' or 'short_desc' or relevant the item is consdiered
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
    // Note: "match" only ensures the attribute matches the given regex. It
    // does NOT perform a relevancy check
],
```

**\*\*Note:** The relevancy checking is done using the `DDG.isRelevant()` function.

## type {string}

The name of the relevancy block to use. If no value is provided, the default `primary` block will be used.

For example, the Quixey spice determines the `type` based on the query. If the query matches against our category regex (i.e. the query contains a category word), we set `type` to "category", otherwise we use "primary".

## skip_words {array}

A list of words to ***skip*** when comparing the specified text against the current query. Generally these words should include any trigger words for your Spice. The skip words list is **not** dependent on the chosen relevancy block.

## primary {array} [required when using relevancy]

The list of relevancy terms for this particular relevancy block

## <additional_relelvancy_block> {array}

An additional list of relevancy terms, using the same format as `primary`. This object (and other relevancy blocks) can be named arbitrarily.

## dup {string}

This indicates which attribute should be used to check for de-duplication. The given string supports dot path formatting, e.g. "item.foo.bar"


# Sorting

In some cases, the order of the tiles is important (e.g. price, rating, popularity) and so the sorting attributes allow you to specify which item attributes should be sorted and you can also specify how their order should be determined.

## sort_fields {object}

{{field name}} : function(l,r) 
comparison function for sorting items by this field

## sort_default {object}

Specify initial sort, keyed to sort_fields