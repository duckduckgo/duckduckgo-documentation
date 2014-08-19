## Goodie Helpers

A few commonly used things are wrapped up into useful helpers that can be easily used by any goodie. These are implemented as "roles" that can be used by using `with 'DDG::GoodieRole::RoleName'`

### Numbers

Often matching and outputting numbers intelligently is required, for this the NumberStyler role is ideal:
```
with 'DDG::GoodieRole::NumberStyler';
# get the regex for something that "looks like a number"
my $number_re = number_style_regex();
my $number_string = qr/($number_re)/;

# get an object that can handle the number
my $styler = number_style_for($number_string);
return unless $styler;  # might not be supported

my $perl_number = $styler->for_computation($number_string);
# now you can use $perl_number however you want

$perl_number *= 2;

# when you're ready for output simply use:
$output = $styler->for_display($perl_number);
```

To aid with ambiguity `number_style_for()` can also take an array to parse as a set:
```
my @numbers = qw(123,450 543.43);
my $styler = number_style_for(@numbers);
```
### Date Parsing

Dates are especially complicated as different cultures use different formats; to this end we have the Date role, a simple usage of which is:
```
with 'DDG::GoodieRole::Dates';

# get the regex for something that "looks like a date"; this doesn't mean it *is* a valid date
my $date_regex = date_regex();

my $probable_date = qr/($date_regex)/i;
# returns a DateTime object or undef if the date is invalid
my $parsed_date = parse_string_to_date($probable_date);
return unless $parsed_date;

# do something with $parsed_date
$parsed_date->add( days => 1 );

# output in the standard format
$output = date_output_string($parsed_date);
```
To aid in distinguishing amiguous formats (such as 01/02/2003) multiple strings can be parsed collectively as one format like so:
```
my @date_strings = qw(01/02/2001 02/13/2002);

# by parsing as below, it will understand the user meant 2nd Jan 2001 and 13th Feb 2002
my @date_objects = parse_all_strings_to_date(@date_strings);
```

Also available for use are:
* `full_month_regex()` - matches full month names, i.e. January
* `short_month_regex()` - matches short month names. i.e. Feb
* `month_regex()` - matches either short or full month names
* `full_day_of_week_regex()` -  maches full weekday i.e. Wednesday
* `short_day_of_week_regex()` - matches short weekday i.e. Thu
* `parse_string_to_date()` - Returns a `DateTime` of the string when in `date_regex()` format or `undef` if the date is invalid
* `parse_vague_string_to_date()` - Takes a string like "next december" and produces the first of the month
* `date_output_string()` - Takes a DateTime object (or a string which can be parsed into one) and returns a standard formatted output string or an empty string if it cannot be parsed.
 

### HTML Encoding

In all situations when the querystring is output as html, it *must be encoded*; this is important for protection from XSS (cross site scripting) attacks. There is a handy helper available for goodies in the form of:

```
# simple scalar:
my $safe_to_output = html_enc($query_string);

# also takes an array:
my @safe_strings = html_enc(@unsafe_strings);

```
