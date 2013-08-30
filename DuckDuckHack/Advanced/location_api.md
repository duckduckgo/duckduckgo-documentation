# Location API

Sometimes, a plugin needs the user's location. This is where the Location API comes in. An example is the [Is it snowing?](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Snow.pm) plugin. Before reading this, you should be familiar with the genereal workings of your plugin type.

The Location API is implemented by [DuckDuckGo](https://github.com/duckduckgo/duckduckgo), which is a package used by Plugins. When testing Plugins interactively with `duckpan`, the location will always point to "Phoenixville, Pennsylvania, United States," but don't worry - it will show the real location once it's live.

Inside the handlers of Goodies and Spice, the `$loc` variable refers to a Location object that can be accessed. Here's the code that the [Is it snowing?](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Snow.pm) Spice is using to read the location.

```perl
# Phoenixville, Pennsylvania, United States
my $location = join(", ", $loc->city, $loc->region_name, $loc->country_name);
```

It isn't limited to just the city, the state, and the country. [Location.pm](https://github.com/duckduckgo/duckduckgo/blob/master/lib/DDG/Location.pm#L6) lists all the things that you can possibly use:

```perl
my @geo_ip_record_attrs = qw( country_code country_code3 country_name region
    region_name city postal_code latitude longitude time_zone area_code
    continent_code metro_code );
```

Sample contents of `$loc`:

```perl
longitude => -75.5385
country_name => United States
area_code => 610
region_name => Pennsylvania
country_code => US
region => PA
continent_code => NA
city => Phoenixville
postal_code => 19460
latitude => 40.1246
time_zone => America/New_York
metro_code => 504
country_code3 => USA
```