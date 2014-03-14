# Location API

Some instant answers need the user's location to provide the most relevant results. For example, since weather conditions vary the world over, the [Is it snowing?](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Snow.pm) instant answer depends on knowing where the user is located.

The [core DDG package](https://github.com/duckduckgo/duckduckgo) provides a Location API. Since Goodie and Spice instant answers inherit from this package, their `handle` functions have access to a `$loc` variable which refers to a [Location object](https://github.com/duckduckgo/duckduckgo/blob/master/lib/DDG/Location.pm).

This Location object has a number of [useful attributes](https://github.com/duckduckgo/duckduckgo/blob/master/lib/DDG/Location.pm#L6) to help you provide revelant answers:

```perl
my @geo_ip_record_attrs = qw( country_code country_code3 country_name region
    region_name city postal_code latitude longitude time_zone area_code
    continent_code metro_code );
```

Example data from `$loc`:

```perl
country_code   => US
country_code3  => USA
country_name   => United States
region         => PA
region_name    => Pennsylvania
city           => Phoenixville
postal_code    => 19460
latitude       => 40.1246
longitude      => -75.5385
time_zone      => America/New_York
area_code      => 610
continent_code => NA
metro_code     => 504
```

When testing instant answers interactively with `duckpan`, the location will always point to "Phoenixville, Pennsylvania, United States":

```perl
# Phoenixville, Pennsylvania, United States
my $location = join(", ", $loc->city, $loc->region_name, $loc->country_name);
```

For assistance with setting the location to be used in automated testing, please refer to the guide to [testing with the Location API](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/testing_location_api.md).

Naturally, once your instant answer is live, `$loc` will refer to the appropriate location.
