# Spice Basic Tutorial

The NPM plugin [[link](https://duckduckgo.com/?q=npm+uglify-js)] [[code](https://github.com/duckduckgo/zeroclickinfo-spice/tree/master/share/spice/npm)] is a great example of a basic Spice implementation which utilizes the [the Node.js package search API](http://registry.npmjs.org/uglify-js/latest). Let's walk through it line-by-line:

## NPM Backend

##### npm.pm
```perl 
package DDG::Spice::Npm;

use DDG::Spice;

spice to => 'http://registry.npmjs.org/$1/latest';
spice wrap_jsonp_callback => 1;
spice is_cached => 0;

triggers startend => 'npm';

handle remainder => sub {
    return $_ if $_;
    return;
};

1;

```

To refresh your memory, the **triggers** keyword tells the plugin system when to call a plugin. In the [Basic Tutorial](#basic-tutorial) we discussed using the **start** keyword to specify trigger words that need to be present at the beginning of the query. Check out the section on [Triggers](general.md#triggers) for more information.

Previously we saw the use of the **remainder** keyword as in **handle remainder**, which works well for trigger words. We use it again here.

##### npm.pm (continued)
```perl
    return $_ if $_;
```

`$_` is a contextual variable in Perl. Its value in this case is the **remainder**. That is, `uglify-js` in the linked example above -- the query with the trigger word stripped out. If we get a non-blank package name, we return it.

Otherwise, we return nothing, which short-circuits the eventual external call.

##### npm.pm (continued)
```perl
   return;
```

When the package name is returned we then plug it into the **spice to** definition.

##### npm.pm (continued)
```perl
spice to => 'http://registry.npmjs.org/$1/latest';
```

The **$_** value from the return statement will get inserted into the **$1** placeholder in the **spice to** line such that you can plug in parameters to the API call as needed. Passing multiple parameters into the API call is also possible and will be discussed later in the advnaced section.

In this particular case, the API we're using to search for packages does not support callback functions. That is, it will not wrap its response in a function call, which in this case would be **ddg_spice_npm**. If it did support a callback, we could use the **{{callback}}** template in the **spice to** line to automatically fill in the default callback value. See the [IMdB spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Imdb.pm) for a simple implementation of the **{{callback}}** template. Since this API doesn't support the callback parameter, we tell the backend to automatically wrap the API's response in a function call for us with:

##### npm.pm (continued)
```perl
spice wrap_jsonp_callback => 1;
```

At this point the response moves from the backend to the frontend. The external API sends a JSON object to the callback function that you will also define, as explained in the following sections.

## NPM Frontend

##### npm.js
```javascript
function ddg_spice_npm (api_result) {
    if (api_result.error) return

    Spice.render({
         data              : api_result,
         force_big_header  : true,
         header1           : api_result.name + ' (' + api_result.version + ')',
         source_name       : "npmjs.org", // More at ...
         source_url        : 'http://npmjs.org/package/' + api_result.name,
         template_normal   : 'npm',
         template_small    : 'npm'
    });
}
```

As mentioned, every plugin requires a Spice callback function, for the *NPM* plugin, the callback is the `ddg_spice_npm()` function that we defined here in *npm.js*. The *NPM* Perl module we wrote specifies this as the callback by using the name of the package `DDG::Spice::NPM` and gives this *ddg_spice_npm* name to the API call so that this funtion will be executed when the API responds using the data returned from the upstream (API) provider as the function's input.

##### npm.js (continued)
```javascript 
if (api_result.error) return
```
Pretty self-explanatory - If the error object in the API result is defined, then break out of the function and don't show any results. In the case of this API, when the error object is defined, it means no results are given, so we have no data to use for a Spice result. 

##### npm.js (continued)
```javascript
Spice.render({
     data              : api_result,
     force_big_header  : true,
     header1           : api_result.name + ' (' + api_result.version + ')',
     source_name       : "npmjs.org",
     source_url        : 'http://npmjs.org/package/' + api_result.name,
     template_normal   : 'npm',
     template_small    : 'npm'
});
```

Alright, so here is the bulk of the plugin, but it's very simple:

- `Spice.render()` is a function that the plugin system has already defined. You pass an object to it that specifies a bunch of important parameters. 

- `data` is perhaps the most important parameter. The object given here will be the object that is passed along to the Handlebars template. In this case, the context of the NPM template will be the **api_result** object. This is very important to understand because **only the data passed along to the template is accessible to the template**. In most cases the `data` parameter should be set to 
`api_result` so all the data returned from the API is accessible to the template. 

- `force_big_header` is related to the display formatting -- it forces the system to display the large grey header that you see when you click the example link above. 

- `header1` is the text of this header, i.e. the text displayed inside the large grey bar. 

- `source_name` is the name of the source for the "More at <source>" link that's displayed below the text of the plugin for attribution purposes. 

- `source_url` is the target of the "More at" link. It's the page that the user will click through to. 

- `template_normal` is the name of the Handlebars template that contains the structure information for your plugin.

- `template_small` is the name of the Handlebars template to be used when you plugin is displayed in a stacked state. This isn't required, but if your plugin can provide a succint, one or two line answer this template should be used in the event that the plugin appears in the stacked state. If no template is given the stacked result will simply show the header of the spice result 

----

Now, let's look at the NPM plugin's Handlebars template:

###### npm.handlebars
```html
<div>
    <div>{{{description}}}</div>
    <pre> $ npm install {{{name}}}</pre>
</div>
```

As you can see, this is a special type of HTML template. Within the template, you can refer directly to objects that are returned by the API. `description` and `name` are both from the `api_result` object that we discussed earlier -- the data that's returned by the API. All of `api_result`'s sub-objects (e.g. `name`, `description`) are in the template's scope. You can access them by name using double or triple curly braces (triple braces will not escape the contents). Here, we just create a basic HTML skeleton and fill it in with the proper information.

### Conclusion
We've created two files in the Spice share directory (`share/spice/npm/`) :

1. `npm.js` - which delegates the API's response and calls `Spice.render()`
2. `npm.handlebars` - which specifies the plugin's HTML structure and determines which attributes of the API response are placed in the HTML result

You may notice other plugins also include a css file. For **NPM** the use of CSS wasn't necessary and this is also true for many other plugins. If however CSS is needed it can be added. Examples with CSS usage will be covered shortly.