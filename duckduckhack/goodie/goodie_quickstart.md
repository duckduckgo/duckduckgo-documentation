# My First Goodie Instant Answer!

**If you are new to DuckDuckHack, you're in the right place.** This Goodie Quick Start is meant to show you the basics of DuckDuckHack by building a simple Instant Answer that will look like [this](https://duckduckgo.com/?q=zekiel+duckduckhack&ia=answer). 

If you're already familiar with how Instant Answers are built, feel free to move along to the [Basic Tutorial](https://duck.co/duckduckhack/goodie_basic_tutorial).

## Set Up Your Development Environment

By this point you should have already **set up your development environment** to be ready to code. If you need help with that (or anything else), please shoot us an email at: [open@duckduckgo.com](mailto:open@duckduckgo.com) and we'll jump on the chance to help!

## Creating Your First Goodie

In this tutorial we'll be making a super-simple Goodie by changing some template files.

We'll be using the **DuckPAN tool** to generate this boilerplate code for us. The DuckPAN tool is an application we built to help DuckDuckHack developers save time. Aside from generating boilerplate code, you'll also use it to run and test your instant answer contribution.

1. Click the "**DuckPAN New Goodie**" button on the command bar. The Terminal should prompt you to enter a name for your Instant Answer.
2. Type **`IsAwesome::GitHubUsername`** (replacing `GitHubUsername` with your actual GitHub username), then press "**Enter**". From this point on, whenever you see, ***GitHubUsername***, replace it with your actual GitHub username.

    ```
    [04:31 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ cd ~/workspace/zeroclickinfo-goodies/ && duckpan new
    Please enter a name for your Instant Answer: IsAwesome::GitHubUsername
    ```

	*Usually you'll be typing in just a regular name like `Calculator` with no prefix, but because so many community members are creating `IsAwesome` projects, we wanted to keep them together in their own directory. Hence the `IsAwesome::` prefix.*

3. DuckPAN should print some text, confirming that your first Goodie was created:

    ```
    [04:31 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ cd ~/workspace/zeroclickinfo-goodies/ && duckpan new duckpan new
    Please enter a name for your Instant Answer : IsAwesome::GitHubUsername

    Created file: ./lib/DDG/Goodie/IsAwesome/GitHubUsername.pm


    Created file: ./t/IsAwesome/GitHubUsername.t


    Successfully created Goodie: IsAwesome::GitHubUsername
    ```

	DuckPAN created two files: a code file, and a test file, each in their proper locations in the repository. That's all it takes to make a Goodie. 

    Currently, these two generated files only contain boilerplate code and comments, which saves us a lot of time. Next, we'll customize the files to our liking and get your Goodie working.

4. Let's start by editing your code file first. Press "**Ctrl+O**" (Cmd+O on a Mac), then type "**GitHubUsername.pm**" and press "**Enter**". This will open the file for editing in Codio's text editor. (Vim, Emacs and Nano are also available). 

	It should look like this:

    ```perl
    package DDG::Goodie::IsAwesome::GitHubUsername;
    # ABSTRACT: Write an abstract here
    # Start at https://duck.co/duckduckhack/goodie_overview if you are new
    # to Instant Answer development

    use DDG::Goodie;

    zci answer_type => "is_awesome_git_hub_username";
    zci is_cached   => 1;

    # Metadata.  See https://duck.co/duckduckhack/metadata for help in filling out this section.
    name "IsAwesome GitHubUsername";
    description "Succinct explanation of what this Instant Answer does";
    primary_example_queries "first example query", "second example query";
    secondary_example_queries "optional -- demonstrate any additional triggers";
    # Uncomment and complete: https://duck.co/duckduckhack/metadata#category
    # category "";
    # Uncomment and complete: https://duck.co/duckduckhack/metadata#topics
    # topics "";
    code_url "https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/IsAwesome/GitHubUsername.pm";
    attribution github => ["GitHubAccount", "Friendly Name"],
                twitter => "twitterhandle";

    # Triggers
    triggers any => "triggerWord", "trigger phrase";

    # Handle statement
    handle remainder => sub {

        # optional - regex guard
        # return unless qr/^\w+/;

        return unless $_; # Guard against "no answer"

        return $_;
    };

    1;
    ```

