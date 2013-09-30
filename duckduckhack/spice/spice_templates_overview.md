# Spice Templates Overview

There are several templates to choose from, each of which are best for displaying certain kinds of results and information.

In order to indicate which template you are using, you must set the `template_frame` property in the object given to the `Spice.render()` call. The below examples and explanations will clarify further implementation details. As well, for each template, various properties need to be set within the `template_options` property. These properties specify various settings for the template being used.

## List

### Use Case:

A list of results (eg. links) to display. Works best for bulleted/numbered lists.

### How it looks:

![List Template Example](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/list_template_example.png)

### How it works:

###### reddit_search.js [(link)](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/reddit_search/reddit_search.js)

```javascript
Spice.render({
    data              : api_result.data.children,
    header1           : header,
    source_url        : source,
    source_name       : 'Reddit',
    spice_name        : 'reddit_search',
    template_frame    : 'list',
    template_options  : {
        items: api_result.data.children,
        show: 2,
        max: 14,
        template_item: 'reddit_search'
    },
    force_big_header  : true,
    force_space_after : true,
    force_no_fold : true
});
```

### Template Options:

#### Required

- `items` &mdash; the array of results to be displayed

#### Optional

- `show` &mdash; default number of list items to display
- `max` maximum number of list items to display
- `template_item` &mdash; handlebars sub-template to be applied to each element in `items` array (should be used when `items` is an array of objects)

#### Advanced

See [below](#advanced-list--carousel).

## Carousel Template

### Use Case:
A list of results to display, each of which has a unique image and title. Each item also has more information to be displayed once the carousel item is clicked.

### How it looks:
![Carousel Template Example](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/carousel_template_example.png)

### How it works:

###### alternative_to.js [(link)](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/alternative_to/alternative_to.js)

```javascript
Spice.render({
    data                     : api_result,
    source_name              : 'AlternativeTo',
    source_url               : api_result.Url,
    spice_name               : 'alternative_to',
    template_frame           : "carousel",
    template_options         : {
        items                : api_result.Items,
        template_item        : "alternative_to",
        template_detail      : "alternative_to_details",
        li_height            : 60,
        single_item_handler  : function(obj) {
            obj.header1 = obj.data.Items[0].Name;
            obj.image_url = obj.data.Items[0].IconUrl;
        }
    },
});
```

### Template Options:

#### Required
- `items` &mdash; the array of results (should be objects) to be displayed
- `template_item` &mdash; handlebars sub-template to be applied to each element in `items` array (used to indicate the image and title for each carousel item)

#### Optional
- `template_detail` &mdash; handlebars sub-template to be applied to each element in `items` array (used to populate the "detail area" below carousel results)

#### Advanced

See [below](#advanced-list--carousel).

## Split Pane Template

### Use Case:

Single result that needs a vertically split layout (left & right panes) for your information.

### How it looks:

![Split Pane Template Example](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/split_pane_template_example.png)

### How it works:

###### airlines.js [(link)](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/airlines/airlines.js)

```javascript
Spice.render({
    header1          : onTime() + ": Flight Status for " + flight.Airline.Name + " " + flight.FlightNumber,
    source_url       : "http://www.flightstats.com/go/FlightStatus/flightStatusByFlight.do?&airlineCode=" + flight.Airline.AirlineCode + "&flightNumber=" + flight.FlightNumber,
    source_name      : "FlightStats",
    spice_name       : "airlines",
    template_frame   : "twopane",
    template_options : {
        left : { template: "airlines", data: departing },
        right : { template: "airlines", data: arriving },
    },
    force_no_fold    : true,
    force_big_header : true
});
```

### Template Options:

#### Required
- `left` &mdash; lets you specify the `template_options` for the left pane
    - `data` &mdash; the object to be used as input for the left pane
- `right` &mdash; lets you specify the `template_options` for the right pane
    - `data` &mdash; the object to be used as input for the right pane

#### Optional
- within in the above `left` or `right` property:
    - `template` &mdash; handlebars sub-template to be applied to the pane's `data` object


## Record Template

This template is somewhat different from the others, as it is more of a sub-template. Instead of having its own base template (like the above templates), developers can use the record template by using the Handlebars helper functions we've written. This means the record template can be used in any Handlebars files and so it can be used within other tempaltes as well.

### Use Case:

Single result with various pieces of information, each of which has a unique name/title/descriptor.

### How it looks:

![Record Template Example](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/record_template_example.png)

### How it works:

###### meta_cpan.js [(link)](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.js)

```javascript
Spice.render({
    data             : api_response,
    header1          : query + " (MetaCPAN)",
    source_url       : 'https://metacpan.org/' + link,
    source_name      : 'MetaCPAN',
    template_normal  : 'meta_cpan',
    force_big_header : true,
    force_no_fold    : true
});
```

###### meta_cpan.handlebars [(link)](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/meta_cpan/meta_cpan.handlebars)

```handlebars
{{rv "abstract"}}
{{rv "author"}}
{{rv "version"}}
{{#rd "Description"}}
    {{condense description maxlen="340" truncation="..."}}
{{/rd}}
```

## Explanation:

Seeing as this is a special kind of sub-template, no template options need to be specified. Instead special Handlebars helpers must be used inside the `template_normal` template.

### Handlebars Helpers:

- `{{#rt}}` &mdash; *block helper* used to specify a Title
- `{{#rd}}` &mdash; *block helper* used to specify a Descriptor (identical to `rt`, but created with a different CSS class)
- `{{rv}}` &mdash; shorter form of `rd`, produces a key-value pair if the named element exists in the `data` object

## Advanced Template Options (List & Carousel)

The **Carousel** and **List** templates also allow for more advanced (optional) `template_options` to be set:

### Modifying Carousel Item Dimensions

- `li_height` &mdash; lets you specify the *absolute* height for each carousel item
- `li_width` &mdash; lets you specify the *minimum* width for each carousel item

### Handling a Single Carousel/List Item

- `single_item_handler` &mdash; lets you specify a function which takes an object (the single API result) as input and uses it to modify/set the properties of `Spice.render()` (eg. `header1`, `image_url`) when only one item is returned from the upstream API.

**\*\*Note**: If a single result is returned and a `template_normal` has been specified, then that template will be used and the single item from the API will be passed along as the input. If no `template_normal` is defined, the system will check for a defined `template_detail` and use that. Failing that, it will check if `template_item` is defined and use that.