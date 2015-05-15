# Adding Your Spice to the DuckDuckGo AnswerBar

Once your Instant Answer has been triggered, and the API request has returned a response to the client, the final step is to display your results onscreen.

![answerbar](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fdiagrams%2Fanswerbar.png&f=1)

## Contents of the Spice Frontend Callback

The Spice frontend callback function, [covered in the Spice Basic Tutorial](https://duck.co/duckduckhack/spice_basic_tutorial#npm-spice-frontend-javascript), contains the code which displays your Spice. 

The most important part of this callback, and often the only part, is calling [`Spice.add()`](#codespiceaddcode-overview). This function is powerful and gives you a lot of control over how your results' appearance, context, and user interactions.

## Available Options

The properties you can pass to the `Spice.add()` function are documented in the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference). This document provides an in-depth overview of all that `Spice.add()` allows you to do.

In some scenarios, you may also want to handle the AnswerBar's events (for example, to stop media playing when the user hides your Instant Answer). These [events](https://duck.co/duckduckhack/display_reference#events) are covered at the end of the reference.

## Calling `Spice.add()`

The following is a code summary of how the options covered in the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference) are passed to `Spice.add()`

```javascript
Spice.add({

	// Required properties:
	
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

		snippetChars: Integer
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

    // Optional properties:

    normalize: Function,

    relevancy: {
        type: String,
        skip_words: [, String],
        primary: [, Object],
        dup: String,
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

For more information on each property and its usage, visit the [Instant Answer Display Reference](https://duck.co/duckduckhack/display_reference).