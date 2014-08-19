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
$output = $styler->for_computation($perl_number);
```


### Date Parsing


### HTML Encoding

