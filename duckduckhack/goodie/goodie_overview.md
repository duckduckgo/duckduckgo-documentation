## Goodie Instant Answers

**If you have questions, [request an invite to our Slack team](mailto:QuackSlack@duckduckgo.com?subject=AddMe) and we'll be happy to chat!** 

Goodies are pure-code Instant Answers. They are essentially a Perl function that is evaluated on our servers, and do not make external HTTP requests to other services.

Goodies can be extremely simple, such as the [Uppercase](https://duckduckgo.com/?q=uppercase+duckduckgo+instant+answers) Goodie, which simply uses the perl `uc` function to uppercase a string. 

Goodies can also be extremely complex and powerful such as the [Calculator](https://duckduckgo.com/?q=%28879+*+14%29+%2F+12) or [Timezone Converter](https://duckduckgo.com/?q=4pm+EST+to+GMT) Goodies. Contributors have used Goodies to do additional cool things like [generate passwords](https://duckduckgo.com/?q=password+15+strong&ia=answer) and [create QR codes](https://duckduckgo.com/?q=qr+duckduckhack.com&ia=answer).

### Goodie Quick Start

If you're new to DuckDuckHack or Perl, writing a simple Goodie Instant Answer is probably the quickest and easiest way to get started with DuckDuckHack. The Goodie [Quick Start Tutorial](https://duck.co/duckduckhack/goodie_quickstart) was created to help you dive right in.

The [Goodie Quick Start](https://duck.co/duckduckhack/goodie_quickstart) is a hands-on, simple way to understand the Goodie framework, going from zero to a working Instant Answer. It's the best preparation for contributing to DuckDuckHack.

### Create a Goodie Cheat Sheet

A popular use of Goodies is creating cheat sheet Instant Answers - for example, a cheat sheet for [vim](https://duckduckgo.com/?q=vim+cheat+sheet&ia=answer) or [tmux](https://duckduckgo.com/?q=tmux+cheat+sheet&ia=answer). We've made it exceptionally quick and easy to [contribute a Cheat Sheet](https://duck.co/duckduckhack/goodie_cheat_sheets) by adding a single file to the repository. 

![vim cheat sheet](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvim_cheat_sheet.png&f=1)

Goodie Cheat Sheets are the quickest way to make a live contribution, and a great place to get started. Learn more about [adding your Goodie Cheat Sheet](https://duck.co/duckduckhack/goodie_cheat_sheets).

## Important Goodie Criteria

- Goodies ***cannot* make HTTP requests**. If it's better served by an external API, it should probably be a [Spice Instant Answer](https://duck.co/duckduckhack/spice_overview).
- Goodies should return an answer in **less than 10ms**. Execution times between 10-50ms require review by the community. Goodies which run longer than 50ms will not be accepted.
- Goodies should use **less than 1MB** in memory. Memory usage greater than 1MB will require review by the community.

Most Goodies shouldn't have a problem, but if you think your idea might run into these constraints, we're happy to help you think through it. Feel free to email us at [open@duckduckgo.com](mailto:open@duckduckgo.com).

## Let Us Know What You're Working On

**Before you start coding your new Instant Answer, let us know your plans.** By involving us early we can provide guidance and potentially save you a lot of time and effort. 

Email us at [open@duckduckgo.com](mailto:open@duckduckgo.com) with what idea you're working on and how you're thinking of going about it.
