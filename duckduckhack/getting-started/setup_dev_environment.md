# Setting Up Your Development Environment

In order to get moving with Instant Answer development, you'll need to setup your environment. At the very minimum, you will need a GitHub account and the DuckDuckHack developer tool, DuckPAN, to make and submit an Instant Answer. This guide will help you determine the best setup for you.

Before moving forward, you **must** know which Instant Answer type you will be using. After this section, the documentation will be specific to each Instant Answer type.

## Before you start...

We highly recommend that everyone uses Codio, a web-based IDE that simplifies the setup and development process greatly. If you prefer using a local text editor, that's alright, but using Codio is still beneficial because we already have the required software installed and ready to go. This page will show you how to set up Codio and then it's on to creating Instant Answers!

**Note:** You can also [develop and test locally](https://github.com/duckduckgo/p5-app-duckpan#installing-duckpan-locally) *if you're using Mac OS/Ubuntu*, or install a [pre-configured virtual machine](https://github.com/duckduckgo/p5-app-duckpan#vagrant-virtual-environment), but these options do require more time and effort. If you're a **Windows** user, you'll need to use Codio, or the virtual machine. Local development is not possible. Sorry.

## Sign up for a GitHub Account

*Already have a GitHub Account? Perfect, move on to [the next step](#sign-up-for-a-codio-account)!*

If you're new to programming, GitHub is a well known, popular tool that many individuals and companies use to save their code. Many open-source projects (such as DuckDuckHack) are hosted on GitHub and anyone with an account can contribute. GitHub is a great tool that you will likely be using long after this tutorial. To get started, let's sign up!

1. Go to https://github.com/join and enter the required information, then click "**Create an Account**"
2. Click "**Finish Signup**" to continue with a **Free** GitHub account.

**Congrats!** You now have a GitHub account.


## Sign up for a Codio Account

Next, you'll need to get an account for Codio:

*Already have a Codio Account? Perfect, move on to [the next step](#fork-the-duckduckhack-project-on-codio)!*

1. Go to https://codio.com and click "**Sign Up**", at the top right corner.
2. Click "**Sign Up via GitHub**".
3. Enter your GitHub login details and then click"**Sign In**".
4. Click "**Authorize Application**" to continue.
5. In the new screen, enter the required details and click "**Create Account**".

**Congrats!** You now have a Codio account. You'll notice that you didn't need to provide a password, that's because you've logged in to Codio using your GitHub account. As long as you can login to your GitHub account, you can also login to Codio. Now let's get started with setting up your Codio environment!


## Fork the DuckDuckHack Project on Codio

1. Go to https://codio.com/duckduckgo/duckduckhack and click "**Project**" at the top left corner.
2. In the drop-down, select the "**Fork**" option.

    ![Codio Fork](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckpan/assets/codio_fork.png)

3. In the pop-up window, select "**Clone both the Project and its Box**".

    ![Codio Fork Both](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckpan/assets/codio_fork_both.png)

4. Wait a minute while the project forks...
5. You should now see a new window with three panes. It should say "**DuckDuckHack**" at the top of the left pane.

**Congrats!** You've now successfully forked the DuckDuckHack environment. Now, let's grab the DuckDuckHack Goodie code (from GitHub.com) and start learning!


## Fork the correct DuckDuckHack repository on GitHub

In order to test out and create your own Instant Answer, you'll need the open-source code that DuckDuckGo hosts on GitHub.com. We're now going to "fork" that code, so you'll have your own personal copy which you can modify.

By now you should have [determined the Instant Answer type](https://duck.co/duckduckhack/determine_your_instant_answer_type) you're going to build.

1. Go to the Instant Answer repository homepage:
    - [Goodies](https://github.com/duckduckgo/zeroclickinfo-goodies)
    - [Spice](https://github.com/duckduckgo/zeroclickinfo-spice)
    - [Fathead](https://github.com/duckduckgo/zeroclickinfo-fathead)
    - [Longtail](https://github.com/duckduckgo/zeroclickinfo-longtail)
2. Do you see your username in the top right corner?
    - **Yes**? Perfect. Move on to the next step.
    - **No**? Click "**Sign In**", then enter your details and click "**Sign In**".
3. Click "**Fork**", near the top-right corner.
4. Wait while the repo forks...
5. You should see a page that looks nearly identical to the repo home page you were just on. The URL should be different though, it should look like **`https://github.com/yourGitHubUsername/zeroclickinfo-xxxxx`**. This is the URL for your personal copy of the DuckDuckHack code.
6. **Keep this URL handy, we'll be using it in a minute!**


## Clone your Repository onto your Codio Machine

Now we need to "clone" the code from GitHub to your Codio box so you can see it, modify it and run it!

1. Go to the [Codio projects page](https://codio.com/home/projects).
    - See a "**Sign In**" screen? Use the "**Sign in via GitHub**" method like you did before (see Step #2 [here](#sign-up-for-a-codio-account)).
2. Click the "**DuckDuckHack**" project.
3. You should now see the three-pane window we previously saw. Press **Ctrl+Alt+R** (Cmd+Alt+R on a Mac), this will improve the layout a bit. (You can also click *View->Layouts->Default* from the command bar at the top).
4. Press **Shift+Alt+T** to open a new Terminal. (You can also click *Tools->Terminal* from the command bar at the top). You should see the right side pane change into a black command prompt.
5. Type **`git clone <Your GitHub URL Here>.git`** into the Terminal, replacing `<Your GitHub URL Here>` accordingly. It should look something like this for a Goodie:

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
    [04:30 PM codio@buffalo-pixel workspace {master}]$
    ```

7. The file tree on the left side should update. There should be a new "**zeroclickinfo-xxxxx**" directory, where "**xxxxx**" is whichever Instant Answer type you chose: Goodie, Spice, Fathead, or Longtail.

**Congrats!** You've now cloned the DuckDuckHack code onto your Codio machine. You're now prepared to code you first Instant Answer!

## Give Us a Heads Up

We know you're eager to get started, and we're super excited to see your awesome Instant Answer creations! Before you start coding up a storm though, **[please send us an email](mailto:open@duckduckgo.com)** to let us know that you plan on submitting a new Instant Answer. This will prevent you from wasting time in case your Instant Answer doesn't get approved. Some reasons why your Instant Answer might not get approved include:

 - the Instant Answer already exists
 - the source isn't usable (e.g. paid API, low rate limit, no JSON support)
 - the idea needs more thought or planning

Here's an example email to help you out:

```text
To: open@duckduckgo.com
Subject: Instant Answer Approvals

I'd like to make an Instant Answer for <topic/subject>!
This is the data source: <link, description, Perl module, etc.>.
This is the related Duck.co idea: <url, if applicable>.
This is my Github username: <username>.

Thanks!

PS: DuckDuckGo is awesome!
```

We'll try and get back to you as soon as possible (ideally within 24hrs). We ask that you wait to hear back from us before moving ahead unless you're absolutely sure this Instant Answer is acceptable (i.e. a duck.co idea that has been approved by DDG staff).

## Start Coding!

At this point, you're ready to start learning about the Instant Answer type you'll be using.

- For **Goodies**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_overview.md)

- For **Spice**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_overview.md)

- For **Fathead**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/fathead/fathead_overview.md)

- For **Longtail**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/longtail/longtail_overview.md)