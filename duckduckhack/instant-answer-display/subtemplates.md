# Using Sub-templates

Many [templates](https://duck.co/duckduckhack/templates_reference) allow you to pass *sub-templates* to fill out particular features. For example, to render custom calls-to-action, render content, or decide how to display lists of values.

The [templates reference](https://duck.co/duckduckhack/templates_reference) indicates which features can be passed a sub-template, and which can only be passed simple types.

## Specifying a Sub-template

Sub-templates are specified when [displaying your Instant Answer](https://duck.co/duckduckhack/display_reference#codetemplatescode_emobjectem_required), under the `options` object of the [`templates` property](https://duck.co/duckduckhack/display_reference#codetemplatescode_emobjectem_required). The name of the property is the template feature, and the value is the reference to the template.

For example, for the [Kwixer](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/kwixer/kwixer.js) Instant Answer, the `buy` feature of the [`products_detail` template](https://duck.co/duckduckhack/templates_reference#codeproductsdetailcode-template) is set to the custom [`Spice.kwixer.buy` sub-template](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/kwixer/buy.handlebars):

```javascript
templates: {
    ...
    options: {
        ...
        buy: Spice.kwixer.buy
    }
}
```

*Note that built-in sub-templates are specified as string values, and custom sub-templates are directly referenced as a function. More on these differences below.*

### Built-In Sub-templates

### Custom Sub-templates

## Using Available Helpers

## Using Style Guide Elements

