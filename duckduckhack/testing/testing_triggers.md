# Testing

Testing is crucial to ensuring a smooth integration process. This section of the documentation walks you through the process of testing everything that you've written so far.

## Interactive Testing

Before reading this section, make sure you've worked through the the [Basic Goodie Tutorial](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_basic_tutorial.md) or the [Basic Spice Tutorial](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_basic_tutorial.md).

1. [Install DuckPAN](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/getting-started/installing_duckpan.md).

2. Go to your fork of the repository (a directory or folder on your computer).

    ```shell
    cd zeroclickinfo-goodies/
    ```

3. Install the repository requirements using duckpan.

    ```shell
    duckpan installdeps
    ```

    This command will install all the Perl modules used by the DuckDuckGo instant answers within your local repository. These requirements are defined in the [/dist.ini file](http://blog.urth.org/2010/06/walking-through-a-real-distini.html) (at the root).

4. Add your instant answer.

    Make a new file in the **lib/DDG/Goodie/** directory for Goodies or the **lib/DDG/Spice/** directory for Spice. The name of the file is the name of the instant answer followed by the extension **.pm** because it is a Perl module. For example, if the name of your instant answer was **"test instant answer"**, the file would be `TestInstantAnswer.pm`.

5. Test your triggers interactively.

    Type this command at the command line.

    ```shell
    duckpan query
    ```

    This command will initially output all of the instant answers available in your local repository. You should see your instant answer in this output.

    ```shell
    Using the following DDG::Goodie plugins:

     - DDG::Goodie::Xor (Words)
     - DDG::Goodie::SigFigs (Words)
     - DDG::Goodie::EmToPx (Words)
     - DDG::Goodie::Length (Words)
     - DDG::Goodie::ABC (Words)
     - DDG::Goodie::Chars (Words)
     ...
    ```

    The script will now proceed to an interactive prompt.

    ```shell
    (Empty query for ending test)
    Query:
    ```

    Now type in any query to see the response.

    ```shell
    Query: chars this is a test

    DDG::ZeroClickInfo  {
        Parents       WWW::DuckDuckGo::ZeroClickInfo
        Linear @ISA   DDG::ZeroClickInfo, WWW::DuckDuckGo::ZeroClickInfo, Moo::Object
        public methods (3) : is_cached, new, ttl
        private methods (0)
        internals: {
            answer   14,
            answer_type   "chars",
            is_cached   1
        }
    }
    ```

    There can be a lot of debugging output. Pay special attention to the **internals** section.

    ```shell
        internals: {
            answer   14,
            answer_type   "chars",
            is_cached   1
        }
    ```

    Here you can see the answer returned, as well as any **zci** keywords (by default there will be an **answer\_type** and **is\_cached** value).

    A blank query will exit interactive mode.

    ```shell
    Query:

    \_o< Thanks for testing!
    ```
    
	You can also run `duckpan server`--this is especially helpful for Goodies that output HTML.