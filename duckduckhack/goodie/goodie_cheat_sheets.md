# Goodie Cheat Sheets

A popular (and perfect) use of Goodies is to create instant cheat sheets, available right from the DuckDuckGo search bar. To make adding a cheat sheet as quick as possible, we've brought all cheat sheets together under one Instant Answer, called the [Cheat Sheets Goodie](https://duck.co/ia/view/cheat_sheets).

![vim cheat sheet](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fvim_cheat_sheet.png&f=1)

## How to Add Your Cheat Sheet

If you have an idea for a cheat sheet, it's easy to add it to the DuckDuckGo Goodie repository. The following instructions assume you've already [set up your development environment](https://duck.co/duckduckhack/setup_dev_environment).

### Create a JSON File

Instead of creating an entirely new Instant Answer, you simply need to add **one JSON file** to the existing [Cheat Sheets Goodie directory](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/share/goodie/cheat_sheets).

To do this in Codio, use the left-hand panel to enter the `zeroclickinfo-goodies` repository directory. Then click into the `share/goodie/cheat_sheets` directory. 

In the file menu above, click **"Create New File"**, and enter the name of your cheat sheet as a JSON file (make sure it's saving in the `cheat_sheets` directory). For example, if the trigger for your cheat sheet is "gopro cheat sheet" create a new file called `gopro.json`.

Erase any pre-filled contents, and enter the values for your cheat sheet using the [cheat sheet JSON syntax](#cheat-sheet-json-syntax).

With this method, there is no need to create a new Instant Answer. There is also no need to edit the `CheatSheets.pm` file, `cheat_sheets.js`, or `cheat_sheets.css`. Simply save your new file, push the changes to your repository on github, and [submit a pull request](https://help.github.com/articles/creating-a-pull-request/).

### Cheat Sheet JSON Syntax

Below is a summary of the [`vim.json`](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/share/goodie/cheat_sheets/vim.json) file, which displays a cheat sheet when searching for ["vim cheat sheet"](https://duckduckgo.com/?q=vim+cheat+sheet&ia=answer).

All the top-level fields below are required. Syntax for the `key` property is explained below.

```javascript
{
    "name": "Vim",
    "description": "Text Editor",
    "metadata": {
        "sourceName": "VimCheatSheet",
        "sourceUrl": "https://duckduckgo.com"
    },
    "section_order": [      
        "Cursor movement",
        "Insert mode - inserting/appending text",
        ...
        "Tabs"
    ],
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
            ...
        ],        
        ... 
        "Insert mode - inserting/appending text": [
            {
                "key": "i",
                "val": "insert before the cursor"               
            }, 
            {
                "key": "I",
                "val": "insert at the beginning of the line"
            }
            ...
        ],  
        ...                  
    }
}
```

### Syntax for Key Presses

Cheat sheet keys often have several combinations, which you can indicate in the syntax of each `key` property.

#### Simultaneous Keys (e.g., pressing A and B together)

Simultaneous key presses are displayed in the same code block. There is no special syntax for the string - for example, `"x"` or `":set color"`. The entire string will be shown in the same code block.	
	
#### Consecutive Keys (e.g., pressing A, then pressing B)

Consecutive key presses are displayed in separate code blocks separated by a space. Wrap each key press in brackets and separate by a space - for example, `"[Ctrl-B] [x]"`.
	
#### Alternative Keys (e.g., pressing either A or B)

Alternative key presses are displayed in separate code blocks separated by a forward slash. Wrap each key press in brackets and separate by a slash - for example, `"[?!=] / [?<!]"`.

