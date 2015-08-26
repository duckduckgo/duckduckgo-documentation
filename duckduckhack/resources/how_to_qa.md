# How to QA an Instant Answer

Our goal is to have a great Instant Answer for every search. When a developer submits a new Instant Answer, it must first be thoroughly reviewed by our community and internal staff before going live on DuckDuckGo.
Please use the following guide when QA-ing Instant Answers:

## Everyone (Reviewing Quality):

### What's an Instant Answer made of?

1. Some code
2. A data source (like a website)

### How do they work?

Instant Answers are a bundle of code that make information from one source available directly on DuckDuckGo. Anyone can suggest them and anyone can create them!
Check out some examples of what we mean:

- [Definition search:](https://duckduckgo.com/?q=define+hello&ia=definition)
	- [Code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/share/spice/dictionary/definition/dictionary_definition.js)
	- [Data Source](https://www.wordnik.com/)

- [Weather search:](https://duckduckgo.com/?q=weather+in+chicago&ia=weather)
	- [Code](https://github.com/duckduckgo/zeroclickinfo-spice/blob/master/lib/DDG/Spice/Forecast.pm)
	- [Data Source](https://developer.forecast.io/)

### What we're looking for in QA

**Function:** Is the Instant Answer actually useful?
Instant Answers should *always* be unambiguously **better** than organic links. If it doesn't add value to the page, then it should not be approved.

- **Example test:** Search for something that will trigger the Instant Answer and compare it to the organic links. The user should benefit from having the Instant Answer available. In the best case scenario, the Instant Answer should give the user all the information they need, so they don't even have to click a link. At the very least, the Instant Answer should offer some different and more valuable information than the links.


**Relevancy:** Does the Instant Answer always provide relevant information?
Instant Answers should only show information that is correct and relevant to the user's search. If an Instant Answer is capable of returning irrelevant information (e.g., "free gaming apps" should *only* show free apps, "the dark knight movie" should ensure both words, "dark" and "knight" are in the resulting movie's title), then the relevancy must be improved before the Instant Answer is accepted and goes live.

- **Example test:** Search for something that will trigger the Instant Answer and compare the information provided to the original source's website (if one exists) or another credible source. For example, if the Instant Answer performs arithmetic operations, you could verify that its calculations are correct using your calculator at home. If it provides movie information, you could verify that it's correct using Wikipedia or IMDb.


**Triggering:** Does the Instant Answer trigger when it shouldn't? Are there any queries that *should* trigger the Instant Answer, but don't?
Goodie and Spice Instant Answers use a list of, "trigger words" (or phrases) that signal DuckDuckGo to use that Instant Answer when those triggers appear in a search query. If they are too generic, it will cause the Instant Answer to be shown in cases which are inappropriate. For example, "app" is a very generic word which occurs in many queries that aren't necessarily an app search. Instant Answers that use generic triggers should always further qualify the query to make sure it should return an answer. On the other hand, if triggers are too specific, it can lead users to believe that an Instant Answer doesn't exist for that topic or query space, reducing the value in searching with DuckDuckGo.

- **Example test:** Can you think of any queries that should or shouldn't be triggering this Instant Answer? Let's say we have an Instant Answer that shows movies, and it triggers with the term, "movie". The query, "movie Thor" would trigger this Instant Answer, but other queries, such as, "watch Thor", "Thor movies", "film Thor" or "Thor film" should also trigger this Instant Answer.


**Adult Content:**
Is the Instant Answer effectively preventing adult words or inappropriate content from showing? There shouldn't be any adult imagery or profanity in Instant Answers, by default. If an Instant Answer is capable of displaying profanity or questionable adult humor, it should not be approved (if it's vulgar or distasteful), or it can be set to only show when safe search is off. If ever in doubt, please ask community leaders or DDG staff for help.

- **Example test:** Check if the Instant Answer is capable of producing profanity or adult imagery by searching for relevant (profane) keywords or risqué content. If so, the Instant Answer should block all instances of adult language and adult imagery. If not, you've found a bug!


**Design:**
Can we minimize the space used? How does it look on smaller screens? Can you break the design? For example, try using non-UTF8 characters or long search queries. Do the design and layout make sense given the type of information? Does it look and feel like other Instant Answers? (It should!) Spotting design bugs and improvements can be tricky, since everyone's eye for design is a bit different, but you can refer to live Instant Answers as an example.

- **Example test:** Test the Instant Answer with a few different queries. Make sure the most important information is easy to identify and understand. The information shouldn't be too crowded or too sparse. Try previewing the Instant Answer on a mobile device (phone, tablet) and check if the design breaks or if too much vertical space is used. Ideally, an Instant Answer on mobile screens should ***not*** push organic links off the page. If this is the case, look for ways to either increase the information density or reduce the information shown &mdash; this is a great way to determine what information is absolutely necessary and deserves to be shown.


**Conflicts:**
Does it conflict with other Instant Answers? We wouldn't want to step on the query space of other Instant Answers.

- **Example test:** Check to see if an Instant Answer already exists for the new Instant Answer's triggers. For example, [a search for "Bill Murray"](https://duckduckgo.com/?q=bill+murray) currently shows Wikipedia, so if the new Instant Answer will show for searches like, "Bill Murray," then it should be noted to the developer in case one Instant Answer is better than the other.


## Developers (Reviewing Code):

**High Level (Perl & JavaScript)**

- Is this the right Instant Answer type? Would it be better to implement this as another IA type?

	- If this should really be another IA type (e.g., JavaScript heavy Goodie should probably be a Spice) it's best to note this as early in the process as possible, since the Instant Answer will need to be re-implemented and a new pull-request submitted.

- What other data is available from this source? (check the API response for anything really useful that's not being displayed).

- Is this the best layout/design to display all the data? (For Spice, consider the various templates)

- Does the API often return irrelevant results? If so, consider using the `isRelevant()` function or, if that is already in use, improve the client-side relevancy checking by making it more strict.

**Regarding the code...**

- The code should well organized. If things don't make sense, make comments and ask questions! It's better to go overboard with your feedback than to hold back.

	- For Perl modules, metadata comes first, then static variables and function definitions, then the `handle` function last.

- The code should be easy to understand and follow. Other developers must be able to understand the code reasonably well, in case fixes or improvements need to be made.

	- Non-trivial functions and processes should be well documented.

	- The code should be written to optimize performance and efficiency while maintaining simplicity and legibility (where applicable and without causing performance problems).

	- Inefficient code should be noted and improvements should be suggested.

- Are the caching parameters correct? Should we *not* cache the API responses? (they are cached by default)

	- Consider `is_cached` and `proxy_cache_valid`.

- If an Instant Answer is capable of displaying profanity or questionable adult humor, make sure the `is_unsafe` flag is set.

**Low Level (Perl)**

- Static variables (e.g., lists, hashes, regular expressions) and helper functions should not be declared inside `handle` functions (this will cause them to be redefined each time the Instant Answer is triggered). The same applies when reading files &mdash; the file handler should be outside the `handle` function.

- Long lists of trigger words/phrases should be moved to a `triggers.txt` file (in the share directory) and `slurp()` should be used to convert them into a list.

- API Keys should not be merged in, the proper placeholder syntax should be used `{{ENV{DDG_SPICE_<SPICE_NAME>_APIKEY}}}`

	- DDG staff should also be notified so we can get our own API Key.

- Check if existing CPAN libraries can replace some functions. We can use libraries for a variety of things and you can find them all on [MetaCPAN](https://metacpan.org/).

**Low Level (JavaScript)**

- Semicolons must be used; Point out any missing semicolons;

- Cross-browser compatibility is very important! Use jQuery methods where applicable to ensure this. We also support IE9+, and it's good to be aware of these. Search for the method on MDN if you're unsure.

	- e.g., `Array.prototype.forEach()` should be replaced with `$.each()`.

- JavaScript that runs before the rendering of the Spice (`Spice.render()`) should be used to error-check, massage, and organize the data that will be passed on to the template.

- Template helpers should be used to format output and decide what should be shown.

- HTML should not be created or inserted into the DOM before or after rendering. For example, don't use jQuery to build your display, that's what templates are for :)

- Templates and sub-templates should be used when dealing with HTML, not jQuery.

- Don't declare any global variables. JavaScript has function scope, so anything outside of a function is global (or part of the `window` object). Also, variables that were not declared with `var` are globals, too. Check out the [JavaScript Garden](http://bonsaiden.github.io/JavaScript-Garden/#function.general) for more information about this.

	- On this note, make sure [strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode?redirectlocale=en-US&redirectslug=JavaScript%2FReference%2FFunctions_and_function_scope%2FStrict_mode) is enabled. This helps catch the usual pitfalls in JS.

- `if` statements should always use curly braces, `{}`
