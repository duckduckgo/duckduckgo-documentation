# Basic Fathead Tutorial

In this tutorial, we'll be making a Fathead instant answer that shows you a small "Hello World" example program for a given programming language. The end result works [like this](https://duckduckgo.com/?q=hello+world+scala) and the tab-delimited, output file our Fathead instant answer generates, will look like this:

###### output.txt

```
hello world (python) [TAB(S)] https://github.com/leachim6/hello-world        Hello World in python (python.py) [TAB(S)] #!/usr/bin/env python\nprint "Hello World"\n                        

hello world (postscript_page) [TAB(S)] https://github.com/leachim6/hello-world [TAB(S)] Hello World in postscript_page (postscript_page.ps) [TAB(S)] % run> gs -q postscript_page.ps\n/pt {72 div} def\n/y 9 def\n/textdraw {/Courier findfont 12 pt scalefont setfont 8 pt y moveto show} def\n\n72 72 scale\n0 0 0 setrgbcolor\n\n(Hello world!) textdraw\nshowpage\nquit                        

hello world (perl) [TAB(S)] https://github.com/leachim6/hello-world [TAB(S)] Hello World in perl (perl.pl) [TAB(S)] #!/usr/bin/perl\nprint "Hello World\\n";\n
```

## Naming our Fathead Package

