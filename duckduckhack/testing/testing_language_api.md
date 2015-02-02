## Testing with the Language API

To write a test for a locale-aware Instant Answer, you'll need to pass the test function an extra parameter - a `DDG::Request` object, with the location specified. To do this, you'll need to `use DDG::Test::Language` and `use DDG::Request`. Here is a quick annotated example testing the language detect feature of the [Translate](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Translate/Detect.pm) Instant Answer:

```perl
#!/usr/bin/env perl

use strict;
use warnings;
use Test::More;
use DDG::Test::Spice;

# These two modules are only necessary when testing with the Language API.
use DDG::Test::Language;
use DDG::Request;

ddg_spice_test(
    ["DDG::Spice::Translate::Detect"],
    # This optional argument to ddg_spice_test is a DDG::Request oject.
    # The two arguments we pass to the constructor are:
    # the query we're testing against
    # language object, created by calling test_language with a country code

    # Note that the only supported values for test_language are:
    # "us" (US English), "de" (German) and "my" (Malay)
    DDG::Request->new(
        query_raw => "translate good",
        language => test_language("de"),
    ), test_spice(
        '/js/spice/translate/detect/good/de',
        caller => "DDG::Spice::Translate::Detect"
    )
);

done_testing;
```
