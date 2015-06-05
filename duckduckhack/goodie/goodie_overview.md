## Goodie Instant Answers

**If you have questions about Goodies, ask our [Goodie Chat room](https://gitter.im/duckduckgo/zeroclickinfo-goodies)**  

Goodies are pure-code Instant Answers. They are essentially a Perl function that is evaluated on our servers, and do not make external HTTP requests to other services.

Goodies can be extremely simple, such as the [Uppercase](https://duckduckgo.com/?q=uppercase+duckduckgo+instant+answers) Goodie, which simply uses the perl `uc` function to uppercase a string. 

Goodies can also be extremely complex and powerful such as the [Calculator](https://duckduckgo.com/?q=%28879+*+14%29+%2F+12) or [Timezone Converter](https://duckduckgo.com/?q=4pm+EST+to+GMT) Goodies. Contributors have used Goodies to do additional cool things like [generate passwords](https://duckduckgo.com/?q=password+15+strong&ia=answer) and [create QR codes](https://duckduckgo.com/?q=qr+duckduckhack.com&ia=answer).

If you're new to DuckDuckHack or Perl, writing a simple Goodie Instant Answer is probably the quickest and easiest way to get started with DuckDuckHack. The Goodie [Quick Start Tutorial](https://duck.co/duckduckhack/goodie_quickstart) was created to help you dive right in.

## Important Goodie Criteria

- Goodies ***cannot* make HTTP requests**. If it's better served by an external API, it should probably be a [Spice Instant Answer](https://duck.co/duckduckhack/spice_overview).
- Goodies should return an answer in **less than 10ms**. Execution times between 10-50ms require review by the community. Goodies which run longer than 50ms will not be accepted.
- Goodies should use **less than 1MB** in memory. Memory usage greater than 1MB will require review by the community.

Most Goodies shouldn't have a problem, but if you think your idea might run into these constraints, we're happy to help you think through it. Feel free to email us at [open@duckduckgo.com](mailto:open@duckduckgo.com).
