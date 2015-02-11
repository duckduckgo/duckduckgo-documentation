# Thanks for joining DuckDuckHack!

We are a community of developers and non-developers alike, with a passion for search and privacy, who are helping to make DuckDuckGo and its community a better place. As a developer, we need your help creating and improving the coolest part of our search engine - our Instant Answers!

## What are Instant Answers?


Instant Answers help you find what you're looking for in few or zero clicks. They're placed above ads and regular search results, and they're created/maintained by you (the community). Some Instant Answers are built from pure code and others require external sources (API requests), databases, or key-value stores. The possibilities are endless but the point is to provide a perfect result for every search. 

![App search Instant Answer example](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fapp_search_example.png&f=1)

In the above example, Quixey was a source that our own DuckDuckHack Community suggested for mobile app search. Now, any time someone searches for apps on DuckDuckGo, we can show the Quixey App Search Instant Answer!

## Start

The first step in creating Instant Answers is to let the DuckDuckGo staff and community know that you're getting started. **[Please email us](mailto:open@duckduckgo.com)** to let us know you plan on submitting a new Instant Answer. This will prevent you from wasting time in case your Instant Answer doesn't get approved. Some reasons why your Instant Answer might not get approved include:

 - the Instant Answer already exists
 - the source isn't usable (e.g. paid API, low rate limit, no JSON support)
 - the idea needs more thought or planning
 - the developer is incorrectly implementing design.

Here's an example email to help you out:

```text
To: open@duckduckgo.com
Subject: Instant Answer Approvals

I'd like to make an Instant Answer for <topic/subject>!
This is the data source: <link, description, Perl module, etc.>.
This is the related Duck.co idea: <url, if applicable>.
This is my Github username: <username>.

Thanks!

PS: DuckDuckGo is awesome!
```

We'll try and get back to you as soon as possible (ideally within 24hrs). We ask that you wait to hear back from us before moving ahead unless you're absolutely sure this Instant Answer is acceptable (i.e. a duck.co idea that has been approved by DDG staff). 

**One more thing:** Please consider joining our [The DuckDuckHack Developer Mailing List](https://www.listbox.com/subscribe/?list_id=197814) to stay in tune with the important updates happening among the community. 

If you're confident that you can figure things out along the way, you're welcome to carry on, but please be patient as we assist others in the community who need a bit more help. 

If you're new to programming, you can try out the quick-start [guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_quickstart.md) which creates an Instant Answer like [this](https://duckduckgo.com/?q=duckduckhack+zekiel&ia=answer) with your username. It's not exactly an "Instant Answer" but does give you the basic idea of what's involved in the creation process, so you can go on to make something more spectacular.  


## Creating Your Own Instant Answer

After getting approval, you'll need to [determine your Instant Answer back-end type](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/getting-started/determine_your_instant_answer_type.md).
