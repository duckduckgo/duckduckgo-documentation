# Spice Templates Overview
There are several templates to choose from, each of which are best for displaying certain kinds of results and information

## List

### Use Case:
A list of results (eg. links) to display. Works best for bulleted/numbered lists.

### How it looks:
![List Template Example](../assets/list_template_example.png)

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

### Explanation:
#### Required
- In the `Spice.render()` call, set the `template_frame` to `list` 
- In the `template options` property,  you must provide an array of results to the `items` property

#### Optional
- Indicate the default number of list items to show by setting the `show` property
- Indicate the max number of list items to show by setting the `max` property
- Indicate the sub-template to be used for each item in the list by giving the name of the handlebars template to the `template_item` property

## Carousel

### Use Case:
A list of results to display, each of which has a unique image and title. Each item also has more information to be displayed once the carousel item is clicked.

### How it looks:
![Carousel Template Example](../assets/carousel_template_example.png)

### How it works:
###### quixey.js [(link)](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/quixey/quixey.js)
```javascript
Spice.render({
    data: api_result,
    source_name: 'Quixey',
    source_url: 'https://www.quixey.com/search?q=' + q,
    header1: api_result.q + ' (App Search)',
    force_big_header: true,
    more_logo: "quixey_logo.png",
    template_frame: "carousel",
    template_options: {
        template_item: "quixey",
        template_detail: "quixey_detail",
        items: relevants
    }
});
```

### Explanation:
#### Required
- In the `Spice.render()` call, set the `template_frame` to `carousel` 
- In the `template options` property, you must provide an array of results to the `items` property
- Indicate the sub-template to be used for each item in the list by giving the name of the handlebars template to the `template_item` property

#### Optional
- Indicate the default number of list items to show by setting the `show` property
- Indicate the max number of list items to show by setting the `max` property
- Indicate the sub-template to be used for each item's detail area (the space that opens below the carousel) in the list by giving the name of the handlebars template to the `template_detail` property

## Split Pane

### Use Case:
Single result that needs a vertically split layout (left & right panes) for your information.

### How it looks:
![Split Pane Template Example](../assets/split_pane_template_example.png)

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

### Explanation:
#### Required
- In the `Spice.render()` call, set the `template_frame` to `twopane` 

#### Optional
- For each of the `left` and `right` panes, you can indicate both the data to be used as input as well as the sub-template to be used for the layout
- To set the input data for a pane, set the `data` property of the `left` or `right` pane to the name of the object to be used as input
- To set the sub-template for a pane, set the `template` property of the `left` or `right` pane to the name of the handlebars template to be used

## Record
This template is somewhat different from the others, as it is more of a sub-template. Instead of having its own base template (like the above templates), developers can use the record template by using the Handlebars helper functions we've written. This means the record template can be used in any Handlebars files and so it can be used within other tempaltes as well.

### Use Case:
Single result with various pieces of information, each of which has a unique name/title/descriptor.

### How it looks:
![Record Template Example](../assets/record_template_example.png)

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