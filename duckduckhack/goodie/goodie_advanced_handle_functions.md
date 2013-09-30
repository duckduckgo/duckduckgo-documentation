# Advanced Handle Functions

In the [Basic tutorial](general.md#basic-tutorial) we walked through a simple query transformation and in the [Spice handle functions](spice.md#spice-handle-functions) section we walked through a simple return of the query.

Here are some more advanced handle techniques you may need to use:

## Further Qualifying the Query

Trigger words are blunt instruments; they may send you queries you cannot handle. As such, you generally need to further qualify the query (and return nothing in cases where the query doesn't really qualify for your goodie).

There are number of techniques for doing so. For example, the first line of [Base Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Base.pm) has a return statement paired with unless.

```perl
return unless  /^([0-9]+)\s*(?:(?:in|as)\s+)?(hex|hexadecimal|octal|oct|binary|base\s*([0-9]+))$/;
```

You could also do it the other way, like the [GoldenRatio Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GoldenRatio.pm).

```perl
if ($input =~ /^(?:(?:(\?)\s*:\s*(\d+(?:\.\d+)?))|(?:(\d+(?:\.\d+)?)\s*:\s*(\?)))$/) {
```

Another technique is to use a hash to allow specific query strings, as the [GUID Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/GUID.pm) does.

```
my %guid = (
    'guid' => 0,
    'uuid' => 1,
    'globally unique identifier' => 0,
    'universally unique identifier' => 1,
    'rfc 4122' => 0,
    );

return unless exists $guid{$_};
```

## Handling the Whole Query

In the Chars example, we handled the **remainder**. You can also handle:

* **query_raw** - the actual (full) query
* **query** - with extra whitespace removed
* **query_parts** - like query but given as an array of words
* **query_nowhitespace** - with whitespace totally removed
* **query_nowhitespace_nodash** - with whitespace and dashes totally removed

For example, the [Xor Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Xor.pm) handles query_raw and the [ABC Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/ABC.pm) handles query_parts.

Using files**. You can use simple text/html input files for display or processing.

```perl
# IO should always be done outside of the handle function
my @words = share('words.txt')->slurp;
```

The [Passphrase Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Passphrase.pm) does this for processing purposes and the [PrivateNetwork Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/PrivateNetwork.pm) does it for display purposes.

The files themselves go in the **/share/goodie/** directory.

## Generating Data Files

You may also need to generate data files. If you do so, please also include the generation scripts. These do not have to be done in Perl, and you can also put them within the **/share/goodie/** directory. For example, the [CurrencyIn Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/currency_in) uses a Python script to generate the input data.


There are a couple more sections on advanced handle techniques depending on [Plugin type](#overview):

* For **Goodies**, check out the [Advanced Goodies](https://github.com/duckduckgo/zeroclickinfo-goodies#advanced-goodies) section.
* For **Spice**, check out the [Advanced Spice handlers](https://github.com/duckduckgo/zeroclickinfo-spice#advanced-spice-handlers) section.