5. Change the **`trigger`** (line 25) to this:

    ```perl
    triggers start => "duckduckhack githubusername";
    ```

    This tells the Instant Answer system to trigger your Goodie when the query **starts** with the phrase "**duckduckhack githubusername**".

    **Note:** Triggers must be entered in **lowercase**. If your username has uppercase letters, **don't worry**, a lowercased trigger will always work because we compare the *lowercased query* against the trigger.

6. Change the **`handle`** statement (lines 28-36) to this:

    ```perl
    handle remainder => sub {

        return "GitHubUsername is awesome and has successfully completed the DuckDuckHack Goodie tutorial!";
    };
    ```

    This will make your Goodie tell everyone that you're totally awesome!
    
    **Note:** Do ***not*** remove the `1;` from the end of the file. This is required because Perl modules must return a true value.

7. Switch back to your Terminal by clicking on the "**Terminal**" tab.
8. Type **`duckpan server`** and press "**Enter**". The Terminal should print some text and let you know that the server is listening on port 5000.

    ```
    Starting up webserver...

    You can stop the webserver with Ctrl-C

    HTTP::Server::PSGI: Accepting connections at http://0:5000/
    ```

    **Note:** If you modify **GitHubUsername.pm** (or any other Perl files) while DuckPAN Server is *running*, you **must restart the server** for the changes to take effect. In the Terminal, press "**Ctrl+C**" to shut down the DuckPAN Server. Type **`duckpan server`** and press "**Enter**" to start it again.

9. Click the "**DuckPAN Server**" button at the top of the screen. A new browser tab should open and you should see the DuckDuckGo Homepage. Type "**duckduckhack GitHubUsername**" and press "**Enter**".
10. You should see a DuckDuckGo Instant Answer displaying the text, "**GitHubUsername is awesome and has successfully completed the DuckDuckHack Goodie tutorial!**". This is the text we told your Goodie to **`return`**!
11. In the Terminal, press "**Ctrl+C**" to shut down the DuckPAN Server. The Terminal should return to a regular command prompt.

    ```
    Starting up webserver...

    You can stop the webserver with Ctrl-C

    HTTP::Server::PSGI: Accepting connections at http://0:5000/
    ^C
    [04:32 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$
    ```

**Congrats!** Your first Goodie is working! You specified its **`trigger`** and told it what to **`return`**. You're almost done! Now you should write a test to make sure your Goodie only triggers when we want it to.


## Writing Your First Goodie Test File

1. Let's edit your corresponding test file. Press "**Ctrl+O**" (Cmd+O on a Mac), then type "**GitHubUsername.t**" and press "**Enter**". This will open the file for editing in Codio's text editor. 

	It should look like this:

    ```perl
    #!/usr/bin/env perl

    use strict;
    use warnings;
    use Test::More;
    use DDG::Test::Goodie;

    zci answer_type => "is_awesome_git_hub_username";
    zci is_cached   => 1;

    ddg_goodie_test(
        [qw( DDG::Goodie::IsAwesome::GitHubUsername )],
        # At a minimum, be sure to include tests for all:
        # - primary_example_queries
        # - secondary_example_queries
        'example query' => test_zci('query'),
        # Try to include some examples of queries on which it might
        # appear that your answer will trigger, but does not.
        'bad example query' => undef,
    );

    done_testing;
    ```

	_Make sure to change **all** instances of `GitHubUsername` in the file to your user name._

2. Change the **`ddg_goodie_test`** function (lines 11-20) to this:

    ```perl
    ddg_goodie_test(
        [qw(
            DDG::Goodie::IsAwesome::GitHubUsername
        )],
        'duckduckhack GitHubUsername' => test_zci('GitHubUsername is awesome and has successfully completed the DuckDuckHack Goodie tutorial!'),
        'duckduckhack GitHubUsername is awesome' => undef,
    );
    ```

    This test file now ensure two things:

    1. For the query "**duckduckhack GitHubUsername**", your Goodie returns "GitHubUsername is awesome and has successfully completed the DuckDuckHack Goodie tutorial!".
    2. For the query "**duckduckhack GitHubUsername is awesome**", your Goodie returns **`undef`**, meaning it won't display any result for that query.

	*Can you guess what the `test_zci()` function does? ZCI stands for Zero Click Info. The `test_zci()` function verifies what is being returned specifically in the Zero Click Info section of the search page.*


