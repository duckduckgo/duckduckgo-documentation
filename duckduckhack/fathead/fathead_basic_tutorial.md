This is a basic tutorial about how to add instant answer for query "***Hello world in C***" with DuckDuckGo in 10 steps!

# Fathead Tutorial

## Step 1

Clone the fathead repo from github with following command

    git clone git@github.com:/duckduckgo/zeroclickinfo-fathead.git

## Step 2

We need to create a perl file aka metafile (**HelloWorldInC.pm**) under **lib/DDG/Fathead** with basic 
details about the instant answer. For our "***Hello world in C***" example, basic metafile should look like 

    $ cat lib/DDG/Fathead/HelloWorldInC.pm 
    package DDG::Fathead::HelloWorldInC;
    use DDG::Fathead;

    primary_example_queries "hello world in c";

    secondary_example_queries
        "hello world c program",
        "hello world in c programming";
    description "Hello World programs in C language";
    name "HelloWorldInC";
    source "GitHub";
    code_url "https://raw.github.com/leachim6/hello-world/master/c/c.c";
    topics "geek", "programming";
    category "programming";
    1;

## Step 3

Now create directory named **HellowWorldInC** under **share** directory.

    mkdir -p zeroclickinfo-fathead/share/HelloWorldInC

## Step 4

Create a file **fetch.sh**. This shell script is invoked to fetch the data. 
For example, following script will retrieve the **c.c** file and place it under **download** directory

    $ cat zeroclickinfo-fathead/share/HelloWorldInC/fetch.sh 
    #!/bin/bash
    wget --directory-prefix=download https://raw.github.com/leachim6/hello-world/master/c/c.c

Please ensure all tmp files created under **download** directory. Go ahead and execute the 
**fetch.sh** script like

    #./fetch.sh

It should create a **c.c** file under **download** directory.

## Step 5 

Our objective is to parse the fetched data and create an output file (**output.txt**).
In order to parse, we write wrapper called **parse.sh** which will invoke the actual script
which can be written in your favorite language (.pl, .py, .rb, .js, etc)

    $ cat zeroclickinfo-fathead/share/HelloWorldInC/parse.sh 
    #!/bin/bash
    python parse.py

## Step 6 

As we can see above, we have the wrapper script which simply invokes following python script, which will
read **download/c.c** and format it then write into **output.txt** file.

    $ cat zeroclickinfo-fathead/share/HelloWorldInC/parse.py 
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

## Step 7

Now we will execute the python script via wrapper like 

    $ ./parse.sh 
    Parsed domain successfully

It has created the final **output.txt** file.

## Step 8

The content of output file is

    $ cat output.txt 
    hello world (c)		https://raw.github.com/leachim6/hello-world/master/c/c.c	Hello World in c (c.c)	#include<stdio.h>\n\nint main(void) {\n\tprintf("Hello World\\n");\n\treturn 0;\n}\n

As we need to complete the tutorial in 10 steps here comes 

## Step 8.5 

:) You can commit this **output.txt** along with perl,bash or python (.pm/.sh/.py) files since **output.txt** is less than **1MB**. 

## Step 9

You can create optional **data.url** file which will point to URL that contains the data to process.
Thus you don't need to perform fetch operation (step 4).

## Step 10

You can add specific instruction or any dependencies on a file named **README.txt**.
The final structure of your **share/HelloWorldInC** shoud look like 

    $ ls
    data.url  download  fetch.sh  output.txt  parse.py  parse.sh  README.txt


That's it, go ahead, create a patch and sent it for review.

