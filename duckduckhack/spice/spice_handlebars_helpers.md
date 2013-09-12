# Spice Helpers (Handlebars)

###`{{\#concat}}`
A block iterator that separates elements with an item separator and a
conjunction for the last item

#### Input
Array of Objects or Strings

#### Parameters
- `sep` (optional) &mdash; item seperator
    -   default value: `''`
- `conj` (optional) &mdash; confunction for last item
    -   default value: `''`

#### Usage
```handlebars
{{#concat arrayOfObjects sep="," conj="and"}}
    <a href="{{url}}">{{name}}</a>
{{/concat}}
```

```handlebars
{{#concat arrayOfStrings sep="," conj="and"}}
    {{this}}
{{/concat}}
```

###`{{\#condense}}`
Shortens input string to given `maxlen` and appends `truncation` to shortened string. If input string is already shorter than `maxlen`, simply returns input string

#### Input
String

#### Parameters
- `maxlen` &mdash; maximum string length
- `fuzz` (optional) &mdash; allowable deviation from the maxlen, allows a sentence/word to complete if it is less than `fuzz` character
    -   default value: `0`
- `truncation` (optional) &mdash; truncation string, appended to shortend string
    -   default value: `...`

#### Usage
```handlebars
{{condense myString maxlen="135" truncation="..."}}
```


###`{{\#stripHTML}}`
Removes all HTML tags and elements from input string

#### Input
String

#### Parameters
None

#### Usage
```handlebars
{{stripHTML text}}
```


###`{{\#loop}}`
Counts from zero to the value of obj, assuming obj is an object

#### Input
#### Parameters

#### Usage


###`{{\# }}`

#### Input
#### Parameters

#### Usage