# Basic Goodie Tutorial
<!--
<h2 class="summary" moreat="goodie_basic_tutorial">Basic goodie tutorial</h2>
<span class="summary-text" markdown="1">
In this tutorial, we'll be making a Goodie instant answer that checks the number of characters in a given search query. The end result  works [like this](https://duckduckgo.com/?q=chars+How+many+characters+are+in+this+sentence%3F)
</span>
-->
In this tutorial, we'll be making a Goodie instant answer that checks the number of characters in a given search query. The end result  works [like this](https://duckduckgo.com/?q=chars+How+many+characters+are+in+this+sentence%3F) and will look like this:

###### chars.pm

```perl
package DDG::Goodie::Chars;
# ABSTRACT: Give the number of characters (length) of the query.

use DDG::Goodie;

triggers start => 'chars';

handle remainder => sub {
    return 'Chars: ' . length $_ if $_;
    return;
};
1;

```

## Naming our Goodie Package
<!-- <h2 class="summary" moreat="goodie_basic_tutorial#naming-our-goodie-package">Naming a Goodie Package</h2>
<span class="summary-text" markdown="1">
To begin, open your favourite text editor like [gedit](http://projects.gnome.org/gedit/), notepad or [emacs](http://www.gnu.org/software/emacs/) and type the following:

```perl
package DDG::Goodie::Chars;
# ABSTRACT: Give the number of characters (length) of the query.
```
</span>
-->
To begin, open your favourite text editor like [gedit](http://projects.gnome.org/gedit/), notepad or [emacs](http://www.gnu.org/software/emacs/) and type the following:

```perl
package DDG::Goodie::Chars;
# ABSTRACT: Give the number of characters (length) of the query.
```

Each instant answer is a [Perl package](https://duckduckgo.com/?q=perl+package), so we start by declaring the package namespace. For a new Goodie (or any new instant answer), you would change **Chars** to the name of the instant answer (written in [CamelCase](https://duckduckgo.com/?q=camelcase) format).

The second line is a special comment line that is used for documentation purposes.

## Import the Goodie Class

Next, type the following [use statement](https://duckduckgo.com/?q=perl+use) to import [the magic behind](https://github.com/duckduckgo/duckduckgo/tree/master/lib/DDG) our instant answer system.

```perl
use DDG::Goodie;
```

**\*\*Note:** Right after the above line, you should include any Perl modules that you'll be leveraging to help generate the answer. **Make sure** you add those modules to the `dist.ini` file in this repository. If you're not using any additional modules, carry on!

## Define the Trigger Word(s)

On the next line, type:

```perl
triggers start => 'chars';
```

**triggers** are keywords/phrases that tell us when to make the instant answer run. When a particular *trigger word* (or phrase) is part of a search query, it tells DuckDuckGo to *trigger* the instant answer(s) that have indicated they should trigger for the given word (or phrase).

In this case there is one trigger word: "**chars**". 

Let's say someone searched "**chars this is a test**". **chars** is the *first* word, so it would trigger our Goodie because the **start** keyword says, "Make sure the *trigger word* is at the *start* of the query." 

There are several other keywords like **start** which will be covered shortly. The **=>** symbol is there to separate the trigger words from the keywords (for readability).

## Define the Handle Function
<!-- <h2 class="summary" moreat="goodie_basic_tutorial#naming-our-goodie-package">Goodie defining the handle function</h2>
<span class="summary-text" markdown="1">
```perl
handle remainder => sub {
```

Once triggers are specified, we define how to *handle* the query. `handle` is another keyword, similar to **triggers**.
</span>
-->
Moving on, enter this on the next line:

```perl
handle remainder => sub {
```

Once triggers are specified, we define how to *handle* the query. `handle` is another keyword, similar to **triggers**.

You can *handle* different parts of the search query, but the most common is the **remainder**, which refers to the remainder of the query, after the first matched trigger word/phrase has been removed. 

For example, if the query was "**chars this is a test**", the trigger would be *chars* and the remainder would be *this is a test*.

Now let's add a few more lines to complete the handle function:

```perl
handle remainder => sub {
    return 'Chars: ' . length $_ if $_;
    return;
};
```

This function (the part within the **{}**, after **sub**) is the most important part of the Goodie. It defines the instant answer that will be displayed at the top of the [search results page](https://duckduckgo.com/?q=chars+this+is+a+test).

Whatever you are handling is passed to the function in the **$\_** variable ( **$\_** is a special default variable in Perl that is commonly used to store temporary values). For example, if you searched DuckDuckGo for *"chars this is a test"*, the value of **$\_** will be *"this is a test"*, i.e. the remainder.

Let's take a closer look at the first line of the function:

```perl
return 'Chars: ' . length $_ if $_;
```

The heart of the function is just this one line. The **remainder** is in the **$\_** variable as discussed. If it is not blank ( **if $\_** ), we return the number of chars using Perl's built-in [length function](https://duckduckgo.com/?q=perl+length).

Perl has a lot of built-in functions, as well as thousands of modules available [via CPAN](https://metacpan.org/). You can leverage these modules when making Goodies, similar to how the [Roman Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/Roman.pm) uses the [Roman module](https://metacpan.org/module/Roman).

If we are unable to provide a good instant answer, we simply **return nothing**. That's exactly what the second line in the function does.

```perl
return;
```

This line is only run if **$\_** contained nothing, because otherwise the line before it would return something and end the function execution.


## Return True at EOF

Finally, all Perl packages that load correctly should [return a true value](http://stackoverflow.com/questions/5293246/why-the-1-at-the-end-of-each-perl-package) so add a 1 on the very last line, and make sure to also add a newline at the end of the file.

```perl
1;

```

And that's it! At this point you have a working Goodie instant answer. 

## Recap
The instant answer system works like this at the highest level:

- We break the query (search terms) down into separate words, which is a process that happens in the background.

- We see if any of those words or groups of words are **triggers** for any instant answers. These **triggers** are defined by the developer when creating an instant answer. In the example we used above, the trigger word is "**chars**".

- If a Goodie is triggered, we run its `handle` function.

- If the Goodie's handle function outputs an instant answer via a **return** statement, we display it at the top of the SERP (search engine results pages).
