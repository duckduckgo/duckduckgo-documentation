# Triggers

There are two types of triggers, **words** and **regex**. We insist that you use word triggers whenever possible as they are simpler and faster.

## Word Triggers

### Usage
 
```perl
triggers <location> => <array of words and phrases>
```

#### Examples

```perl
triggers start => "trigger my instant answer", "trigger myIA", "myIA";
```

or

```perl
@triggers = qw(these are seperate triggers for my instant answer);
triggers any => @triggers;
```

or

```perl
triggers start => "starting phrase of query";
triggers end => "ending phrase of query";
```

### Trigger Locations

- `start` &mdash; Word exists at the start of the query
- `end` &mdash; Word exists at the end of the query
- `startend` &mdash; Word is at the beginning or end of the query
- `any` &mdash; Word is anywhere in the query

**\*\*Note:** You can combine several trigger statements if, for example, you want certain words or phrases to be **startend** but others to be **start**. The [Average Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Average.pm#L5) demonstrates the usage of multiple Word trigger statements.

## Regex Triggers

### Usage

```perl
triggers <query_format> => <regular expression>
```

#### Examples

```perl
triggers query_lc => qr/trigger (?:my|your|our) instant answer/;
```

or

```perl
my $regex = qr/^this is an? instant answer regexp$/;
triggers query_raw => $regex;
```

#### Query Formats

- `query_raw` &mdash; The query in its original form, with whitespace and case preserved
- `query` &mdash; Uniformly whitespaced version of `query_raw`
- `query_lc` &mdash; Lowercase version of `query`
- `query_nowhitespace` &mdash; `query` with all whitespace removed
- `query_clean` &mdash; `query_lc`, but with whitespace and non-alphanumeric ascii removed

**\*\*Note:** You **cannot** combine the use of **Regex Triggers** with **Word Triggers**.

## Regex Guards

We much prefer you use **trigger words** when possible because they are faster on the backend. In some cases however, **regular expressions** are necessary, e.g. you need to trigger on sub-words. In this case we suggest you consider using a **word trigger** and supplement it with a **regex guard**. A regex guard is a return clause immediately inside the `handle` function.

A good example of this is the Base64 goodie. In this case we want to trigger on queries with the form "base64 encode/decode \<string\>". Here's an excerpt from [Base64.pm](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Base64.pm) which shows how this case is handled using a word trigger, with a regex guard:

```perl
triggers startend => "base64";

handle remainder => sub {
    return unless $_ =~ /^(encode|decode|)\s*(.*)$/i;
```