# Determine Your Instant Answer Type

## Choose an Instant Answer

Before you can start working on an instant answer, you'll need to know what kind of instant answer it is that you want to work on. You can get some instant answer ideas on our [ideas forum](https://dukgo.com/ideas).

## What kind of data source?

Most instant answers rely on some type of data source. The [weather](https://duckduckgo.com/?q=weather) instant answer, for example, needs to fetch data from [Forecast.io](http://forecast.io) to work. However not all of them need a data source to work. Some can be self-contained instant answers such as our [resistor color calculator](https://duckduckgo.com/?q=60+ohms).

Please use the following flowchart to help you to determine which kind of instant answer you'll be creating. Your instant answer type will be based on the date source your instant answer will be using:

![instant answer type flow chart](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/instant_answer_flowchart.png)

If you were able to determine which instant answer type you will be using, please continue below to fork the repository so you can begin coding!

If the right instant answer type is still not obvious, don't worry. The DuckDuckGo community is here for you! Please visit our [instant answer idea forum](https://dukgo.com/forum) and post a new thread for your instant answer. Be sure to describe the instant answer you have in mind, and don't forget to indicate where you think the date should come from. Someone from the community or the DuckDuckGo team will be able to help you determine the best course of action for you.

**Note:** Sometimes more than one instant answer type can work (depending on the data source), and we can help you figure out which one would work best. As always, you can reach us in the [forum](https://dukgo.com/forum), the [DuckDuckHack e-mail list](https://www.listbox.com/subscribe/?list_id=197814), or you can chat with us on our [IRC channel](http://webchat.freenode.net/?channels=duckduckgo).

Before moving forward, you **must** know which instant answer type you will be using. From this point onwards, the documentation will be specific to each instant answer type.

## Fork the Instant Answer Repository

**Hang on:** We're going to be using a piece of software called Git here. If you're not familiar with it, you can learn more about it on [Try Git](http://try.github.com/). When you're done with that, you can start [setting up Git](https://help.github.com/articles/set-up-git) on your computer.

Now that you know the instant answer type that you'll be using, you'll have to fork the right repository that you're going to work on ([GitHub instructions](http://help.github.com/fork-a-repo/)) so you can start coding. You'll need a GitHub account for this one. This is required because we use GitHub to handle all incoming *Pull Requests* (code modifications) and *Issues* (bug reports) which cannot be made without a GitHub account.

Once you have an account, please fork the appropriate repository:

- [**Goodies**](https://github.com/duckduckgo/zeroclickinfo-goodies/)

- [**Spice**](https://github.com/duckduckgo/zeroclickinfo-spice/)

- [**Fathead**](https://github.com/duckduckgo/zeroclickinfo-fathead/)

- [**Longtail**](https://github.com/duckduckgo/zeroclickinfo-longtail/)

## Start Coding!

At this point, you should be ready to start learning about the instant answer type you'll be using:

- For **Goodies**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_overview.md)

- For **Spice**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_overview.md)

- For **Fathead**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/fathead/fathead_overview.md)

- For **Longtail**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/longtail/longtail_overview.md)
