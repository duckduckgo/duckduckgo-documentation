# Advanced Triggers
In the [Basic tutorial](general.md#basic-tutorial) we walked through a one word trigger and in the [Spice handle functions](spice.md#spice-handle-functions) section we walked through a simple regexp trigger.

Here are some more advanced trigger techniques you may need to use:

**Multiple trigger words**. &nbsp;Suppose you thought that in addition to _chars_, _numchars_ should also trigger the [Chars Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Chars.pm). You can simply add extra trigger words to the triggers definition.

```perl
triggers start => 'chars', 'numchars';
```

**Trigger locations.** &nbsp;The keyword after triggers, **start** in the Chars example, specifies where the triggers need to appear. Here are the choices:

 * start - just at the start of the query
 * end - just at the end of the query
 * startend - at either end of the query
 * any - anywhere in the query

**Combining locations.** &nbsp;You can use multiple locations like in the [Drinks Spice](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Drinks.pm).

```perl
triggers any => "drink", "make", "mix", "recipe", "ingredients";
triggers start => "mixing", "making";
```

**Regular Expressions.** &nbsp;As we walked through in the [Spice handle functions](spice.md#spice-handle-functions) section you can also trigger on a regular expression.

```perl
triggers query_lc => qr/^@([^\s]+)$/;
```

We much prefer you use trigger words when possible because they are faster on the backend. In some cases regular expressions are necessary, e.g. when you need to trigger on sub-words. However, you should still consider using a word trigger and a **regex guard**. A regex guard is a return clause immediately inside the handle function. A good example of this is the Base64 goodie. Here's an excerpt from Base64.pm:

```perl
triggers startend => "base64";

handle remainder => sub {
    return unless $_ =~ /^(encode|decode|)\s*(.*)$/i;
```

This way, we get the speed of the word trigger and still ensure that the search query is an exact match for our plugin. You can also return similarly (without a value) at any point in the handle function if the answer cannot be calculated.


**Regexp types.** &nbsp;Like trigger words, regular expression triggers have several keywords as well. In the above example **query_lc** was used, which operates on the lower case version of the full query. Here are the choices:

 * **query_raw** - the actual (full) query
 * **query** - with extra whitespace removed
 * **query_lc** - lower case version of the query and extra whitespace removed
 * **query_clean** - lower case with non alphanumeric ASCII and extra whitespace removed
 * **query_nowhitespace** - with whitespace totally removed
 * **query_nowhitespace_nodash** - with whitespace and dashes totally removed

If you want to see some test cases where these types are enumerated check out our [internal test file](https://github.com/duckduckgo/duckduckgo/blob/master/t/15-request.t) that tests they are generated properly.

**Multi-word triggers**. &nbsp;Triggering also supports the use of trigger "phrases". An example of this usage can be seen in the [Hacker News](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/HackerNews.pm) plugin.

```perl
triggers startend => "hn", "hackernews", "hacker news", "hn search", "hnsearch", "hacker news search", "news.yc", "news.ycombinator.com", "hackernews search";
```

Just like single word triggers, if a phrase is used when handling the remainder, the entire phrase will be stripped away from the query.

Alternatively to using a trigger phrase a you could also use a word trigger and then further qualify the query within the handle function as explained in the [Advanced handle functions](#advanced-handle-functions) section.
