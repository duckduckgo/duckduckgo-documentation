# My First Goodie Instant Answer!

This is a quick start tutorial designed to teach about Goodie Instant Answers. You'll be making and submitting your first Instant Answer to the DuckDuckHack project. In order to get moving quickly, we'll be using a web based IDE, [Codio](https://codio.com), along with a pre-configured DuckDuckHack environment.

This tutorial assumes zero knowledge and walks you through every step required. No guesswork needed!


## Before We Get Going...

Aside from a working internet connection and a computer, there are two important things you'll need to get started:

- a **free** Codio account
    + Codio provides a web-based code editor where you will be creating and testing new Instant Answers. We're using Codio because it works across all platforms (Windows, Linux, Mac) and comes preconfigured with the necessary software for Instant Answer development.
- a **free** GitHub account
    + GitHub provides a place for you to save your code on the internet.
    + When your Instant Answer is ready for us to review, you'll use GitHub to send us your code!


## Sign up for a GitHub Account

*Already have a GitHub Account? Perfect, move on to [the next step](#sign_up_for_a_codio_account)!*

If you're new to programming, GitHub is a well known, popular tool that many individuals and companies use to save their code. Many open-source projects (such as DuckDuckHack) are hosted on GitHub and anyone with an account can contribute. GitHub is a great tool that'll you likely be using long after this tutorial. To get started, let's sign up!

1. Go to https://github.com/join and enter the reqiured information, then click "**Create an Account**"
2. Click "**Finish Signup**" to continue with a **Free** GitHub account.

**Congrats!** You now have a GitHub account.


## Sign up for a Codio Account

Next, you'll need to get an account for Codio:

*Already have a Codio Account? Perfect, move on to [the next step](#fork_the_duckduckhack_project_on_codio)!*

1. Go to https://codio.com and click "Sign Up", at the top right corner.
2. Click "**Sign Up via GitHub**".
3. Enter your GitHub login details and then click"**Sign In**".
4. Click "**Authorize Application**" to continue.
5. In the new screen, enter the required details and click "**Create Account**".

**Congrats!** You now have a Codio account. You'll notice that you didn't need to provide a password, that's because you've logged in to Codio using your GitHub account. As long as you can login to your GitHub account, you can also login to Codio. Now let's get started with setting up your Codio environment!


## Fork the DuckDuckHack Project on Codio

1. Go to https://codio.com/duckduckgo/duckduckhack and click "**Project**" at the top left corner.
2. In the dropdown, select the "**Fork**" option.

    ![Codio Fork](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckpan/assets/codio_fork.png)

3. In the pop-up window, select "**Clone both the Project and its Box**".

    ![Codio Fork Both](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckpan/assets/codio_fork_both.png)

4. Wait a minute while the project forks...
5. You should now see a new window with three panes. It should say "**DuckDuckHack**" at the top of the left pane.

**Congrats!** You've now successfully forked the DuckDuckHack environment. Now, let's grab the DuckDuckHack Goodie code (from GitHub.com) and start learning!


## Fork the DuckDuckHack Goodie Repository on GitHub

In order to test out and create your own Goodie Instant Answer, you'll need the open-source code that DuckDuckGo hosts on GitHub.com. We're now going to "fork" that code, so you'll have your own personal copy which you can modify.

1. Go to https://github.com/duckduckgo/zeroclickinfo-goodies. This is the home page for the DuckDuckHack Goodie repository (also known as a "repo").
2. Do you see your username in the top right corner?
    - **Yes**? Perfect. Move on to the next step.
    - **No**? Click "**Sign In**", then enter your details and click "**Sign In**".
3. Click "**Fork**", near the top-right corner.
4. Wait while the repo forks...
5. You should see a page that looks nearly identical to the Goodie repo home page. The URL should be different though, it should look like "**https://github.com/\<your user name\>/zeroclickinfo-goodie**". This is the URL for your personal copy of the DuckDuckHack Goodie code.
6. **Keep this URL handy, we'll be using it in a minute!**


## Clone your Goodie Repository onto your Codio Machine

Now we need to "clone" the code from GitHub to your Codio box so you can see it, modify it and run it!

1. Go to https://codio.com/home/projects.
    - See a "**Sign In**" screen? Use the "**Sign in via GitHub**" method like you did before (see Step #2 [here](#sign_up_for_a_codio_account)).
2. Click "**DuckDuckHack**" to select that project.
3. You should now see the three-paned window we previously saw. We're going to change the layout a bit, press **Ctrl+Alt+R** (Cmd+Alt+R on a Mac). *You can also click View->Layouts->Default from the command bar at the top*.
4. Press **Shift+Alt+T** to open a new Terminal. *You can also click Tools->Terminal from the command bar at the top*.You should see the right side pane change into a black command prompt.
5. Type **`git clone <Your GitHub URL Here>.git`** into the Terminal, replacing `<Your GitHub URL Here>` accordingly. It should look something like this:

    ```
    [04:30 PM codio@buffalo-pixel workspace {master}]$ git clone https://github.com/githubusername/zeroclickinfo-goodies.git
    ```

6. Press "**Enter**". You should see the Terminal print out some text that looks like this:

    ```
    [04:30 PM codio@buffalo-pixel workspace {master}]$ git clone https://github.com/githubusername/zeroclickinfo-goodies.git
    Cloning into 'zeroclickinfo-goodies'...
    remote: Counting objects: 18623, done.
    remote: Compressing objects: 100% (8083/8083), done.
    remote: Total 18623 (delta 8084), reused 18179 (delta 7868)
    Receiving objects: 100% (18623/18623), 5.50 MiB | 9.51 MiB/s, done.
    Resolving deltas: 100% (8084/8084), done.
    Checking connectivity... done.
    [04:30 PM codio@buffalo-pixel workspace {master}]$ git clone https://github.com/githubusername/zeroclickinfo-goodies.git
    ```

7. The filetree on the left side should update, there should be a new "**zeroclickinfo-goodies**" directory.

<!-- PICTURE OF UPDATE DIRECTORY -->

**Congrats!** You've now cloned your fork of the Goodie repo onto your Codio machine. Now, let's code our first Goodie and run it!

------

*Curious to know what we just did?*

You just used a program called **Git**, to **clone** (copy) the Git repository (a special file containing all the code) located at "https://github.com/GitHubUsername/zeroclickinfo-goodies.git" onto your Codio machine. Git automatically creates a new folder based on the name of the repository it's cloning and copies the code into it. In our case, Git create a folder, "zeroclickinfo-goodies", and copied all the code into there.


## Creating Your First Goodie

Now we're going to create our first Goodie! We'll be using the DuckPAN tool to generate some boilerplate code for us to make things easier.

1. Click the "**DuckPAN New Goodie**" button on the command bar. The should Terminal prompt you to enter a name for your Instant Answer.
2. Type **`IsAwesome::GitHubUsername`**, replacing `GitHubUsername` with your actual GitHub username, then press "**Enter**". From this point on, whenever you see, ***GitHubUsername***, replace it with your actual GitHub username.

    ```
    [04:31 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ cd ~/workspace/zeroclickinfo-goodies/ && duckpan new
    Please enter a name for your Instant Answer: IsAwesome::GitHubUsername
    ```

3. DuckPAN should print some text, confirming that your first Goodie was created:

    ```
    [04:31 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ cd ~/workspace/zeroclickinfo-goodies/ && duckpan new duckpan new
    Please enter a name for your Instant Answer : IsAwesome::GitHubUsername

    Created file: ./lib/DDG/Goodie/IsAwesome/GitHubUsername.pm


    Created file: ./t/IsAwesome/GitHubUsername.t


    Successfully created Goodie: IsAwesome::GitHubUsername
    ```

    These two generates files only contain boilerplate code and comments. We'll have to complete the code in order to get your new Goodie working!

4. Press "**Ctrl+O**" (Cmd+O on a Mac), then type "**GitHubUsername.pm**" and press "**Enter**". This will open the file for editing in Codio's text editor. (If you prefer a Terminal text editor, Vim, Emacs and Nano are also available). It should look like this:

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
    # Uncomment and fill out before submitting
    # category "";
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

5. Change the **`trigger`** (line 23) to this:

    ```perl
    triggers start => "duckduckhack githubusername";
    ```

    This tells the Instant Answer system to trigger your Goodie when the query **starts** with the phrase "**duckduckhack githubusername**".

6. Change the **`handle`** statement (lines 28-36) to this:

    ```perl
    handle remainder => sub {

        return "GitHubUsername is awesome and has successfully completed the DuckDuckHack Goodie tutorial!";
    };
    ```

    This will make your Goodie tell everyone that you're totally awesome!

7. Switch back to you Terminal by clicking on the "**Terminal**" tab.
8. Ttype **`duckpan server`** and press "**Enter**". The Terminal should print some text and let you know that the server is listening on port 5000.

    ```
    Starting up webserver...

    You can stop the webserver with Ctrl-C

    HTTP::Server::PSGI: Accepting connections at http://0:5000/
    ```

9. Click the "**DuckPAN Server**" button at the top of the screen. A new browser tab should open and you should see the DuckDuckGo Homepage. Type "**duckduckhack GitHubUsername**" and press "**Enter**".
10. You should see a DuckDuckGo Instant Answer displaying the text, "GitHubUsername is awesome and has successfully completed the DuckDuckHack Goodie tutorial!". This is the text we told your Goodie to **`return`**!
11. In the Terminal, press "**Ctrl+C**" (Cmd+C on a Mac) to shut down the DuckPAN Server. The Terminal should return to a regular command prompt.

```
Starting up webserver...

You can stop the webserver with Ctrl-C

HTTP::Server::PSGI: Accepting connections at http://0:5000/
^C
[04:32 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$
```

Congrats! Your first Goodie is working! You specified its **`trigger`** and told it what to **`return`**. You're almost done, we should write a test to make sure the Goodie only triggers when we want it to.


## Writing Your First Goodie Test File

1. Press "**Ctrl+O**" (Cmd+O on a Mac), then type "**GitHubUsername.t" and press "**Enter**". This will open the file for editing in Codio's text editor. It should look like this:

    ```perl
    #!/usr/bin/env perl

    use strict;
    use warnings;
    use Test::More;
    use DDG::Test::Goodie;

    zci answer_type => "is_awesome_git_hub_username";
    zci is_cached   => 1;

    ddg_goodie_test(
        [qw(
            DDG::Goodie::IsAwesome::GitHubUsername
        )],
        'example query' => test_zci('query')
    );

    done_testing;
    ```

2. Change the **`ddg_goodie_test`** (lines 11-16) to this:

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

3. Switch back to you Terminal by clicking on the "**Terminal**" tab.
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


    Uh oh! We failed a test! The output says a DDG::ZeroClickInfo object was returned, but the test was expecting `undef`. Let's update our code to make this test pass.

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

    Sucess! The test passes, meaning that your Goodie will only `return` an answer when our query `start`s with the `trigger` "**duckduckhack GitHubUsername**" and has no `remainder` after that.

Congrats! You've written and tested your first Goodie! There's so much more that Goodies can do though, checkout our other tutorials to learn more. You can also explore the Goodie repo by looking at the other Goodies in the `/lib/DDG/Goodie` directory. Read their **.pm** files and look at the `triggers`. You can test them all in the `duckpan server`.

At this point you're done the tutorial, but we have a bonus surprise for you...


## Bonus - See Your Instant Answer live on DuckDuckGo.com

1. Open "**GitHubUsername.pm**" in the editor and change the Metadata to this:

    ```perl
    # Metadata.  See https://duck.co/duckduckhack/metadata for help in filling out this section.
    name "IsAwesome GitHubUsername";
    description "My first Goodie, it let's the world know GitHubUsername is awesome";
    primary_example_queries "duckduckhack GitHubUsername";
    category "";
    topics "";
    code_url "https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/lib/DDG/Goodie/IsAwesome/GitHubUsername.pm";
    attribution github => ["https://github.com/GitHubUsername", "GitHubUserName"],
                twitter => "TwitterUserName";
    ```

    Note: The "TwitterUserName" is optional. If you don't want us to attribute your Twitter handle, just remove that line. Make sure the `attribution` statement still ends with a semicolon (`;`) though!

2. Switch back to the "**Terminal**" tab.
3. Type **`git add .`**, then press enter.
4. Type **`git commit -m "Created my first Goodie"`** and press **`Enter`**. Git should print some text confirming the changes that have been committed.

    ```
    [04:35 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ git commit -m "Created my first Goodie"
    [master 6aeb841] Created my first Goodie
     2 files changed, 55 insertions(+)
     create mode 100644 lib/DDG/Goodie/IsAwesome/GitHubUsername.pm
     create mode 100644 t/IsAwesome/GitHubUsername.t
    ```

    This shows you've **created** two new files, **`lib/DDG/Goodie/IsAwesome/GitHubUsername.pm`** and **`t/IsAwesome/GitHubUsername.t`**.

5. Type **`git push`** and press **`Enter`**. Enter your GitHub Username and password, press **`Enter`** after each. Git will print some text to the Terminal letting you know that your code has been pushed to GitHub.

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

6. Open a **new browser tab** and go to https://github.com/githubusername/zeroclickinfo-goodies.
7. Click the "**Pull Request**" button.
8. Review the changes.
9. Enter a title for your pull request, "Submitting My First Goodie" or similar is perfect.
10. Copy and paste the Goodie Pull Request Template from [here](https://github.com/duckduckgo/zeroclickinfo-goodies/blob/master/pull_request_template_goodie.md) and paste in into the "Pull Request Description".
11. Answer the questions in the Pull Request Template (this helps the DDG Staff and Community understand your Pull Request better).
12. Go back to your Codio.com browser tab.
13. Open the "Terminal" tab and type `duckpan server` then press "**Enter**".
14. Click the DuckPAN Server button, and search for "duckduckhack GitHubUsername"
15. Take a screenshot of your awesome Instant Answer result, save it somewhere easily accessible.
16. Go back to your GitHub.com browser tab.
17. Drag-and-Drop your screenshot into the Pull Request Description (where it asks for a screenshot).
18. Click "Submit Pull Request"
19. Now sit back and relax. When a Community Leader or Staff member has a chance, they'll review your Goodie, give you any feedback (if necessary) and merge it in