To begin, open your favourite text editor like [gedit](http://projects.gnome.org/gedit/), notepad or [emacs](http://www.gnu.org/software/emacs/) and type the following:

```perl
package DDG::Fathead::HelloWorld;
# ABSTRACT: Provides an example "Hello World" program for a given programming language
```

## Import the Fathead Class

Next, type the following [use statement](https://duckduckgo.com/?q=perl+use) to import [the magic behind](https://github.com/duckduckgo/duckduckgo/tree/master/lib/DDG) our instant answer system.

```perl
use DDG::Fathead;
```

## Return True at EOF

Finally, all Perl packages that load correctly should [return a true value](http://stackoverflow.com/questions/5293246/why-the-1-at-the-end-of-each-perl-package) so add a 1 on the very last line, and make sure to also add a newline at the end of the file.

```perl
1;

```

At this point our Perl Package is mostly complete. We'll come back to this file later, when we have more to add.

## Define the Fetch.sh Shell Script

Every Fathead instant answer requires a **fetch.sh** file in its share directory. This shell script is invoked to fetch the data that our Fathead will use to produce its **output.txt** file. For example, following script will retrieve the **c.c** file and place it under **download** directory

###### fetch.sh

```shell
#!/bin/bash
git clone git://github.com/leachim6/hello-world.git download
```

In this case the "data" being used to produce the `output.txt` is actually a GitHub repository which is then parsed using a **python** script.

This of course is not the only way to "download" the required data. Most other Fatheads use `curl` and `wget` to download HTML or files that are then processed and parsed by their respective parsing scripts.

**\*\*Note:** All temporary files should be placed in a `/download` directory, within your Fathead's `/share` directory. Your `fetch.sh` script should create and utilize this directory.

## Define the Parsing Script

Every Fathead must parse the data it downloads in order to generate the required `output.txt` file. The parser can technically be written in any language however we ask that you use a more commonly used languages such as Perl, Python, JavaScript, Go, etc. If your chosen language requires a complicated setup or your parser has many external dependencies, it will likely make things much more difficult for us to do, so we ask that you **please try to keep things as simple and straightforward as possible**. Also, if the parser is written in a more uncommon language, it will make future maintenance or bug fixes very difficult for us and our community of developers, so please keep these in mind when writing your parser.

Seeing as every Fathead is unique and different we can't really tell you how to parse your data and produce your `output.txt` file. It is **suggested** that you look through the [Fathead repository](https://github.com/duckduckgo/zeroclickinfo-fathead/tree/master/share) to see how other developers have written their parsing scripts.

**\*\*Note:** Our development machines are running **Ubuntu 12.04**. These are the machines that will be used to test and run your parser, so **please make sure your language and dependencies are compatible with our environment**.

For the purpose of the tutorial, let's take a quick look at the approach used in the **HelloWorld** Fathead:

###### parse.py

```python
if __name__ == "__main__":
    # setup logger
    logging.basicConfig(level=logging.INFO,format="%(message)s")
    logger = logging.getLogger()
    
    # dump config items
    count = 0
    with open("output.txt", "wt") as output_file:
        for filepath in glob.glob('download/*/*'):
            _,filename = os.path.split(filepath)
            # ignore some "languages"
            if filename not in ['ls.ls', 'readlink.readlink', 'piet.png']:

                language,_ = os.path.splitext(filename)
                with open(filepath, 'r') as f:
                    source = f.read()
                source = source.replace('\\n', '~~~n')
                source = source.replace('\n', '\\n')
                source = source.replace('~~~n', '\\\\n')
                source = source.replace('\t', '\\t')
                    
                item = HelloWorldItem(language, filename, source)
                if count % 10 == 0:
                    logger.info("%d languages processed" % count )

                count += 1
                output_file.write(str(item))
    logger.info("Parsed %d domain rankings successfully" % count)
```

This uses a relatively simple loop, `for filepath in glob.glob('download/*/*'):` which iterates over each of the files in the repository our `fetch.sh` script cloned into the `download` directory. After doing some checks to make sure the files is a "Hello World" program, it opens the file, reads the file, escapes newline (`\n`) and tab (`\t`) characters and then then "parses" the file to create an `item` using the `HelloWorldItem` class:

###### parse.py (continued)

```python
class HelloWorldItem:
  def __init__(self, language, filename, source):
    self.language = language
    self.filename = filename
    self.source = source

  def __str__(self):
    
    fields = [ "hello world (%s)" % self.language,
               "", # namespace
               "https://github.com/leachim6/hello-world",
               "Hello World in %s (%s)" % (self.language, self.filename),
               self.source, # synposis (code)
               "", # details
               "", # type
               "", # lang
             ]

    output = "%s\n" % ("\t".join(fields))

    return output
```

The `HelloWorldItem` class works by defining the string representation of itself, which we later use to print our object into `output.txt`: `output_file.write(str(item))`.

The most important thing to note about the string representation function, `def __str__(self):`, is that it creates an array containing the relevant information we need to pass along to `output.txt`, which **includes a few blank lines to represent the optional output fields we have not used** and then joins them with tab characters (`\t`). It also appends a newline (`\n`) at the end of our built string. This string now represent a single line in our `output.txt` file and denotes the **title**, **abstract**, **synopsis** and the **source_url**.

## Step 6 

As we can see above, we have the wrapper script which simply invokes the following Python script, which will
read **download/c.c** and format it then write into **output.txt** file.

```python
# content of  zeroclickinfo-fathead/share/HelloWorldInC/parse.py 
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
import  logging, os

class HelloWorldItem:
  def __init__(self, language, filename, source):
    self.language = language
    self.filename = filename

    source = source.replace('\\n', '~~~n')
    source = source.replace('\n', '\\n')
    source = source.replace('~~~n', '\\\\n')
    self.source = source.replace('\t', '\\t')

  def __str__(self):
    fields = [ "hello world (%s)" % self.language,
               "", # namespace
               "https://raw.github.com/leachim6/hello-world/master/c/c.c",
               "Hello World in %s (%s)" % (self.language, self.filename),
               self.source, # synposis (code)
             ]

    output = "%s\n" % ("\t".join(fields))
    return output

if __name__ == "__main__":
    # setup logger
    logging.basicConfig(level=logging.INFO,format="%(message)s")
    logger = logging.getLogger()
    
    # dump config items into output.txt
    with open("output.txt", "wt") as output_file:
        for filepath in os.listdir('download/'):
	    filepath =  os.path.join('download/',filepath)
            _,filename = os.path.split(filepath)
            language,_ = os.path.splitext(filename)

            with open(filepath, 'r') as f:
                source = f.read()
                    
            item = HelloWorldItem(language, filename, source)
            output_file.write(str(item))

    logger.info("Parsed domain successfully")
```

## Step 7

Now we will execute the Python script via wrapper like 

```shell
$ ./parse.sh 
Parsed domain successfully
```

It has created the final **output.txt** file.

## Step 8

The content of output file is

```shell
$ cat output.txt 
hello world (c)		https://raw.github.com/leachim6/hello-world/master/c/c.c	Hello World in c (c.c)	#include<stdio.h>\n\nint main(void) {\n\tprintf("Hello World\\n");\n\treturn 0;\n}\n
```

As we need to complete the tutorial in 10 steps here comes 

## Step 8.5 

:) You can commit this **output.txt** along with Perl,Bash script or Python (.pm/.sh/.py) files since **output.txt** is less than **1MB**. 

## Step 9

You can create optional **data.url** file which will point to URL that contains the data to process.
Thus you don't need to perform fetch operation (step 4).

## Step 10

You can add specific instruction or any dependencies on a file named **README.txt**.
The final structure of your **share/HelloWorldInC** shoud look like 

```shell
$ ls
data.url  download  fetch.sh  output.txt  parse.py  parse.sh  README.txt
```


That's it, go ahead, create a patch and sent it for review.

