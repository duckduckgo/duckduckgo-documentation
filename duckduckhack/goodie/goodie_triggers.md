# Triggers

There are two types of triggers, **words** and **regex**. While you technically *can* use a regular expression as a trigger, we encourage you to use words triggers first, and then use a regexp to further qualify the query once the plugin has been called, like in the [Xkcd example](https://github.com/duckduckgo/zeroclickinfo-spice#spice-handle-functions) in the Spice Handle Functions section. Words triggers are several orders of magnitude faster than regexp triggers (a hash check vs. a regexp match).

## Words Triggers

```
start......word exists at the start of the query
end........word exists at the end of the query
startend...word is at the beginning or end of the query
any........word is anywhere in the query
```

You can combine several trigger statements if, for example, you want certain words to be **startend** but others to be **start**. The [Average Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Average.pm#L5) is a good example of multiple words trigger statements.


## Regex Triggers

Regular expression triggers can be applied to the following query objects:

```
query_raw............the query in its most basic form, with no clean-up string operations.
query................uniformly whitespaced version of query_raw.
query_lc.............lowercase version of *query*.
query_nowhitespace...*query* with no whitespace.
query_clean..........*query_lc*, but with whitespace and non-alphanumeric ascii removed.

```