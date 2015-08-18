# Goodie Cheat Sheets

A popular (and perfect) use of Goodies is to create cheat sheets which are available right from the DuckDuckGo search bar. To make adding a cheat sheet as quick as possible, we've brought all cheat sheets together under one Instant Answer, called the [Cheat Sheets Goodie](https://duck.co/ia/view/cheat_sheets).

![tmux cheat sheet](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftmux_cheat_sheet.png&f=1)

When your cheat sheet name is searched with any of the trigger words, your Instant Answer will be shown. For example, for the *vim* text editor, the Instant Answer will be triggered on: "vim cheatsheet", "vim commands", "vim guide", "vim shortcuts", and so on (full list of triggers available in [CheatSheets.pm](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/CheatSheets.pm)). You can also specify additional triggers, as you'll see in the example below.

Looking for ideas for your cheat sheet? Check our [inspiration list](#cheat-sheet-ideas) below.

## How to Add Your Cheat Sheet

Once you have an [idea for a cheat sheet](#cheat-sheet-ideas), it's easy to add it to the DuckDuckGo Cheat Sheet Goodie. 

The first step is to [set up your development environment](https://duck.co/duckduckhack/setup_dev_environment). Following the [setup instructions](https://duck.co/duckduckhack/setup_dev_environment) will get you ready to contribute to the repository.

After [following the steps](https://duck.co/duckduckhack/setup_dev_environment) to set up your environment, you'll be one file away from submitting your cheat sheet to appear on DuckDuckGo.

### Create a JSON File

Instead of creating an entirely new Instant Answer, you simply need to add **one JSON file** to the existing `/json` folder in the [Cheat Sheets share directory](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/cheat_sheets/json).

To do this in Codio, use the left-hand panel to enter the `/zeroclickinfo-goodies` repository directory. Then use the file tree to click into the `/share/goodie/cheat_sheets` directory. Then click the **json** folder. 

Up in the **File menu**, click **"Create New File"**, and enter the name of your cheat sheet as a JSON file (make sure it's saving to the `cheat_sheets` directory). For example, if the trigger for your cheat sheet is "gopro cheat sheet" create a new file called `gopro.json`.

Erase any pre-filled contents, and enter the values for your cheat sheet using the [cheat sheet JSON syntax](#cheat-sheet-json-syntax). Feel free to copy the code in the following section into your new file as a convenient template.

Conveniently, with cheat sheets there's no need to create a new Instant Answer. There is also no need to edit the `CheatSheets.pm` file, `cheat_sheets.js`, or `cheat_sheets.css`. Simply save your new file, and proceed to test your work.

### Test Your Cheat Sheet

The next step is to test your code and make sure it works like you intended. To do this, we'll create a test server that will allow you to view your Instant Answer as it would appear above DuckDuckGo search results.

1. In Codio, open your Terminal by clicking on **Tools > Terminal**.
2. Change into the `zeroclickinfo-goodies` directory by typing `cd zeroclickinfo-goodies` at the command line.
3. Next, type **`duckpan server`** and press "**Enter**". The Terminal should print some text and let you know that the server is listening on port 5000.

    ```
    Starting up webserver...
    You can stop the webserver with Ctrl-C
    HTTP::Server::PSGI: Accepting connections at http://0:5000/
    ```

4. Click the "**DuckPAN Server**" button at the top of the screen. A new browser tab should open and you should see the DuckDuckGo Homepage. Type the name of your cheat sheet, plus **"cheat sheet"** and press "**Enter**".
10. You should see your cheat sheet show up in the search results! **Make sure it displays correctly; check that all escaped characters and code blocks appear as you intended.**
11. When you're done testing, go back to the Terminal, andpress "**Ctrl+C**" to shut down the DuckPAN Server. The Terminal should return to a regular command prompt.

When your cheat sheet works like you want it to, you're ready to submit your contribution.

### Submit Your Pull Request

Submitting your cheat sheet is similar to submitting any Instant Answer contribution. New code is submitted using pull requests on GitHub. To make a pull request, follow the [submission and review instructions](https://duck.co/duckduckhack/submission_and_review).

## Cheat Sheet JSON

Below is a summary of the [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/vim.json) file, which displays a cheat sheet when searching for ["vim cheat sheet"](https://duckduckgo.com/?q=vim+cheat+sheet&ia=answer).

![vim cheat sheet](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvim_cheat_sheet.png&f=1)

The above Instant Answer was created by simply adding [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/vim.json), explained below. 

**We encourage you to copy the [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/vim.json) code into your new file, as a starting point for your cheat sheet.** (Copy the [actual file](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/vim.json), as the code block below won't work due to inline comments.)

```javascript
{
    // Required; must match the id of the cheat sheet's IA page
    // For example, https://duck.co/ia/view/vim_cheat_sheet
    "id": "vim_cheat_sheet", 

    // Required; displayed as title of AnswerBar
    "name": "Vim",

    // Optional; displayed as subtitle of AnswerBar
    "description": "Text Editor", 
    
    // Required if cheat sheet has a source; useful to link users to further information.
    // Displayed at bottom of AnswerBar, favicon shown automatically
    "metadata": { 
        "sourceName": "VimCheatSheet",
        "sourceUrl": "https://..." // Should be SSL if possible
    },

	// Optional; add additional search triggers for your cheat sheet
	"aliases": [
        "vim", "Vi IMproved", "vi text editor"
    ],

    // Optional; pick the cheat-sheet template (explained below)
    "template_type": "keyboard",

    // Required; controls which sections appear and in what order
    "section_order": [  
        "Cursor movement",
        "Insert mode - inserting/appending text",
        // ...additional sections
        "Tabs"
    ],

    // Required; section names must match those in section_order in order to appear
    "sections": {
        "Tabs": [
            {
                "key": "#gt", 
                "val": "move to tab number #"
            },
            {
                "key": "[Ctrl] [wt]",
                "val": "move the current split window into its own tab"
            }
            // ...additional entries
        ],        
        "Insert mode - inserting/appending text": [
            {
                "key": "i",
                "val": "insert before the cursor"               
            }, 
            {
                "key": "I",
                "val": "insert at the beginning of the line"
            }
            // ...additional entries
        ],  
        // ...additional sections
    }
}
```

### Cheat Sheet Templates

We've seen a wonderfully wide variety of cheat sheets; we realized that one visual format doesn't fit all ideas. We've created an *optional* `template_type` property so you can pick the best look for your cheat sheet.

Here are the available `template_type` values:

- `keyboard` - the default (see it live at ["vim cheatsheet"](https://duckduckgo.com/?q=vim+cheatsheet&ia=cheatsheet))
- `terminal` - (see it live at ["git cheatsheet"](https://duckduckgo.com/?q=git+cheatsheet&ia=cheatsheet))
- `code` - (see it live at ["regex cheatsheet"](https://duckduckgo.com/?q=regex+cheat+sheet&ia=cheatsheet))
- `reference` - (see it live at ["wu-tang cheatsheet"](https://duckduckgo.com/?q=wu-tang+cheat+sheet&ia=cheatsheet))

### Syntax for `key` Property

Cheat sheet actions often have several key combinations, which you can indicate in the syntax of each `key` property.

**Brackets, `[ ]`, or braces, `{ }`, are used to wrap key combinations in code blocks.** For convenience, if you include no brackets or braces, the entire string will be shown in a code block.

*Note: It does not matter whether you use brackets or braces - they both wrap text in code blocks.*

#### Escaping Special Characters

Your cheat sheet might include characters which are themselves part of JSON syntax. To express these literally, escape them using backslashes, like [standard JSON](http://json.org):

- To express a double quote, use a single backslash: `\"`
- To express a forward slash, use a single backslash: `\/`
- For full list of characters, see the diagram on the right on [the official JSON documentation](http://json.org).

Because cheat sheets display brackets `[ ]` and braces `{ }` as code blocks, express those literally using a **double backslash**:

- If you want to express a literal bracket, use a double backslash `{Ctrl + \\[}`.
- If you want to express a literal brace, use a double backslash `[Ctrl + \\{]`.
- To express a **single literal backslash**, type four backslashes in a row: `[Ctrl + \\\\]`.

*Note that an uneven number of sequential backslashes will throw an error.*

### Formatting Key Presses

Cheat sheets often list key combinations, which you can express in any way you choose. The following are only suggestions; choose the appropriate convention for your subject.

#### Single Keys or Commands

There is no special syntax required for the string - for example, `"x"` or `":set color"`. The entire string will be shown in one code block.

#### Simultaneous Keys (e.g., pressing A and B together)

We recommend expressing simultaneous key presses as follows: 

- As adjacent code blocks, e.g. `"[Ctrl] [v]"`
- For "*nix-style" cheatsheets (like Emacs), as a single code block with a dash, e.g. `"[C-v]"`
	
#### Consecutive Keys (e.g., pressing A, then pressing B)

We recommend expressing consecutive key presses as separate code blocks separated by a comma, e.g. `"[Ctrl-B], [x]"`
	
#### Alternative Keys (e.g., pressing either A or B)

We recommend displaying alternatives as follows: 

- For single-key alternatives, wrap in parentheses, e.g. `[Ctrl] ( [L] / [P] )`
- For complete alternatives, we recommend replicating the key-value pair. Make an indication in the `val` that it's an alternative:
	
	```
	{
        "key": "[Ctrl] [j]",
        "val": "Jump"               
    },
	{
        "key": "[Ctrl] [Spacebar]",
        "val": "Jump (alternative)"               
    },
	```

#### Arrow Keys

We've found the best way to express arrow keys is directly using arrow ASCII characters (&larr;, &uarr;, &rarr;, &darr;). Feel free to copy and paste the characters from here.

For example, instead of **[Shift] [Up]** we recommend **[Shift] [&uarr;]**.

## Cheat Sheet Ideas

Grab one of these ideas from the categories below and then start coding using the instructions below. Let us know that you're working on one by emailing open@duckduckgo.com with your selection: 

Apps  
Audio  
Computing  
Cryptography  
Currency  
Dictionary  
-	[Military Slang](https://en.wiktionary.org/wiki/Appendix:Glossary_of_U.S._Navy_slang)  
-	[Jive talk](https://en.wikipedia.org/wiki/Glossary_of_jive_talk)  
-	[How to talk to someone from the nineteen fifties](http://www.citrus.k12.fl.us/staffdev/social%20studies/pdf/slang%20of%20the%201950s.pdf)  
-	[How to talk to someone from the nineteen twenties](http://thoughtcatalog.com/nico-lang/2013/09/59-quick-slang-phrases-from-the-1920s-we-should-start-using-again/)    

Domain  
Entertainment    
-	[Blackjack strategy](http://johnlevandowski.com/wp-content/uploads/2011/04/blackjack6ds17.png)  
-	[Poker hands](https://en.wikipedia.org/wiki/List_of_poker_hands)  

Finance  
Food & Drink  
-	Names of espresso-based drinks   
-	[Types of italian meats](http://www.igourmet.com/italian-meats.asp)  
-	Wine/Food pairings  
-	Wine/Cheese pairings  
-	<del>[Cocktails](https://en.wikipedia.org/wiki/List_of_cocktails)</del> ([submitted](https://github.com/duckduckgo/zeroclickinfo-goodies/pull/1208) by [jppope](https://github.com/jppope))    
-	Kosher animals  
-	[Types of scotch](http://www.dramming.com/2011/06/16/10-essential-things-about-scotch-whisky-everybody-should-know/)  
-	Types of wine  
-	[Types of liquor](http://classyboozer.com/different-types-of-liquor/)  
	
Games  
-	<del>Minecraft commands for PC</del> ([submitted](https://github.com/duckduckgo/zeroclickinfo-goodies/pull/1222) by [kbhat95](https://github.com/kbhat95))  
	
Geek  
-	Superheroes and their superpowers  
	
Geography  
-	Chinese dialects by region/province  
	
Health  
-	Types of sugars and where found  
-	Vitamins/Minerals and their benefits  
-	Superfoods and their benefits  
	
Images  
Jobs  
Literature  
-	<del>Game of Thrones house names</del> ([completed](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/game-of-thrones-houses.json) by [zekiel](https://github.com/zekiel/))    
-	Game of Thrones house slogans  
-	Game of Thrones house sigils  
	
Local  
Math  
Movies  
Music  
News  
Politics  
Productivity  
-	<del>Firefox Awesome bar shortcuts</del>  ([completed](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/awesome-bar.json) by [domjacko](https://github.com/domjacko)  
-	<del>Imgur shortcuts</del> ([submitted](https://github.com/duckduckgo/zeroclickinfo-goodies/pull/1220) by [RomainLG](https://github.com/RomainLG))  
-	<del>Emacs shortcuts</del> ([completed](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/emacs.json) by [punchagan](https://github.com/punchagan))  
-	<del>Photoshop shortcuts</del> ([submitted](https://github.com/duckduckgo/zeroclickinfo-goodies/pull/1203) by [kbhat95](https://github.com/kbhat95))  
	
Products  
Programming  
Reference  
-	Car ownership (which companies own which companies)  
-	[Anniversary themes (paper, cotton, leather, golden, etc.](https://en.wikipedia.org/wiki/Anniversary)     
-	Greek god names and their dominion   
-	Roman god names and their dominion   
-	[Plant zones](http://www.lawn-and-gardening-tips.com/planting-zones.html)  
-	[Police codes](http://www.radiolabs.com/police-codes.html) 
	
Science  
-	Lightbulb color:temperature   
-	[VHF Frequencies](https://en.wikipedia.org/wiki/Marine_VHF_radio)  
	
Social  
Software  
Sports  
Statistics  
Sysadmin  
Tools  
Travel  
TV  
Videos  
Weather  
Web Design  
Words & Games  
-	[SMS spellings](https://en.wikipedia.org/wiki/SMS_language)  
-	Military alphabet (Alpha, Bravo, Charlie...)  
-	[News/politics shorthand SCOTUS, FLOTUS, POTUS](http://www.nytimes.com/1997/10/12/magazine/on-language-potus-and-flotus.html)  
-	[Secret Service code names over the years](https://en.wikipedia.org/wiki/Secret_Service_codename)  
-	[Morse Code Alphabet](http://www.scoutscan.com/cubs/morsecode.html)  


