# Thanks for joining DuckDuckHack!

We are a community of developers and non-developers with a passion for search and privacy. We're helping to make DuckDuckGo and its community a better place by improving the coolest part of our search engine - the Instant Answers!

## What are Instant Answers?

Instant Answers help you find what you're looking for in few or zero clicks. They're placed above ads and regular search results, and they're created/maintained by you (the community). Some Instant Answers are built from pure code and others require external sources (API requests), databases, or key-value stores. The possibilities are endless but the point is to provide a perfect result for every search. 

![App search Instant Answer example](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fapp_search_example.png&f=1)

In the above example, [Quixey](http://quixey.com/) was a source that our own DuckDuckHack Community suggested for mobile app search. Now, any time someone searches for apps on DuckDuckGo, we request information directly from Quixey to help answer the search. Here, we'll show you how to build Instant Answers that can do this and more! 

## How can I contribute? 

Create new Instant Answers.  
*Use this documentation to develop a new Instant Answer*  

Improve Current Instant Answers.  
*Fix issues in our [zeroclickinfo repositories](https://github.com/duckduckgo)*  

Code review and help  
*Help with pull requests in our [zeroclickinfo repositories](https://github.com/duckduckgo)*  

Discuss Instant Answers.  
*Help others with their [ideas](https://duck.co/ideas)*  


## Start

Instant Answers come in all varieties but we encourage everyone to work on an Instant Answer they're genuinely passionate about. The section below will help you refine your ideas. 

### Forming your Idea

If you've never created an Instant Answer before, please start by working on a [pre-approved Instant Answer idea.](https://duck.co/ideas/status/3?table_lnKRpLENwO2NUmZUyukQpw_sort=votes)    

If you've already built an Instant Answer (the quick-start goodie doesn't count), think of the searches you do most often:

- What has always frustrated you about the results? 
- What do you wish "just worked?"
- Is there a website or source of data that would help answer most/all of those searches? 

A great example is the [CourseBuffet Instant Answer](https://duck.co/ia/view/coursebuffet). Rubydubee (the contributor) created an Instant Answer powered by CourseBuffet's API make searching for online courses easier: https://duckduckgo.com/?q=computer+science+online+course&ia=onlinecourses 

A simpler example can be found with the dice Instant Answer. Want to virtually throw a pair of dice? How about 5 dice? You can do it on DuckDuckGo: https://duckduckgo.com/?q=throw+2+dice&ia=answer 

In both of these examples, users will more easily find what they're looking for via the Instant Answers provided, instead of clicking through regular results. If you're still unsure of what to build, you can work on an idea from our community or get help with your idea here: https://duck.co/ideas 

#### Improve Another Idea

You can check if your idea has already been suggested or implemented in the [Ideas forum](https://duck.co/ideas ) and [Instant Answers index](https://duck.co/ia). If it already exists (as an idea or a live Instant Answer), you can still contribute to it. Let us know how you'd like to improve the Instant Answer using the same steps below for, "Submitting Your Idea." 


### Submitting Your Idea

The most important step in creating Instant Answers is to let the DuckDuckGo staff and community know that you're getting started. Sometimes, we cannot accept a submitted Instant Answer because the implementation or source are not up to our standard. There are multiple ways to reach out:  

- Ask in our [Ideas chat channel](https://gitter.im/duckduckgo/Ideas)
- Email us at [open@duckduckgo.com](mailto:open@duckduckgo.com)
- Join and ask our [developer's email list](https://www.listbox.com/subscribe/?list_id=197814)
- Submit to [Duck.co/ideas](https://duck.co/ideas)


If choosing email, this sample will help you craft your message:

```text
To: open@duckduckgo.com
Subject: Awesome Instant Answer Idea

I'd like to make an Instant Answer to help people searching for <topic/subject>!
When someone searches for <your trigger idea>, it would be cool if they could see <your response idea>.
I'm going to accomplish this with a <Goodie/Spice/Fathead/Longtail> type Instant Answer.
This is the data source: <link, description, Perl module, etc.>.
This is the related Duck.co idea: <url, if applicable>.
This is my Github username: <username>.

Thanks!

PS: DuckDuckGo is awesome!
```

With every channel, we'll try and get back to you as soon as possible (ideally within 24hrs). We ask that you wait to hear back from us before moving ahead unless you're absolutely sure this Instant Answer is acceptable (e.g. a [duck.co idea](https://duck.co/ideas) that has been approved by DDG staff). 


## Creating Your Own Instant Answer

After getting approval, you'll need to [determine your Instant Answer back-end type](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/getting-started/determine_your_instant_answer_type.md).