3. Switch back to your Terminal by clicking on the "**Terminal**" tab.
4. Type **`prove -Ilib t/IsAwesome/GitHubUsername.t`** and press "**Enter**". The prompt should print the results of the test.

    ```
    [04:33 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ prove -Ilib t/IsAwesome/GitHubUsername.t
    t/IsAwesome/GitHubUsername.t .. 1/?
    #   Failed test 'Checking for not matching on duckduckhack GitHubUsername is awesome'
    #   at /home/codio/perl5/perls/perl-5.18.2/lib/site_perl/5.18.2/DDG/Test/Block.pm line 62.
    #          got: 'DDG::ZeroClickInfo=HASH(0x2e5b628)'
    #     expected: undef
    # Looks like you failed 1 test of 2.
    t/IsAwesome/GitHubUsername.t .. Dubious, test returned 1 (wstat 256, 0x100)
    Failed 1/2 subtests

    Test Summary Report
    -------------------
    t/IsAwesome/GitHubUsername.t (Wstat: 256 Tests: 2 Failed: 1)
      Failed test:  2
      Non-zero exit status: 1
    Files=1, Tests=2,  0 wallclock secs ( 0.02 usr  0.02 sys +  0.14 cusr  0.04 csys =  0.22 CPU)
    Result: FAIL
    ```


    Uh oh! We failed a test! The output says a `DDG::ZeroClickInfo` object was returned, but the test was expecting `undef`. Let's update our code to make this test pass.

4. Switch back to your text editor by clicking the tab if it's still open, or open the "**GitHubUsername.pm**" file with "**Ctrl+O**" (Cmd+O on a Mac).
5. Update the **`handle`** statement to this:

    ```perl
    handle remainder => sub {
        return if $_;
        return "GitHubUsername is awesome and has successfully completed the DuckDuckHack Goodie tutorial!";
    };
    ```

    Now your Goodie will return nothing (i.e. `undef`) if `$_` has a value. Within our `handle` function, `$_` is a special variable that takes on the value of **`remainder`**. The `remainder` refers to the rest of the query after removing our matched **`trigger`**. So for the query "duckduckhack GitHubUsername is awesome", the value of `$_` will be:

    ```
    "duckduckhack GitHubUsername is awesome" - "duckduckhack GitHubUsername" = `is awesome`
    ```

6. Switch back to your text editor by clicking the "**Terminal**" tab.
7. Type **`prove -Ilib t/IsAwesome/GitHubUsername.t`** and press "**Enter**". The prompt should print the results of the test again.

    ```
    [04:34 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ prove -Ilib t/IsAwesome/GitHubUsername.t
    t/IsAwesome/GitHubUsername.t .. ok
    All tests successful.
    Files=1, Tests=2,  0 wallclock secs ( 0.02 usr  0.01 sys +  0.15 cusr  0.03 csys =  0.21 CPU)
    Result: PASS
    ```

    **Success!** The test passes, meaning that your Goodie will only `return` an answer when our query `start`s with the `trigger` "**duckduckhack GitHubUsername**" and has no `remainder` after that.

	_Still not passing? Make sure you changed **all** instances of `GitHubUsername` in the file to your user name._

**Congrats!** You've written and tested your first Goodie! Feels great, doesn't it?

Of course, this was just a taste of all the things you can create using a Goodie. Fortunately, you're now super ready to tackle the [Basic Tutorial](https://duck.co/duckduckhack/goodie_basic_tutorial). You will find many things familiar there and be well on your way to advanced Goodie functionality.

Do you enjoy looking under the hood and learning by example? You'll enjoy casually browsing other Goodies in the [`/lib/DDG/Goodie`](https://github.com/duckduckgo/zeroclickinfo-goodies/tree/master/lib/DDG/Goodie) directory of the repository. Take a look at their their **.pm** files and look at the `triggers`. You can even test them all using the `duckpan server` command you learned - or live up on [DuckDuckGo.com](http://www.duckduckgo.com).

## Bonus - See Your Instant Answer live on DuckDuckGo.com

This bonus section will walk you through submitting the IsAwesome Goodie you just created for review and acceptance into the *live DuckDuckGo.com codebase*. If you'd rather jump straight in and work on *your* idea, don't worry about this for now. You'll find this information in the rest of the docs as well.

