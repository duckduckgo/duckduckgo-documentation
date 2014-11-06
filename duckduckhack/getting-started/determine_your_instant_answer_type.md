# Determine Your Instant Answer Type

Most Instant Answers rely on some type of data source (e.g. database, textfile, API) to provide their answer. Others however, are able to provide their answer through the use of pure code, like a pre-existing Perl package on CPAN or simply a script you write (e.g. a string manipulation function).

The following flowchart will help you to determine what type of Instant Answer you'll be creating, which is based on your Instant Answer's date source:

![Instant Answer type flow chart](https://raw.github.com/duckduckgo/duckduckgo-documentation/master/duckduckhack/assets/instant_answer_flowchart.png)

<!-- /summary -->

If you were able to determine your Instant Answer type, then [continue below](#fork-the-instant-answer-repository)!

If the right Instant Answer type is still not obvious, don't worry, the DuckDuckGo Community is here for you! Please visit our [Instant Answer Ideas Forum](https://dukgo.com/ideas) and post a new thread for your Instant Answer. Be sure to describe the Instant Answer you have in mind, and don't forget to indicate where you think the data should come from. Someone from the community or the DuckDuckGo staff will be able to help you determine the best course of action for you.

**\*\*Note:** Sometimes more than one Instant Answer type can work (depending on the data source), and we can help you figure out which one would work best.

Before moving forward, you **must** know which Instant Answer type you will be using. From this point onwards, the documentation will be specific to each Instant Answer type.

## Fork the Instant Answer Repository

Now that you know which Instant Answer type you'll be using for your Instant Answer, you'll have to fork the associated DuckDuckHack Instant Answer repository ([GitHub instructions](http://help.github.com/fork-a-repo/)) so you can start coding. If you don't already have a GitHub account, please [signup](https://github.com/signup/free) now. This is required because we use GitHub to handle all incoming *Pull Requests* (code modifications) and *Issues* (bug reports) which cannot be made without a GitHub account.

Once you have an account, please fork the appropriate repository:

- For **Goodies**, [click here](https://github.com/duckduckgo/zeroclickinfo-goodies/fork)

- For **Spice**, [click here](https://github.com/duckduckgo/zeroclickinfo-spice/fork)

- For **Fathead**, [click here](https://github.com/duckduckgo/zeroclickinfo-fathead/fork)

- For **Longtail**, [click here](https://github.com/duckduckgo/zeroclickinfo-longtail/fork)

## Give Us a Heads Up

We know you're eager to get started, and we're super excited to see your awesome Instant Answer creations! Before you start coding up a storm though, **please send us an email** (open@duckduckgo.com) to let us know that you plan on submitting a new Instant Answer. We suggest you do this to save you from wasting time in case your Instant Answer doesn't get approved. Reasons why your Instant Answer might not get approved include:

 - the Instant Answer already exists
 - the source isn't usable (e.g. paid API, low rate limit, no JSON support)
 - the idea needs more thought or planning

Here's an example email to help you out:

```text
To: open@duckduckgo.com
Subject: Instant Answer Approvals

I'd like to make an Instant Answer for \<topic/subject\>!
This is the data source: \<link, description, Perl module, etc.\>.
This is the related Duck.co idea: \<url, if applicable\>.
This is my Github username: \<username\>.

Thanks!

PS: DuckDuckGo is awesome!
```

We'll try and get back to you as soon as possible (ideally within 24hrs). We ask that you wait to hear back from us before moving ahead unless you're absolutely sure this Instant Answer is acceptable (i.e. a duck.co idea that has been approved by DDG staff).

## Start Coding!

At this point, you're ready to start learning about the Instant Answer type you'll be using.

- For **Goodies**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_overview.md)

- For **Spice**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_overview.md)

- For **Fathead**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/fathead/fathead_overview.md)

- For **Longtail**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/longtail/longtail_overview.md)
