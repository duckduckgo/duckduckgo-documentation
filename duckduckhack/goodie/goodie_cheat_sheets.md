# Goodie Cheat Sheets

A popular (and perfect) use of Goodies is to create cheat sheets which are available right from the DuckDuckGo search bar. To make adding a cheat sheet as quick as possible, we've brought all cheat sheets together under one Instant Answer, called the [Cheat Sheets Goodie](https://duck.co/ia/view/cheat_sheets).

![tmux cheat sheet](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Ftmux_cheat_sheet.png&f=1)

When your cheat sheet name is searched with any of the trigger words, your Instant Answer will be shown. For example, for the *vim* text editor, the Instant Answer will be triggered on: "vim cheatsheet", "vim commands", "vim guide", "vim shortcuts", and so on (full list of triggers available in [CheatSheets.pm](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/CheatSheets.pm))

## How to Add Your Cheat Sheet

If you have an idea for a cheat sheet, it's easy to add it to the DuckDuckGo Goodie repository. The following instructions assume you've already [set up your development environment](https://duck.co/duckduckhack/setup_dev_environment).

### Create a JSON File

Instead of creating an entirely new Instant Answer, you simply need to add **one JSON file** to the existing [Cheat Sheets Goodie directory](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/cheat_sheets).

To do this in Codio, use the left-hand panel to enter the `/zeroclickinfo-goodies` repository directory. Then use the file tree to click into the `/share/goodie/cheat_sheets` directory. 

Up in the **File menu**, click **"Create New File"**, and enter the name of your cheat sheet as a JSON file (make sure it's saving to the `cheat_sheets` directory). For example, if the trigger for your cheat sheet is "gopro cheat sheet" create a new file called `gopro.json`.

Erase any pre-filled contents, and enter the values for your cheat sheet using the [cheat sheet JSON syntax](#cheat-sheet-json-syntax). Feel free to copy the code in the following section into your new file as a convenient template.

With this method, there is no need to create a new Instant Answer. There is also no need to edit the `CheatSheets.pm` file, `cheat_sheets.js`, or `cheat_sheets.css`. Simply save your new file, push the changes to your repository on GitHub, and [submit a pull request](https://help.github.com/articles/creating-a-pull-request/).

### Cheat Sheet JSON Syntax

Below is a summary of the [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/vim.json) file, which displays a cheat sheet when searching for ["vim cheat sheet"](https://duckduckgo.com/?q=vim+cheat+sheet&ia=answer).

![vim cheat sheet](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvim_cheat_sheet.png&f=1)

The above Instant Answer was created by simply adding `vim.json`, summarized below. **We encourage you to copy the following working code into your new file, as a starting point for your cheat sheet.**

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
                "key": "[Ctrl] + [wt]",
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

### Syntax for `key` Property

Cheat sheet actions often have several key combinations, which you can indicate in the syntax of each `key` property.
Brackets, `[ ]`, or braces, `{ }`, are used to wrap key combinations in code blocks. For convenience, if you include no brackets or braces, the entire string will be shown in a code block.

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

Cheat sheet actions often have several key combinations, which you can express in any way you choose. The following are only suggestions; choose the most appropriate format for your subject.

#### Single Keys or Commands

There is no special syntax required for the string - for example, `"x"` or `":set color"`. The entire string will be shown in one code block.

#### Simultaneous Keys (e.g., pressing A and B together)

You might express simultaneous key presses as follows: 

- As separate code blocks, connected by a plus, e.g. `"[Ctrl]+[v]"`
- As a single code block, connected by a plus, e.g. `"[Ctrl+v]"`
- As a single code block, connected by a dash, e.g. `"[C-v]"`
	
#### Consecutive Keys (e.g., pressing A, then pressing B)

You might express consecutive key presses as follows:

- As separate code blocks separated by a space, e.g. `"[Ctrl-B] [x]"`
- As separate code blocks separated by a comma, e.g. `"[Ctrl-B], [x]"`
	
#### Alternative Keys (e.g., pressing either A or B)

You can express alternatives as follows:

- As separate code blocks separated by a forward slash, e.g. `"[?!=] / [?<!]"`
- As separate code blocks separated by "or", e.g. `"[?!=] or [?<!]"`

