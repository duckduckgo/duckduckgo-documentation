# Triggers

There are two types of triggers, **words** and **regex**. We insist that you use word triggers whenever possible as they are several orders of magnitude faster than regexp triggers (a hash check vs. a regexp match). Although you *can* use a regular expression as a trigger, unless it is completely necessary, we encourage you to rather use a word trigger followed by the use of regular expressions (in the `handle` function) to further qualify the query once the instant answer has been triggered. This way the triggering of the instant answer is simplified and quick, but the use of a regex inside the `handle` allows you to make sure the instant answer works for the given query.

## Words Triggers

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

**\*\*Note:** You can combine several trigger statements if, for example, you want certain words or phrases to be **startend** but others to be **start**. The [Average Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Average.pm#L5) demonstrate the usage of multiple Word trigger statements.

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

