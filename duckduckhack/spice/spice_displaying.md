## Adding Your Spice to the DuckDuckGo AnswerBar

Once your Instant Answer has been triggered, and the API request has returned a response to the client, the final step is to display your results onscreen.

This is done by the Spice frontend callback function, [covered in the basic tutorial](https://duck.co/duckduckhack/spice_basic_tutorial#npm-spice-frontend-javascript). The most important part of this callback is calling `Spice.add()`. This function adds your Spice to the AnswerBar. 

This function is powerful and gives you a lot of control over how your results' appearance, context, and user interactions. This document provides an in-depth overview of all that `Spice.add()` allows you to do.

------

## `Spice.add()` Properties Overview

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

		variants: Object
		
		elClass: Object
    },

	view: String,
	model: String,

    sort_fields: Object,
    sort_default: String|Object,

    onItemSelect: Function,
    onItemUnselect: Function,
    onShow: Function,
    onHide: Function

  });
```

### Required Properties

- [id](http://duck.co/duckduckhack/spice_displaying#id-codestringcode-required) A unique identifier for your Spice. The `id` should match the name of your callback function
- [name](http://duck.co/duckduckhack/spice_displaying#name-codestringcode-required) The name that will be used for your Spice's AnswerBar tab
- [data](http://duck.co/duckduckhack/spice_displaying#data-codeobjectcode-required) The object containing the data to be used by your templates

### Optional Properties

- [meta](http://duck.co/duckduckhack/spice_displaying#instant-answer-metadata) Used to define elements of the **MetaBar** including the "More at" link
- [normalize](http://duck.co/duckduckhack/spice_displaying#data-normalization) This allows you to normalize the `data` before it is passed on to the template
- [templates](http://duck.co/duckduckhack/spice_displaying#templates) Used to specify the template group and all other templates that are being used
- [relevancy](http://duck.co/duckduckhack/spice_displaying#relevancy) Used to ensure the relevancy of your Spice's result
- [view](http://duck.co/duckduckhack/spice_displaying#views) This allows you to explicitly specify the view class used for displaying the Instant Answer
- [model](http://duck.co/duckduckhack/spice_displaying#model) This allows you to use one of our predefined data models that include domain specific helpers/normalization/formatting.

------

## `id` *string* [required]

A unique identifier for your Spice. The `id` should match the name of your callback function. For example, if your callback function is named `ddg_spice_name`, your `id` should be `spice_name`.

------

## `name` *string* [required]

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

------

## `data` *object* [required]

The object containing the data to be used by your templates. In most cases, it is best to pass along `api_result` to `data`, so that all of your API response is accessible to your templates.

------

## `meta` *object* [required]

The following options are used to define elements of the MetaBar including the "More at" link. They are all properties of the `meta: {}` property.

- ### `sourceName` *string* [required]

    The name of the source as it should be shown in the "More at" link. For example, in "More at Quixey", "Quixey" [is specified](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js#L77) as `sourceName`.

- ### `sourceUrl` *url string* [required]

	The URL to follow when the "More at" link is clicked. This value is the `href` attribute of the "More at" link. This can refer to the main page of the source, or better yet, the specific page relevant to the user's query. 
	
	Secure **https\:\/\/** should be used whenever possible.

	#### Examples
	
	- In [rand_word.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/rand_word/rand_word.js#L14), the `sourceUrl` is a hardcoded address.
	- In [is_it_up.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/is_it_up/is_it_up.js#L15), the `sourceUrl` is dynamically generated to direct to a specific page relating to the search query.

- ### `searchTerm` *string*

	Determines the modifier in the MetaBar's description: "Showing 15 `searchTerm` `itemType`".
	
    The `searchTerm` is used to describe the `itemType` and it can be determined by removing any skip words from the original query. 

	For example, searching "coupons for electronics", will display the phrase "Showing 15 **electronics** Coupons" in the MetaBar. In this case, the word "electronics" is the `searchTerm`.
	
	#### Examples 

	- In [news.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/news/news.js#L89), `searchTerm` is passed the search query with some string manipulation.
	- In [images.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/images/images.js#L19), `searchTerm` is passed the query as-is.
	- In [alternative_to.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js#L16), `searchTerm` is passed a name provided by the API.
	- In [songkick_geteventid.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/songkick/geteventid/songkick_geteventid.js#L38), `searchTerm` is passed a city name.

- ### `itemType` *string*

    Determines the noun in the MetaBar's description: "Showing 15 `searchTerm` `itemType`". In other words, `itemType` is the type of item being shown (e.g., Videos, Images, Recipes).
	
	Using the previous example, in the phrase, "Showing 15 **electronics** Coupons", the word "Coupons" is the `itemType`.
	
	#### Examples
	
	- In [news.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/news/news.js#L90), the `itemType` is a string: `'News articles'`.
	- In [images.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/images/images.js#L19), there is no `itemType`. You can see the [resulting description](https://duckduckgo.com/?q=duck+images&ia=images) in the AnswerBar.

- ### `primaryText` *string*

    If defined, this text will replace the MetaBar's "Showing **n** Items" text. 

	#### Example

	- In [parking.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/parking/parking.js#L89), the `primaryText` is set to `'Parking near'` plus the location.

- ### `secondaryText` *string*

    This is an optional text label, displayed to the left of the "More at" link. For example, a weather forecast Spice might use this to indicate the temperature unit, such as "Temperature in F&deg;".

- ### `sourceLogo` *url string*

    If defined, the image provided will replace the `sourceName` with a logo. Generally this is not necessary; in rare cases, API providers require that a specific image be used to represent their brand.

	### Example
	
	From [quixey.js](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js#L79):
	
	```javascript
		meta:{
			...
			sourceLogo: {
	            url: DDG.get_asset_path('quixey','quixey_logo.png'),
	            width: '45',
	            height: '12'
	        }
		}
	```
	
	You can see it in action by [searching for apps](https://duckduckgo.com/?q=money+apps&ia=apps).

- ### `sourceIcon` *boolean*

    A boolean flag that determines if a favicon should be shown to the left of the "More at" link. The favicon is pulled dynamically from the source domain by duckduckgo's server. 

	When a `sourceUrl` is given, this will default to `true`. It should only be set to `false` when the `sourceUrl` domain does not have a favicon.

- ### `sourceIconUrl` *url string*

    If the `sourceUrl` domain has no favicon (or if a different favicon is preferred), you can explicitly set a url path for the "More at" favicon source. This value, if set, will take precedence any favicons pulled from the `sourceUrl` domain.

------

## `normalize` *function*

Specifying this optional function allows you to normalize each item (or single item) returned in the `data` object before it is passed on to the template. You can use this function to add or modify properties for use by your template. 

When dealing with multiple items returned in the `data` object, the normalize function iterates over each `item` so they can be individually normalized.

Use this function to return an object with properties to be incorporated in your item as it's passed to the template. These properties are incorporated using jQuery's `$.extend()` method, meaning it will *modify* your original `data` object instead of replacing it. Using `$.extend()` means that any properties that don't already exist will be added, and those that did originally exit will be overwritten. In other words, a shallow copy is made.

Normalize can be particularly useful if you are using a [built-in template](https://duck.co/duckduckhack/spice_templates_reference#spice-templates) (e.g., *basic_image_item*). Built-in templates expect that certain properties will be present (e.g. `title`, `image`) and so the normalized function allows you to provide those (or normalize their values if the already exist in your `api_result`).

For example, if you have a `data` object that looks like this:

```javascript
// original data object from API
{
    heading: "My awesome title",
    image:   "http://website.com/image.png"
}
```

You will likely want to pass the `heading` property as the `title` for the **basic_image_item** template, so your `normalize` function would need to look like this:

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

### `exactMatch` *boolean* and `boost` *boolean*

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

------

## `templates` *object*

A `templates: {}` property should be used to specify the template group and all other templates that are being used. Template options can also be provided to enable or disable features depending on the chosen template group.

<!-- /summary -->

- ### `group` *string* [required, unless `item` and `detail` are specified]

    Used to specify the base template (layout) to be used. Each template `group` is composed of several features. The various options for this will be explained later in the [template overview](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_templates_overview.md).

    This will tell the template system that the templates belonging to the given group will be used for the `item`, `detail`, etc. **unless otherwise specified**.

    For example, `group: 'info'` will implicitly set:

    ```javascript
    item: 'basic_item',
    item_detail: 'basic_info_item_detail',
    detail: 'basic_info_detail'
    ```

- ### `item` *string|function* [required if no `group` is specified]

    The template to be used for the body of each tile in a tile view.

    **Note:** The `item` template is only used when your Spice Instant Answer returns multiple items (like the recipe or app Instant Answers), meaning the object given to `data` is an *`array`* with more than 1 elements.

    - Generally, a string is provided to indicate the name of the built-in Spice template to be used, e.g., "products_item"

    - Alternatively, a function can be provided when a custom template is necessary, e.g., `Spice.quixey.item`, which references the file "**/share/spice/quixey/item.handlebars**".

- ### `item_mobile` *string|function*

    An alternative `item` template to be used when displaying on smaller screens, such as mobile and hand-held devices.

- ### `detail` *string|function* [required if no `group` is specified]

    The template to be used for the detail area.

    *For multiple items*, the detail area will be located below the tiles, and will display when a tile is clicked. If your Spice returns multiple items, the `detail` template is **optional**.

    *For a single item*, the detail area will be right below the AnswerBar and will display instantly. If your Spice always returns a single item, only a `detail` template is **required**.

    **Note:** The `detail` templates is **optional for a tile view** and should only be used to provide additional information for each tile.

- ### `detail_mobile` *string|function*

    An alternative `detail` template to be used when displaying on smaller screens, such as mobile and hand-held devices.

- ### `item_detail` *string|function*

    An alternative `detail` template to be used when a tile view contains a **single** tile.

- ### `options` *object*

    Allows you to explicitly disable or enable features of a template, as well as specify any sub-templates when applicable (e.g., the `content` feature of the `'info'` template). Depending on the templates being used, the features will vary. For example, the `'info'` template doesn't have a `brand` feature, so attempting to enable or disable that feature will have no effect.

- ### `variants` *object*

	If you'd like to modify a template to fit your needs, the Spice framework offers preset options called [Variants](https://duck.co/duckduckhack/spice_templates_reference#spice-variants-reference). Variants are passed as the `variants` property of `templates`, in your call to `Spice.add()`. Variants correspond to pre-determined css classes (or combinations of classes) from the [DDG style guide](https://duckduckgo.com/styleguide) that work particularly well in each context.
	
- ### `elClass` *object*

	When variants don't suffice, you can [directly choose classes](https://duck.co/duckduckhack/spice_templates_variants#directly_specifying_classes) based on the [DDG style guide](https://duckduckgo.com/styleguide) through the `elClass` property of `templates`, in your call to `Spice.add()`. This feature is mainly used for specifying text size and color.

	Classes can be directly specified to the same elements as Variants; the locations are identical. If you are specifying both `variants` and `elClass`, both will be applied together.

    **Note:** If you intend to use a feature that is disabled by default, it **must** be enabled in the `options` for it to display. Even if the property exists in the `data` object, the template system will ignore it if the feature is disabled. For example:

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

------

## `relevancy` *object*

If you want to ensure the relevancy of your Spice's result (usually when dealing with multiple items), the `relevancy: {}` property can be used to ensure the relevancy of each individual item. It can also be used to de-duplicate the returned items if desired.

In most cases you will only need to specify relevancy properties for the, **primary** relevancy block. If your Spice is capable of dealing with different types of queries though, where different relevancy checks are necessary, you can supply additional relevancy blocks. For example, the Quixey (Apps) Spice handles two distinct types of app searches, being **categorical** searches, such as "social networking apps", or more specific, named searches such as "free angry birds apps". When dealing with **categorical** searches, the name of the app doesn't need to be checked against the query for relevancy. However, the app's category does need to be checked and so two separate relevancy blocks, `primary` and `category`, are used to define the different relevancy constraints.

### Relevancy Blocks

A relevancy block is comprised of an array of simple objects. For each object, the properties are used to indicate certain constraints. The concept of a relevancy block is best explained with an example:

<!-- /summary -->

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

**Note:** The relevancy checking is done using the `DDG.isRelevant()` function.

- ### `type` *string*

    The name of the relevancy block to use. If no value is provided, the default `primary` block will be used.

    For example, the Quixey spice determines the `type` based on the query. If the query matches against our category regex (i.e. the query contains a category word), we set `type` to "category", otherwise we use "primary".

- ### `skip_words` *array*

    A list of words to ***skip*** when comparing the specified text against the current query. Generally these words should include any trigger words for your Spice. The skip words list is **not** dependent on the chosen relevancy block.

- ### `primary` *array* [required if using `relevancy`]

    The list of relevancy terms for this particular relevancy block

- ### `<additional_relevancy_block>` *array*

    An additional list of relevancy terms, using the same format as `primary`. This object (and other relevancy blocks) can be named arbitrarily.

- ### `dup` *string*

    This indicates which property should be used to check for de-duplication. The given string supports dot path formatting, e.g., "item.foo.bar"

------

## `sort_fields` *object*

In some cases, the order of the tiles is important (e.g., price, rating, popularity) and you can use the sorting properties to specify the default ordering of the tiles. You can also specify additional sorting fields that will allow users to re-order the tiles using a different sort method.

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


### `sort_default` *string|object*

A string specifying the default `sort_field` to be used for initial sorting of the tiles.

```javascript
sort_default: 'name';
```

If you have used **more than one** relevancy block, `sort_default` can be given an `object` specifying the default `sort_field` for each relevancy block.

For example, if we had two relevancy blocks named `primary` and `category` our `default_sort` could look like this:

```javascript
//because we have two relevancy blocks...
sort_default: {
    primary: 'name',
    category: 'rating'
}
```

------

## `view` *string*

Typically you don't need to specify a view for Instant Answers unless you're using special functionality like the playable Audio tiles for the SoundCloud IA, or the Maps used in our Places IA.

Available Views:

- Audio
- Detail (default view for IAs with a single item)
- Images
- Map
- Places
- Tiles (default view for IAs with multiple items)
- TilesWithTopics
- Videos

------

## `model` *string*

Typically you don't need to specify a model for your Instant Answer. However, if your data is of a common type, we have pre-built models that can help with formatting things like Lat/Lon for a Place or Dimensions for an Image. Also, to use some of our non-default views, like Audio or Places you need to use a compatible data model.

Available Models:

- Audio
- Image
- Place
- Product
- Video

<!-- 

#### Audio attributes:

#### Image attributes:

-->

#### Place attributes:

If you use the Place data model, you can normalize your data into objects with these attributes and the built-in Map/Places views will automatically know how to handle them:

- id (string): unique identifier for the location
- name (string): name of the location
- address (string): display address of the location
- city (string)
- neighborhood (string): if neighborhood and city are both passed in, it will use neighborhood for the tile and fall back to the city when it's not there
- image (string): path to image thumbnail to be used for the location, will use default marker image if none is provided
- polygonPoints (array): if the location represents a region, array of lat/lon coordinates that create the shaded outline in queries like 'Paris map'
- lat (number): latitude of the location
- lon (number): longitude of the location
- rating (number): number from [0-5], supports half's, i.e. 3.5
- ratingImageURL (string): optional, use custom rating image URL (i.e. Yelp)
- reviews (number): number of reviews
- price (number): integer from [0-4], will be converted to $$$$ symbols
- hours (object): hash where three char day is the key and the value is a string of hours for that day, i.e.: { 'Mon': '8am - 5pm', 'Thu': '1pm - 5pm' }
- phone (string)

<!--

#### Product attributes:

#### Video attributes:

-->

#### Examples:

Render a single location on a map:

```
Spice.add({
  id: 'landmarks',
  name: 'Landmarks',
  model: 'Place',
  view: 'Map',
  templates: {
    group: 'places'
  },
  meta: {
    sourceName: 'Wikipedia',
    sourceUrl: 'https://wikipedia.org'
  },
  data: [{
    id: 'uniqueid-1',
    name: 'Empire State Building',
    url: 'https://en.wikipedia.org/wiki/Empire_State_Building',
    image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/2/20/Empire_State_Building_by_David_Shankbone.jpg/480px-Empire_State_Building_by_David_Shankbone.jpg',
    rating: '3.5',
    address: '350 Fifth Ave',
    neighborhood: 'Midtown',
    city: 'New York City',
    price: 3,
    lat: 40.7484324,
    lon: -73.98566413,
    hours: {
      Thu: '8am - 5pm'
    }
  }]
});
```

Render multiple locations as tiles with an expandable map:

```
Spice.add({
  id: 'landmarks',
  name: 'Landmarks',
  model: 'Place',
  view: 'Places',
  templates: {
    group: 'places'
  },
  meta: {
    type: 'Landmarks',
    sourceName: 'Wikipedia',
    sourceUrl: 'https://wikipedia.org'
  },
  data: [{
    id: 'uniqueid-1',
    name: 'Empire State Building',
    url: 'https://en.wikipedia.org/wiki/Empire_State_Building',
    image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/2/20/Empire_State_Building_by_David_Shankbone.jpg/480px-Empire_State_Building_by_David_Shankbone.jpg',
    rating: '3.5',
    address: '350 Fifth Ave',
    neighborhood: 'Midtown',
    city: 'New York City',
    price: 3,
    lat: 40.7484324,
    lon: -73.98566413,
    hours: {
      Thu: '8am - 5pm'
    }
  },{
    id: 'uniqueid-2',
    name: 'Central Park',
    url: 'https://en.wikipedia.org/wiki/Central_Park',
    image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/0/05/Southwest_corner_of_Central_Park%2C_looking_east%2C_NYC.jpg/240px-Southwest_corner_of_Central_Park%2C_looking_east%2C_NYC.jpg',
    rating: 5,
    address: '86th Street, Traverse Road',
    neighborhood: 'Midtown',
    city: 'New York City',
      lat: "40.78257765",
      lon: "-73.9654435614027",
    phone: '867-5309',
    reviews: 327,
    polygonPoints: [["-73.9812971","40.7685782"],["-73.9812422","40.7686381"],["-73.9808211","40.7692536"],["-73.9582984","40.8002063"],["-73.958121","40.8002149"],["-73.9580084","40.8002271"],["-73.9578827","40.8002631"],["-73.957767","40.8003367"],["-73.9577187","40.8003814"],["-73.9497096","40.7969917"],["-73.9497163","40.7969425"],["-73.9497167","40.7968837"],["-73.9497187","40.796838"],["-73.9497076","40.7967616"],["-73.9496758","40.7966888"],["-73.9496293","40.7966412"],["-73.9495571","40.79659"],["-73.9724949","40.7650918"],["-73.9732368","40.7653987"],["-73.9737105","40.7647739"],["-73.9793669","40.767163"],["-73.9810178","40.7678443"],["-73.9809825","40.7678988"],["-73.9809709","40.7679534"],["-73.9809572","40.7680187"],["-73.9808933","40.7680086"],["-73.9808902","40.7680668"],["-73.980888","40.7681073"],["-73.9809093","40.7682121"],["-73.9808827","40.7682181"],["-73.980908","40.7682967"],["-73.9809213","40.7682936"],["-73.9809652","40.7684004"],["-73.9810569","40.7683631"],["-73.9810729","40.7683834"],["-73.9811234","40.7684477"],["-73.9811992","40.7685112"],["-73.9812971","40.7685782"]]
  }]
});
```

------

## Events

If you need to fire off an event handler when a tile is clicked or when your Spice's tab initially opens, you can handle these events with a callback function.

- ### `onItemSelect` *function*

	This event occurs each time a tile is selected.

	Example:

	```javascript
	onItemSelected: function(item) {
	   player.play(item);
	}
	```

	**Note:** If a tile-view result returns a single result, this event will also fire when the tab is opened/clicked, so you don't need to use both `onItemSelected` and `onShow` to handle the case of a single-result tile view

- ### `onItemUnselect` *function*

	This event occurs each time a tile is unselected.

	**Note:** If a tile-view result returns a single result, this event will also fire when the tab is closed, so you don't need to use both `onItemSelected` and `onShow` to handle the case of a single-result tile view

- ### `onShow` *function*

	This event occurs when a Spice tab initially opens.

- ### `onHide` *function*

	This event occurs when a Spice tab is closed i.e. when another tab is selected.
