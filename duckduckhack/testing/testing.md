# Testing

This section of the documentation walks you through the process of testing everything that you've written so far, and is crucial to ensuring a smooth integration process. Don't forget to write your test files!

## Interactive Testing

Before reading this section, make sure you've at least worked through the [basic tutorial](general.md#basic-tutorial).

1. Install our DuckDuckHack utility called [DuckPAN](https://github.com/duckduckgo/p5-app-duckpan). You can find instructions [here](https://github.com/duckduckgo/p5-app-duckpan/blob/master/README.md). It is also hosted [here](https://metacpan.org/module/App::DuckPAN) on MetaCPAN.

2. Go to your fork of the repository (a directory or folder on your computer).

    ```bash
    cd zeroclickinfo-goodies/
    ```

3. Install the repository requirements using duckpan.

    ```shell
    duckpan installdeps
    ```

    This command will install all the Perl modules used by the DuckDuckGo plugins within your local repository. These requirements are defined in the [/dist.ini file](http://blog.urth.org/2010/06/walking-through-a-real-distini.html) (at the root).

4. Add your plugin.

    Make a new file in the **lib/DDG/Goodie/** directory for Goodies or the **lib/DDG/Spice/** directory for Spice. The name of the file is the name of the plugin followed by the extension **.pm** because it is a Perl package. For example, if the name of your plugin was _TestPlugin_, the file would be _TestPlugin.pm_.

5. Test your trigger(s) interactively.

    Type this command at the command line.

    ```shell
    duckpan query
    ```

    First, this command will output all of the plugins available in your local plugin repository.

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

    You should see your plugin in there as well. When the output is finished it gives you an interactive prompt.

    ```
    (Empty query for ending test)
    Query:
    ```

    Now you can type in any query and see what the response will be.

    ```
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

    There is a lot of debugging output, but you will want to pay special attention to the internals section.

    ```shell
        internals: {
            answer   14,
            answer_type   "chars",
            is_cached   1
        }
    ```

    Here you can see the answer returned, as well as any **zci** keywords (by default there will be a default **answer_type** and **is_cached** value).

    Simply hit enter (a blank query) to exit interactive mode.

    ```shell
    Query:

    \_o< Thanks for testing!
    ```