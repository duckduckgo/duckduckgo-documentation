# Advanced Handle Functions

## Further Qualifying the Query

Trigger words are coarse filters; they may send you queries you cannot handle. Your Instant Answer should return nothing in these cases.  As such, you generally need to further qualify the query in your code.

There are many techniques for doing this qualification.  One of the most popular is to `return` as soon as a query can be disqualified.

As an example, the [Base Goodie's](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Base.pm) has a `return` statement paired with an `unless` right on the first line of its `handle` function:

```perl
handle remainder => sub {
  return unless  /^([0-9]+)\s*(?:(?:in|as)\s+)?(hex|hexadecimal|octal|oct|binary|base\s*([0-9]+))$/;
  ...
}
```

## Using Structured Responses

Most Goodies essentially take some input and provide output based from it. One example is the [Calculator Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Calculator.pm).

As this is often used, Goodies can return a structured answer which will always be displayed in a consistent way between goodies. A simple example is as follows:

```perl
return "Text output",
  structured_answer => {
    input     => "What the input was, usually highlighting how it has been parsed",
    operation => "What has been perfomed, for example 'calculate' or 'convert'",
    result    => "The actual output or answer to the input query",
};
```

Realistic examples are scattered through the Goodie Repository:
 * [Calculator](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Calculator.pm#L155...L162)
 * [GUID](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GUID.pm#L47..L52)
 * [URLDecode](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/URLDecode.pm#L45..L50)

## Using Files in the Share Directory

Goodies can use simple text or html input files for display or processing. These files can be read once and reused to answer many queries without cluttering up your source code.

The `share` function gives each Instant Answer access to a subdirectory of the repository's `share` directory. The subdirectory for your Instant Answer is based on its Perl package name which is transformed from CamelCase to underscore_separated_words. For example the [Passphrase Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Passphrase.pm) uses the `share` directory to hold data for processing purposes:

```perl
my @words = share('words.txt')->slurp;
```

Here the `share` function grabs the `words.txt` file, found in `zeroclickinfo-goodies/share/goodie/passphrase/`. The returned object's `slurp` method is called which pushes each line of the file into the `@words` array.

In another case, the [PrivateNetwork Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/PrivateNetwork.pm) uses its `share` directory to hold files for display purposes:

```perl
my $text = scalar share('private_network.txt')->slurp,
my $html = scalar share('private_network.html')->slurp;

handle sub {
    $text, html => $html;
};
```

Here each file is grabbed from `share/goodie/private_network/` and `slurp`ed in a `scalar` context. This returns the entire file as a **string** and assigns it to the appropriate variable. In the `handle` function, `$text` and `$html` are returned to display as plain text or HTML Instant Answer.

One further consideration is whether your data file contains non-ASCII characters. If so, you will want to prepare the file with UTF-8 encoding.  The [Shortcut Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Shortcut.pm) uses a UTF-8 data file:

```perl
my @shortcuts = share('shortcuts.csv')->slurp(iomode => '<:encoding(UTF-8)');
```

As with the Passphrase Goodie example above, each line becomes an entry in the resulting array. With this `iomode` set, the UTF-8 characters used to denote system-specific keys will be handled properly throughout the rest of the processing.

## Generating Data Files

In some cases, you may need to generate the data files you will `slurp` from the share directory. If so, please put the required generation scripts in the Goodie's `share` directory. While **shell scripts are preferred**, your scripts can be written in the language of your choice.

As an example, the [CurrencyIn Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/currency_in) uses a [combination of Shell and Python scripts](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/currency_in) to generate its input data, `currency.txt`.

## Stylesheets

Goodies not using structured answers can use custom stylesheets from the `share` directory. A `.css` with the same filename as the directory is automatically included along with the Goodie's output. For example, the [DDG::Goodie::RegexCheatSheet package](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/RegexCheatSheet.pm) uses the directory [share/goodie/regex_cheat_sheet] and has an automatically included stylesheet (https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/regex_cheat_sheet/regex_cheat_sheet.css).
