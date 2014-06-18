# DuckDuckHack FAQ

## General

### Why should I make instant answers?

We hope you will consider making DuckDuckGo instant answers to:

- Improve results in areas you personally search and care about, e.g., [programming documentation](https://duckduckgo.com/?q=perl+split), [gaming](https://duckduckgo.com/?q=roll+3d12+%2B+4) or [entertainment](https://duckduckgo.com/?q=xkcd).
- Increase usage of your own projects, e.g., data and [APIs](https://duckduckgo.com/?q=cost+of+living+nyc+philadelphia).
- Attribution [on our site](https://duckduckgo.com/goodies.html) and [Twitter](https://twitter.com/duckduckhack) (working on more).
- See your code live on a [growing](https://duckduckgo.com/traffic.html) search engine!
- Learn something new.

### What if I'm not a coder at all?

If you don't code at all and you've ended up here, please go over to our [instant answers ideas forum](http://ideas.duckduckhack.com/) where you can suggest and comment on instant answer ideas. For instance, identifying the best sources to draw from is extremely important but not many developers know the best sources, which is where you come in! Similarly, you can submit [issues about current instant answers](https://github.com/duckduckgo/duckduckgo/issues?direction=desc&sort=created&state=open). Both of these activities are very valuable and will help direct community efforts.

If you're a business and want your data to be utilized, adding your service to [ideas.duckduckhack.com](http://ideas.duckduckhack.com) is a great way for your API to get picked up by a developer and integrated into the search engine.

### Can you help me?

Of course! Here are the easiest ways to contact someone who can help answer your questions:

- Write us publicly on the [discussion list](https://www.listbox.com/subscribe/?list_id=197814).
- Write us privately at open@duckduckgo.com.

### What if I don't know Perl?

If you don't know Perl, that's OK! Some instant answer types ([Fathead](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/fathead/fathead_overview.md), [Longtail](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/longtail/longtail_overview.md)) don't require the use of Perl. Also, if you know PHP, Ruby, or Python you should be able to write a [Goodie](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_overview.md) in Perl pretty easily using [this awesome cheat sheet](http://hyperpolyglot.org/scripting).

### Do you have any instant answer ideas?

Yup! We maintain [a growing list](http://ideas.duckduckhack.com/). There are also improvement ideas for [Goodies](https://github.com/duckduckgo/zeroclickinfo-goodies/issues), [Spice](https://github.com/duckduckgo/zeroclickinfo-spice/issues), [Fathead](https://github.com/duckduckgo/zeroclickinfo-fathead/issues) and [Longtail](https://github.com/duckduckgo/zeroclickinfo-longtail/issues).

### How do I note that I've started on something?

In your initial pull request, please note the link on the [idea list](http://ideas.duckduckhack.com/). We'll move it to the "in process" bucket for you.

### Where I can report instant answer bugs?

Submit GitHub issues in the [appropriate repo](http://github.com/duckduckgo).

### What if there are instant answer conflicts?

The ultimate arbiter is the user, and that's the perspective we take. In other words, we ask "what is best for the user experience?" That said, it often makes sense to combine ideas into one, better instant answer.

### Why isn't my instant answer in the [DuckDuckGo Instant Answers API](https://api.duckduckgo.com)?

If your instant answer is spice or longtail, sometimes we can't expose it through the API for licensing reasons (e.g., the WolframAlpha instant answer), but our
over-arching goal is to make all of our instant answers available on their own.

### Can I do something more complicated?

Maybe. There are a bunch more internal interfaces we haven't exposed yet, and we'd love to hear your ideas to influence that roadmap.

### What's the roadmap?

Here's what we're working on (in roughly in this order):

- better testing/file structure for spice instant answers.
- better JS interface for spice instant answer callback functions.
- better attribution.
- embedding instant answers.
- better testing/file structure for fathead instant answers.
- more defined structure for longtail instant answers.
- better testing for longtail instant answers.

### Are there other open source projects? 

Yes! Check out the other repositories in [our GitHub account](https://github.com/duckduckgo). You can email open@duckduckgo.com if you have any questions on those.

### Can I get the instant answers through an API?

Yes! Check out the [DuckDuckGo API](https://api.duckduckgo.com). Our goal is to make as many instant answers as possible
available through this interface. Fathead and goodie instant answers are automatically syndicated through the API, and Spice and Longtail are selectively (due to licensing complications) mixed in.

### Can I talk to you about a partnership idea?###

Sure -- check out [our partnerships page](http://help.duckduckgo.com/customer/portal/articles/775109-partnerships).

## Goodie

### Can Goodie instant answers make network requests?

No. If you are trying to use an API, you should consider creating a Spice instant answer instead.

### Can Goodie instant answers include the user's query string?

Yes. **However**, they must be handled *very* carefully. User-supplied strings create a lot of potential for [cross-site scripting attacks](https://www.owasp.org/index.php/Cross-site_Scripting_%28XSS%29).  While the platform attempts to mitigate these issues in pure ASCII responses, HTML responses should **never** include a raw query string. It is safest to return only data which is generated by your Goodie itself.

## Spice

### I want to use 'X' API, but it doesn't have an endpoint for 'Y'. What should I do?

Email them! - If you explain what it's for, they might be willing to create and endpoint for you! If not, it's probably best to find another API.

### Can I use an API that returns XML?

Sorry, but **no**. We currently don't support XML. We're considering it though...

### Can I use an API that returns HTML or a String? 

If the response is a single string, then yes - you can use `zci wrap_jsonp_callback`. You can read more about that [here](#). Or take a look at the [Automeme](https://github.com/duckduckgo/zeroclickinfo-spice/blob/spice2/lib/DDG/Spice/Automeme.pm#L8) instant answer. If the response is more complicated, then sorry but **no**.

### Can I use the 'X', 'Y' or 'Z' JavaScript library?

Probably not. Maybe, if it is very small, but we prefer that no third party, extra libraries are used. ***Please*** ask us first before writing an instant answer that is **dependent** on an extra library - we don't want you to waste your time and energy on something we can't accept!

### Can I use Coffeescript?

No.

### What about...

Nope. Just use JavaScript, please and thanks :)

## Fathead

### How can I test my output file?

Unfortunately, there is no way for contributors to do so. But if you've gotten that far, we want to hear about it! Please open a pull request and we'll help you through the testing process.

### What can go in a result abstract?

A result abstract can be either plain text (generally one readable sentence, ending in a period), or HTML. Special care needs to be taken when abstracts contain HTML. Please let us know ahead of time if you are planning to use HTML.

(This section is still growing! Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

## Longtail

(This section is coming soon! Know what should go here? Then **please** [contribute to the documentation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/CONTRIBUTING.md)!)

## DuckPAN

### How do I install a missing Perl dependency?

Any Perl module (.pm file) that has external Perl dependencies will load them with a `use` statement. Typically these statements are located near the top of the file. For example, the Factors Goodie (`lib/DDG/Goodie/Factors.pm`) loads the class `Math::Prime::Util`. If this is not installed on your system, DuckPAN will not be able to use the Factors Goodie and you will likely see an error or warning.

In order to install any missing dependencies you can use cpan or cpanm like so:

```perl
cpan install Math::Prime::Util
# or
cpanm Math::Prime::Util
```

Alternatively, if you would like to install all the dependencies for the repo (e.g. zeroclickinfo-goodies), you can run `duckpan installdeps`. Please note that installing all the dependencies will take **several minutes** to install as there are many dependencies.

![dependency](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckpan/assets/dependency.png)
