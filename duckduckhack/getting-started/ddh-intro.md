# Welcome to DuckDuckHack!

We are a community of developers (and non-developers) who share a passion for search and privacy. Through DuckDuckHack, we're helping to make DuckDuckGo better and develop the community that powers it. Whether you're an experienced developer or are just getting started, we need your help to create and improve the coolest part of our search engine - Instant Answers!

## What is an Instant Answer?

An Instant Answer helps you find the information you're looking for in zero (_or few_) clicks. They appear above ads and regular search results. An Instant Answer aims to answer your search query directly, ideally without the need to click through to another site.

Instant Answers are created and maintained by the community - that means you! Some Instant Answers get their information from pure code and others require external sources such as API requests, databases or key-value stores. 

Lets illustrate with an example:

![App search Instant Answer example](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fapp_search_example.png&f=1)

Quixey was a source that the DuckDuckHack Community suggested for mobile app search. Now, whenever someone searches for apps on DuckDuckGo, they see the Quixey App Search Instant Answer. 

DuckDuckGo already includes thousands of Instant Answers, including word definitions, calculations, movies and music. The possibilities are endless - by building a comprehensive range of Instant Answers we aim to provide a conclusive result for every search.

## Want to Make an Instant Answer?

Great! To get started, first ask yourself what it will do:

- What will the user search for?
- What information will it return?
- Where will the information come from?
- What will it look like?

Before you start working on your Instant Answer - get in touch either via email [open@duckduckgo.com](mailto:open@duckduckgo.com) or in the [forum](https://duck.co/ideas). Each Instant Answer is a collaborative effort between you and staff/ community members, so keep talking!

You can see discussions on ideas for Instant Answers in the [forum](https://duck.co/ideas) - feel free to get involved there or to get in touch about starting work a forum idea that doesn't have a developer working on it yet.

**Make sure you discuss your Instant Answer before you dedicate any time to working on it**, in case there's some reason it might not work or there's something you need to bear in mind before developing it. For example:
 - your Instant Answer might already exist, or someone else might be working on it
 - your planned source might not be suitable (e.g. paid API, low rate limit, no JSON support)
 - your idea or design might need a bit more thought or planning

Here's an example email to help you out:

```text
To: open@duckduckgo.com
Subject: Instant Answer Suggestions

I'd like to make DuckDuckGo even more awesome with a new Instant Answer!

When the user searches for <user search term(s)>,
It will display <info displayed>.
The data will come from <data source e.g. API link, description, Perl module etc>(if applicable).
It comes from this Duck.co idea: <url>(if applicable).
This is my Github username: <username>(if applicable).

Looking forward to getting started on it!
```

We'll try and get back to you as soon as possible (ideally within 24hrs). Unless you know the idea has already been discussed and approved, wait until you hear back from us before moving ahead - that way you won't waste any of your own time! 

**Keep up to date:** Please consider joining our [The DuckDuckHack Developer Mailing List](https://www.listbox.com/subscribe/?list_id=197814) to stay in tune with what's happening the community.

The DuckDuckHack staff and community are keen to support anyone who wants to make a contribution, regardless of development experience. We take the time to provide whatever assistance contributors need to get involved. If you are an experienced developer and want to get stuck in, bear with us as we do this - for the same reason you are encouraged to provide help and guidance to other contributors if you're in a position to do so!

If you're new to programming or the DuckDuckHack project, check out the [Quick Start guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_quickstart.md) - it creates an Instant Answer that testifies to your awesomeness! ([See this example](https://duckduckgo.com/?q=duckduckhack+zekiel&ia=answer), yours will appear with your own username. _Although it doesn't create a "real" Instant Answer it will famliarize you with the development process - then you can make something more spectacular._)

## Creating Your Instant Answer

Once you hear back about your idea, use the flowchart to [determine your Instant Answer back-end type](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/getting-started/determine_your_instant_answer_type.md). Instant Answers are categorized as **Goodie**, **Spice**, **Fathead** and **Longtail** depending on where they get their information.

A great way to famliarize yourself with the structure and detail of an Instant Answer is to have a good look around the GitHub repos:
 - [Goodie Repo](https://github.com/duckduckgo/zeroclickinfo-goodies)
 - [Spice Repo](https://github.com/duckduckgo/zeroclickinfo-spice)
 - [Fathead Repo](https://github.com/duckduckgo/zeroclickinfo-fathead)
 - [Longtail Repo](https://github.com/duckduckgo/zeroclickinfo-longtail)

If you get stuck or are unsure about any aspect of the process at any stage of your Instant Answer development - give us a shout via [email](mailto:open@duckduckgo.com), in the [forum](https://duck.co/ideas), on GitHub (in the relevant repo) or on IRC (on irc.freenode.net in the channel #duckduckgo)!