1. Open "**GitHubUsername.pm**" in the editor and change the **`Metadata`** (lines 11-20) to this:

    ```perl
    name "IsAwesome GitHubUsername";
    description "My first Goodie, it lets the world know that GitHubUsername is awesome";
    primary_example_queries "duckduckhack GitHubUsername";
    category "special";
    topics "special_interest", "geek";
    code_url "https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/IsAwesome/GitHubUsername.pm";
    attribution github => ["https://github.com/GitHubUsername", "GitHubUserName"],
                twitter => "TwitterUserName";
    ```

    **Note:** The "TwitterUserName" is optional. If you don't want us to attribute your Twitter handle, just remove that line. Make sure the `attribution` statement still ends with a semicolon (`;`) though!

    If you do fill in your Twitter handle, please **leave out the @ symbol**. There are also other forms of attribution you can use listed [here](https://duck.co/duckduckhack/metadata#attribution).

2. Update the **`Abstract`** (top of the file) to this:

    ```perl
    # ABSTRACT: GitHubUsername's first Goodie
    ```

    and remove any remaining comments from the code:

    ```
    # Start at https://duck.co/duckduckhack/goodie_overview if you are new
    # to Instant Answer development

    # Metadata.  See https://duck.co/duckduckhack/metadata for help in filling out this section.

    # Uncomment and fill out before submitting

    # Triggers

    # Handle Statement
    ```

3. Switch back to the "**Terminal**" tab.

4. Type **`git add .`**, then press enter.

	*This command tells the git repository to include and track changes to the two files you've created. Even though the files were physically located in the repository, we need to explicitly tell git to track them.*
	
5. Type **`git commit -m "Created my first Goodie"`** and press **`Enter`**. Git should print some text confirming the changes that have been committed.

    ```
    [04:35 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ git commit -m "Created my first Goodie"
    [master 6aeb841] Created my first Goodie
     2 files changed, 55 insertions(+)
     create mode 100644 lib/DDG/Goodie/IsAwesome/GitHubUsername.pm
     create mode 100644 t/IsAwesome/GitHubUsername.t
    ```

    This shows you've **created** two new files, **`lib/DDG/Goodie/IsAwesome/GitHubUsername.pm`** and **`t/IsAwesome/GitHubUsername.t`**.

6. Type **`git push`** and press **`Enter`**. Enter your GitHub Username and password, press **`Enter`** after each. Git will print some text to the Terminal letting you know that your code has been pushed to GitHub.

    ```
    [04:35 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ git push
    Username for 'https://github.com': GitHubUsername
    Password for 'https://GitHubUsername@github.com':
    Counting objects: 75, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (60/60), done.
    Writing objects: 100% (75/75), 11.05 KiB | 0 bytes/s, done.
    Total 75 (delta 36), reused 0 (delta 0)
    To https://github.com/GitHubUsername/zeroclickinfo-goodies.git
       138f5bc..c69c517  master -> master
    ```

7. Open a **new browser tab** and go to **`https://github.com/githubusername/zeroclickinfo-goodies`**.
8. Click the "**Pull Request**" button (grey text, middle of the screen).
9. Review the changes and click "**Create Pull Request**".
10. Enter a title for your pull request, "**GitHubUsername's First Goodie**" or similar is perfect.
11. Copy the "Goodie Pull Request Template" from [here](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-goodies/master/pull_request_template_goodie.md), and paste it into the text box that says "**Leave a comment**".
12. Answer the questions in the Pull Request Template (this helps the DDG Staff and Community understand your Pull Request better).
13. Go back to your Codio.com browser tab.
14. Open the "Terminal" tab and type `duckpan server`, then press "**Enter**".
15. Click the DuckPAN Server button, and search for "**duckduckhack GitHubUsername**"
16. Take a screen shot of your awesome Instant Answer result, save it somewhere easily accessible.
17. Go back to your GitHub.com browser tab.
18. Drag-and-Drop your screen shot into the textbox. The picture will be uploaded and a link will be generated.
19. Move the screenshot link **above the "Checklist"** in the pull request template. (where it asks for a screen shot).
20. Click **"Create Pull Request"**.
21. Now sit back and relax. When a Community Leader or DDG staff member has a chance, they'll review your Goodie, give you any feedback (if necessary) and merge it in. Once it's merged, it will be deployed to the site and should be live within a few days. **We'll be sure to let you know once it's live!**

**Congrats!** You've now seen what creating an Instant Answer is like. Now, you're prepared to move on and create one of your own!
