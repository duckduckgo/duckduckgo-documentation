# Setup

*First and foremost, we'd like you to know that we're here to help. If you have any questions or frustration during this process, email us at **open@duckduckgo.com** and we'll help you out!*

## Before you start...

For your setup, we highly recommend using Codio, a web IDE that simplifies the development process greatly. This page will show you how to set up Codio and then it's on to creating instant answers!

*Note:* You can also [TO BE ADDED] develop and test locally or via a virtual machine [/link], but these options do require more configuration and are currently maintained by volunteer efforts.

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

1. Go to the DuckDuckHack repository for the type of instant answer youd' like to build:
    - [Goodie](https://github.com/duckduckgo/zeroclickinfo-goodies)
      *Instant Answers that are pure code (e.g. calculations or PRINT functions)*
    - [Spice](https://github.com/duckduckgo/zeroclickinfo-spice)
      *Instant Answers with a real-time data source (e.g. JSON or XML API)*
    - [Fathead](https://github.com/duckduckgo/zeroclickinfo-fathead)
      *Instant Answers with a title-->object/article relation (e.g. MediaWikis)* 
    - [Longtail](https://github.com/duckduckgo/zeroclickinfo-longtail)
      *Instant Answers with consumable data that require full-text search (e.g. lyrics)*
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

7. The file tree on the left side should update, there should be a new "**zeroclickinfo-xxxxx**" directory. Where "xxxxx" is whichever Instant Answer type you chose: Goodie, Spice, Fathead, or Longtail.

**Congrats!** You've now cloned the DuckDuckHack code onto your Codio machine. Now, let's code our first Instant Answer! 
