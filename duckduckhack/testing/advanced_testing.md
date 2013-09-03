# Advanced Testing
The [testing triggers](testing.md#testing-triggers) section explained interactive testing. Before going live we also make programmatic tests for each plugin.

**Step 1.** &nbsp;Add your plugin test file.

Make a new file in the test directory **t/**. The name of the file is the name of your plugin, but this time followed by the extension **.t** for test because it is a Perl testing file. For example, if the name of your plugin was _TestPlugin_, the file would be _TestPlugin.t_.

The top of the file reads like a normal Perl script with some use statements to include testing modules, including the DuckDuckGo testing module.

```perl
#!/usr/bin/env perl

use strict;
use warnings;
use Test::More;
use DDG::Test::Goodie;
```

Then you define any default **zci** values that you set in your plugin.

```perl
zci answer_type => 'chars';
zci is_cached => 1;
```

These should match exactly what you set in your **.pm** file.

Next comes the actual testing function.

```
ddg_goodie_test(
        [qw(
                DDG::Goodie::Chars
        )],
        'chars test' => test_zci('Chars: 4'),
        'chars this is a test' => test_zci('Chars: 14'),
);
```

For each test, you include a line like this:

```perl
        'chars test' => test_zci('Chars: 4'),
```

The first part, **'chars test'** in this example, is the test query. The second part, **test_zci('Chars: 4')** calls the test function and checks if **Chars: 4** is the answer.

Finally you end a testing file with this line.

```perl
done_testing;
```

The full file should look like this:

```perl
#!/usr/bin/env perl

use strict;
use warnings;
use Test::More;
use DDG::Test::Goodie;

zci answer_type => 'chars';
zci is_cached => 1;

ddg_goodie_test(
        [qw(
                DDG::Goodie::Chars
        )],
        'chars test' => test_zci('Chars: 4'),
        'chars this is a test' => test_zci('Chars: 14'),
);

done_testing;
```

If you have a long list of queries that need to be tested, you can map over an array or hash inside `ddg_goodie_test`. Remember, this is a Perl program, so we have all the normal tools at our disposal to construct a list to pass to the function.


```perl
#!/usr/bin/env perl

use strict;
use warnings;
use Test::More;
use DDG::Test::Goodie;

zci answer_type => 'time_conversion';
zci is_cached => 1;

ddg_goodie_test(
    [qw(
        DDG::Goodie::UnixTime
    )],
    map {
        "$_ 0" => test_zci('Unix Time Conversion: Thu Jan 01 00:00:00 1970 +0000'),
    }, [ 'unixtime', 'time', 'timestamp', 'datetime', 'epoch', 'unix time', 'unix epoch' ]
);

done_testing;
```



**Step 2.** &nbsp;Test your plugin programmatically.

Run your plugin test file like this:

```txt
perl -Ilib t/Chars.t
```

If successful, you should see a lot of **ok** lines.

```txt
ubuntu@yegg:~/zeroclickinfo-goodies$ perl -Ilib t/Chars.t
ok 1 - Testing query chars test
ok 2 - Testing query chars this is a test
1..2
```

If unsuccessful, you will see one or more **not ok** lines followed with some debugging output to help you chase down the error(s).

```txt
ok 1 - Testing query chars test
not ok 2 - Testing query chars this is a test
#   Failed test 'Testing query chars this is a test'
#   at /usr/local/ddg.cpan/perl5/lib/perl5/DDG/Test/Goodie.pm line 69.
#     Structures begin differing at:
#          $got->{answer} = '14'
#     $expected->{answer} = '15'
1..2
# Looks like you failed 1 test of 2.
```