# How to QA an Instant Answer

Our goal is to have a great instant answer for every search. When a developer submits a new instant answer, it must first be thoroughly reviewed by our community and internal staff before going live on DuckDuckGo.com
Please use the following guide when QA-ing instant answers:

## Everyone (Reviewing Quality):

### What's an instant answer made of?

- 1. Some code
- 2. A data source (like a website)

### How do they work?

Instant answers are a bundle of code that make information from one source available directly on DuckDuckGo. Anyone can suggest them and anyone can create them!
Check out some examples of what we mean:

- [Definition search:](https://duckduckgo.com/?q=define+hello)

	- [Code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dictionary/definition/dictionary_definition.js)

	- [Data Source](https://www.wordnik.com/)

- [Coupon search:](https://duckduckgo.com/?q=running+shoes+coupons)

	- [Code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/coupon_mountain/coupon_mountain.js)

	- [Data Source](http://www.couponmountain.com/)

### What we're looking for in QA

**Function:** Is the information shown in the instant answer better than using a regular organic link?
Instant Answers should always be more useful than just clicking on an organic link. If the instant answer doesn't add value to the page, then it shouldn't be approved.

   - **Example test:** Search for something that will generate the instant answer and compare the information provided to what's in the organic links. Is the user more informed if they use the instant answer instead of clicking on a link? Does the instant answer make it easier to find relevant information (e.g. less or no clicks necessary)?


**Relevancy:** Does the instant answer return relevant data from the source?
Instant answers should never show information that's incorrect or not relevant to the user's search. Sometimes, an instant answer will return bad information, like showing the wrong value for a calculation or the wrong Wikipedia article for an actor's name.

	- **Example test:** Search for something that will generate the instant answer and compare the information provided to the original source or another source. More often than not, you can check the relevancy of an instant answer by comparing it to the original source's website (or another credible source). If the instant answer did math additions, you could verify that [5 x 8 = 40] using your calculator at home. If it showed movie information, you could verify what it showed on Wikipedia or IMDB.com


**Triggering:** Can you think of other ways of triggering the instant answer?
Every instant answer is triggered in some way. Most instant answers use a list of, "trigger words" (or phrases) that signal DuckDuckGo to use that instant answer. Sometimes, the triggers are too generic or too specific, resulting in an instant answer being shown too much or too little.

	- **Example test:** Can you think of any queries that should trigger this instant answer? Let's say we have an instant answer that shows movies, and it triggers with "movie". So typing in "movie thor" would trigger this instant answer, but maybe we want it to trigger on "watch thor" or "thor movies" or "film thor" or "thor film."


**Adult Content:** 
Is the instant answer effectively not showing adult words or content by default (safe-search on)? There shouldn't be any adult imagery or profanity in instant answers by default.

	- **Example test:** Try looking for profanity or generating adult imagery (if the instant answer shows images). The instant answer should block all instances of adult language and adult imagery. If not, you've found a bug! 


**Design:** 
Can we minimize the space used? How does it look on smaller screens? Can you break the design? (using non-UTF8 characters, long queries, etc.). Spotting design bugs and improvements can be tricky, since everyone's eye for design is a bit different. 

	- **Example test:** Does the instant answer do math equations? Try a really long math equation to see if the text runs past the page . Is the instant answer really crowded? Think about changing the text color or layout to clean things up, like this before  and after . Try previewing the instant answer on a mobile device and look for ways to reduce either the space occupied or the information shown. That's a great way to determine what information is absolutely necessary on both desktop and mobile.


**Conflicts:**
Does it conflict with other instant answers? We wouldn't want to step on the query space of other instant answers.

	- **Example test:** Check to see if an instant answer already exists for the new instant answer's triggers. For example, a search for "Bill Murray" currently shows Wikipedia  so if the new instant answer will show for searches like, "Bill Murray," then it should be noted to the developer in case one instant answer is better than the other. 


## Developers (Reviewing Code):

**High Level (Perl & JavaScript)**

	- Is this the right instant answer type? Would it be better to implement this as another IA type?

	- If this should really be another IA type (e.g. JavaScript heavy Goodie should probably be a Spice) it's best to note this asap so the IA can be re-implemented and a new PR should be made

	- What other data is available from this source? (check the API response for anything really useful that's not being displayed).

	- Is this the best layout/design to display all the data? (For Spice, consider the various templates)

	- Does the API often return irrelevant results? If so, use/improve client-side relevancy handling (`DDG.isRelevant`).

**Regarding the code...**

	- The code should well organized. If things don't make sense, make comments and ask questions.

		- For Perl modules, metadata comes first, then static variables and function definitions, then the `handle` function last.

	- The code should be easy to understand and follow. Other developers must be able to understand the code reasonably well in-case fixes or improvements need to be made.

		- Non-trivial functions and processes should be well documented.

		- The code should be written to optimize performance and efficiency while maintaining simplicity and legibility (where applicable and without causing performance problems).

		- Inefficient code should be noted and improvements should be suggested.

	- Are the caching parameters correct? Should we *not* cache the API responses? (they are cached by default)

		- Consider `is_cached` and `proxy_cache_valid`.

**Low Level (Perl)**

	- Static variables (e.g. lists, hashes, regular expressions) and helper functions should not be declared inside `handle` functions (this will cause them to be redefined each time the instant answer is triggered). The same applies when reading files &mdash; the file handler should be outside the `handle` function.

	- Long lists of trigger words/phrases should be moved to a `triggers.txt` file (in the share directory) and `slurp()` should be used to convert them into a list.

	- API Keys should not be merged in, the proper placeholder syntax should be used `{{ENV{DDG_SPICE_<SPICE_NAME>_APIKEY}}}`

		- DDG staff should also be notified so we can get our own API Key.

	- Check if existing CPAN libraries can replace some functions. We can use libraries for a variety of things and you can find them all on MetaCPAN.

**Low Level (JavaScript)**

	- Semi-colons must be used; Point out any missing semi-colons;

	- Cross-browser compatibility is very important, use jQuery methods where applicable to ensure this. We're trying to support IE 8, and it's good to be aware of these. Search for the method on MDN if you're unsure.

		- E.g. `Array.prototype.forEach()` should be replaced with `$.each()`.

	- Watch out for `console.log` &mdash; that won't work on IE 8.

	- JavaScript that runs before the rendering of the Spice (`Spice.render()`) should be used to error-check, massage, and organize the data that will be passed on to the template.

	- Template helpers should be used to format output and decide what should be shown.

	- HTML should not be created or inserted into the DOM before or after rendering (i.e. don't use jQuery to build your display, that's what templates are for)

	- Templates and sub-templates should be used when dealing with HTML, not jQuery.

	- Don't declare any global variables. JavaScript has function scope, so anything outside of a function is global (or part of the `window` object). Also, variables that were not declared with `var` are globals, too. Check out the JavaScript Garden for more information about this.

		- On this note, make sure strict mode is enabled. This helps catch the usual pitfalls in JS.

	- `if` statements should always use curly braces, `{}`