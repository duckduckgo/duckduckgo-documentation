# DuckPAN

**The DuckDuckHack Developer Tool**

DuckPAN is an application built to aid DuckDuckHack developers. It is mainly used to generate the required files for new Instant Answers (the developer must implement functionality) and also test both the triggering and visual display of Instant Answers.

**Currently the DuckPAN tool only supports Goodie and Spice Instant Answers.**

## Getting Started Using Codio

Codio is a super quick and easy way to launch the DuckDuckHack development environment.

Codio provides a web-based development environment that you will be using to create and test a new Instant Answer. Codio works across all platforms (Windows, Linux, Mac) and comes pre-configured with the necessary software for Instant Answer development.

1. Create an account on [Codio](https://codio.com/).

2. Go to https://codio.com/duckduckgo/duckduckhack and fork the project. Make sure to fork the project and the box.

![Codio Fork](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckpan%2Fassets%2Fcodio_fork.png&f=1)

![Codio Fork Both](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckpan%2Fassets%2Fcodio_fork_both.png&f=1)

3. Visit one of our Instant Answer repositories (such as https://github.com/duckduckgo/zeroclickinfo-spice), and follow GitHub's instructions to first [fork](https://help.github.com/articles/fork-a-repo) the repository. You can then clone the repo into your Codio machine (You need to open the Terminal for this).

![Codio Terminal](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckpan%2Fassets%2Fcodio_terminal.png&f=1)

4. Go into the directory (by typing in `cd zeroclickinfo-spice`) and run `duckpan server`. Click on "DuckPAN Server" to view the webpage.

![Codio Server](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckpan%2Fassets%2Fcodio_server.png&f=1)

5. You're all set!

![Codio Success](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckpan%2Fassets%2Fcodio_success.png&f=1)

Try typing in queries like "define hello," and see if it works for you. 

*You might be wondering why there are no search results in the page. It's because DuckPAN isn't configured to work with search results - it's only for testing Instant Answers.*

## Using DuckPAN

Running `$ duckpan` with no commands will output some help information. More details on the DuckPAN commands can be found in the [DuckPAN Readme](https://github.com/duckduckgo/p5-app-duckpan#using-duckpan).

The [next section](https://duck.co/duckduckhack/testing_triggers) will show you how to use DuckPAN to interactively test your triggers.
