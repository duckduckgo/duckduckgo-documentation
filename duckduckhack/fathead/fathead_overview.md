# Fathead Instant Answers

(intro - tbd)

## Structure

Each Fathead instant answer has its own directory. Some of the directories are in use on the live system, and some are still in development.

Each directory has a structure like this:

```shell
# This is a Perl file that lists some meta information about the instant answer
lib/DDG/Fathead/FatheadName.pm

# This shell script is called to fetch the data. 
# Tmp files should go in a directory called download.
share/fathead_name/fetch.sh

# This is the script used to parse the data once it has been fetched. 
# .xx can be .pl, .py, .rb, .js, etc. depending on what language you use.
share/fathead_name/parse.xx

# This shell script is called to run the parser. 
share/fathead_name/parse.sh

# Please include any dependencies here,
# or other special instructions for people
# trying to run it.
share/fathead_name/README.txt

# This is the output file.
# Generally it should NOT be committed,
# but if it is small (<1MB) it is useful to do so.
share/fathead_name/output.txt

# This is an optional pointer to a URL in the cloud somewhere,
# which contains the data to process.
share/fathead_name/data.url
```


## Data File Format

Please name the output file output.txt (tab delimited) but do not store the data file(s) in the repository (as noted above) unless it is under 1MB.

The output file needs to use UTF-8 encoding so we can process it. Please make sure you write your parse scripts accordingly or we'll probably run into some problems getting it integrated.

The output format from parse.xx depends on the type of content. In any case, it should be a tab delimited file, with one line per entry. Usually there is no need for newline characters, but if there is a need for some reason, escape them with a backslash like \\\n. If you want a newline displayed, use &lt;br&gt;

The output fields are as follows, not all are required to have values, but all must be accounted for in the delimitations. This example is written in simple [Perl](https://duckduckgo.com/Perl).


```perl
# REQUIRED: full article title, e.g. Perl.
# This should be unique across the data set.
my $title = $line[0] || '';

# REQUIRED: 
# A for article.
# D for disambiguation page.
# R for redirect.
my $type = $line[1] || '';

# Only for redirects, e.g. 
# an alias for a title such as
# a common misspelling or AKA.
# For example: Duck Duck Go -> DuckDuckGo.
# The format is the full title of the Redirect, e.g. DuckDuckGo.
my $redirect = $line[2] || '';

# Ignore.
my $otheruses = $line[3] || '';

# You can put the article in multiple categories, and category pages will be created automatically.
# E.g.: http://duckduckgo.com/c/Procedural_programming_languages
# You would do: Procedural programming languages\\n
# You can have several categories, separated by an escaped newline.
# Categories should generally end with a plural noun.
my $categories = $line[4] || '';

# Ignore.
my $references = $line[5] || '';

# You can reference related topics here, which get turned into links in the Zero-click Info box.
# On the perl example, e.g. Perl Data Language
# You would do: [[Perl Data Language]]
# If the link name is different, you could do [[Perl Data Language|PDL]]
my $see_also = $line[6] || '';

# Ignore.
my $further_reading = $line[7] || '';

# You can add external links that get put first when this article comes out.
# The canonical example is an official site, which looks like:
# [$url Official site]\\n
# You can have several, separated by an escaped newline though only a few will be used.
# You can also have before and after text or put multiple links in one like this.
# Before text [$url link text] after text [$url2 second link].\\n
my $external_links = $line[8] || '';

# Ignore.
my $disambiguation = $line[9] || '';

# You can reference an external image that we will download and reformat for display.
# You would do: [[Image:$url]]
my $images = $line[10] || '';

# This is the snippet info.
# It should generally be ONE readable sentence, ending in a period.
my $abstract = $line[11] || '';

# This is the full URL for the source.
# If all the URLs are relative to the main domain, 
# this can be relative to that domain.
my $source_url = $line[12] || '';

In all this may look like:

print "$title\t$type\t\t\t$categories\t\t$see_also\t\t$external_links\t\t$images\t$abstract\t$source_url\n";
```

There is a pre-process script that is run on this output, which:
* drops duplicates (on $title).
* reduces $abstract to one sentence.
* drops records that look like spam.
* normalizes spacing.
* makes sure the $abstract ends in a sentence.


## Code Blocks

If you want to include a code snippet or another pre-formatted example in the abstract, like the [perl](https://duckduckgo.com/?q=perl+open) Fathead, wrap the code block like this:

```html
<pre><code>code block goes here</code></pre>
```

## Notes

There should be no duplicates in the $page (first) variable. If you have multiple things named the same thing you have a number of options:
  - make disambiguation pages
  - put everything in one snippet
  - pick the most general one
