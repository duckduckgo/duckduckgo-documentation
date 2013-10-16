# Advanced Handle Functions

## Further Qualifying the Query

Trigger words are blunt instruments; they may send you queries you cannot handle. As such, you generally need to further qualify the query (and return nothing in cases where the query doesn't really qualify for your instant answer)

There are number of techniques for doing so. For example, the first line of the [Base Goodie's](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Base.pm) `handle` function has a `return` statement paired with an `unless`:

```perl
handle remainder => sub {
  return unless  /^([0-9]+)\s*(?:(?:in|as)\s+)?(hex|hexadecimal|octal|oct|binary|base\s*([0-9]+))$/;
  ...
}
```

You could also do it another way, like the [GoldenRatio Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GoldenRatio.pm) which uses an `if` block and a regex to make sure the query qualifies:

```perl
handle remainder => sub {
  my $input = $_;
  if ($input =~ /^(?:(?:(\?)\s*:\s*(\d+(?:\.\d+)?))|(?:(\d+(?:\.\d+)?)\s*:\s*(\?)))$/) {
    ...
  }
  return;
}
```

## Using Files in the Share Directory

You can use simple text/html input files for display or processing. The Perl `share` function allows each instant answer access to its own directory in the `share` directory of the repository.

The [Passphrase Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Passphrase.pm) does this for processing purposes: 

```perl
my @words = share('words.txt')->slurp;
```

Here, we use the `share` function to grab the `words.txt` file, found in `zeroclickinfo-goodies/share/goodie/passphrase/`. This returns to us an object which we then use the `slurp` method on, which pushes each line of the file into our `@words` array.

Similarly, the [PrivateNetwork Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/PrivateNetwork.pm) does it for display purposes:

```perl
my $text = scalar share('private_network.txt')->slurp,
my $html = scalar share('private_network.html')->slurp;

handle sub {
    $text, html => $html;
};
```

Here, we are grabbing each of these files from `zeroclickinfo-goodies/share/goodie/private_network/` and `slurp`ing them in a `scalar` context, which returns the entire file as a **string** into our `$text` and `$html` variables. Then, in the `handle` function we are returning `$text` and `$html` which will be used to display with a plaintext or HTML instant answer.

## Generating Data Files

In some cases, you may need to generate the data files you will `slurp` from the share directory. If this is the case, please put the required generation scripts (**shell scripts** are preffered) into the appropriate **/share/goodie/<ia_name>** directory. These generation/parsing scripts do not have to be written in Perl, they can be any language you prefer. For example, the [CurrencyIn Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/currency_in) uses a combination of Shell and Python scripts to generate its input data, `currency.txt`. These scripts can be found inside CurrencyIn Goodie's [share directory](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/currency_in).