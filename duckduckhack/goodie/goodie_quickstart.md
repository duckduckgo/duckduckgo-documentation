# My First Goodie Instant Answer!

This is a quick start tutorial designed to teach about Goodie instant answers. You'll be making and submitting your first Instant Answer to the DuckDuckHack project. In order to get moving quickly, we'll be using a web based IDE, [Codio](https://codio.com), along with a pre-configured DuckDuckHack environment.

This tutorial assumes zero knowledge and walks you through every step required. No guesswork needed!


## Before We Get Going...

Aside from a working internet connection and a computer, there are two important things you'll need to get started:

- a **free** Codio account
    + Codio provides a web-based code editor where you will be creating and testing new instant answers. We're using Codio because it works across all platforms (Windows, Linux, Mac) and comes preconfigured with the necessary software for Instant Answer development.
- a **free** GitHub account
    + GitHub provides a place for you to save your code on the internet.
    + When your Instant Answer is ready for us to review, you'll use GitHub to send us your code!


## Sign up for a GitHub Account

Already have a GitHub Account? Perfect, move on to [the next step](#setup_codio_environment)!

If you're new to programming, GitHub is a well known, popular tool that many individuals and companies use to save their code. Many open-source projects (such as DuckDuckHack) are hosted on GitHub and anyone with an account can contribute. GitHub is a great tool that'll you likely be using long after this tutorial so to get started, lets sign up!

1. Go to https://github.com/join and enter the reqiured information, then click "**Create an Account**"
2. On the next page, click "**Finish Signup**" to continue with a **Free**
GitHub account.

Congrats! You now have a GitHub account. Now let's get started with Codio!


## Sign up for a Codio Account

Now that you have a GitHub account let's sign up for a Codio account!

Already have a Codio Account? Perfect, move on to [the next step](#fork_the_duckduckhack_project_on_codio)!

1. Go to https://codio.com and click "Sign Up", at the top right corner.
2. Click "**Sign Up via GitHub**". You'll be redirected to a login screen at GitHub.com. Enter your GitHub login details and then click "**Sign In**".
3. Now you should see a screen asking you to authorize the Codio application. Click "**Authorize Application**" to continue.
4. You'll now be taken back to Codio and you should see a new screen asking you to confirm a few details for your new Codio account. Enter the required details into the form, then click "**Create Account**".

Congrats! You now have a Codio account. You'll notice that you didn't need to provide a password, that's because you've logged in to Codio using your GitHub account. So as long as you can login to your GitHub you can also login to Codio. Now let's get started with setting up your Codio environment!


## Fork the DuckDuckHack Project on Codio

1. Go to https://codio.com/duckduckgo/duckduckhack and click "**Project**" at the top left corner.
2. From the dropdown, select the **Fork** option.

![Codio Fork](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckpan/assets/codio_fork.png)
3. In the pop-up window, select the **3rd** option, "**Clone both the Project and its Box**".

![Codio Fork Both](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckpan/assets/codio_fork_both.png)
4. Wait a minute while the project forks...
5. After it's done, you should see a new window with three panes. It should say "DuckDuckHack" at the top of the left-pane

Congrats! You've now successfully forked the DuckDuckHack environment. Now, let's grab the DuckDuckHack Goodie code (from GitHub.com) and start learning!


## Fork the DuckDuckHack Goodie Repository on GitHub

In order to test out and create your own Goodie Instant Answer, you'll need the open-source code that DuckDuckGo hosts on GitHub.com. We're now going to "fork" (that's the GitHub term for "copy") that code, so you'll have your own personal copy which you can modify.

1. Go to https://github.com/duckduckgo/zeroclickinfo-goodie. This is the home page for the DuckDuckHack Goodie repository (also known as a "repo").
2. Do you see your username in the top right corner?
    - Yes. Perfect, you're already signed in! Move on to the next step.
    - No. Okay, click "**Sign In**" and enter your details in the pop-up window. Then click the green "**Sign In**" button.
2. Click the **Fork** button, near the top-right corner.
3. Wait while the repo "forks". Once it's done you should see a page that looks nearly idental to the Goodie repo home page. However, the URL should be different and **should have your GitHub username in it**. More specificially, it should look like "https://github.com/\<your user name\>/zeroclickinfo-goodie". This is the URL for your personal copy of the DuckDuckHack Goodie code!
4. **Keep this URL handy, we'll be using it in a minute!**


## Clone your Goodie Repository onto your Codio Machine

Now that you have your own copy of the code on GitHub, we need to copy the code onto your Codio box so we can see it, modify it and even run it!

1. Go to https://codio.com/home/projects. If you see a "**Sign In**" screen, use the "**Sign in via GitHub**" method like you did before (see Step #2 [here](#sign_up_for_a_codio_account)).
2. You should see a page titled "**Pojects**" and below that, a table row that says "**DuckDuckHack**". Click the "**DuckDuckHack**" table row to select that project.
3. You should now see the three-paned window we previously saw. Personally, I'm not a huge fan of this layout so **press Ctrl+Alt+R** (Cmd+Alt+R on a Mac) to change the layout (you can also click View->Layouts->Default from the command bar at the top).
4. Open up a command-line terminal by pressing **Shift+Alt+T** (you can also click Tools->Terminal from the command bar at the top). You should see the large, right side pane change into a black terminal.
5. We're now going to use that GitHub URL I asked you to remember. Type **`git clone <github_url>.git`** into the terminal, replacing `<github_url>` with the URL for your copy of the Goodie code. It should look something like this:
    ```
    [07:39 PM codio@buffalo-pixel workspace {master}]$ git clone https://github.com/moollaza/zeroclickinfo-goodies.git
    ```
6. Press "**Enter**". You should see the terminal print out some text that looks like this:
    ```
    [07:39 PM codio@buffalo-pixel workspace {master}]$ git clone https://github.com/moollaza/zeroclickinfo-goodies.git
    Cloning into 'zeroclickinfo-goodies'...
    remote: Counting objects: 18623, done.
    remote: Compressing objects: 100% (8083/8083), done.
    remote: Total 18623 (delta 8084), reused 18179 (delta 7868)
    Receiving objects: 100% (18623/18623), 5.50 MiB | 9.51 MiB/s, done.
    Resolving deltas: 100% (8084/8084), done.
    Checking connectivity... done.
    [07:39 PM codio@buffalo-pixel workspace {master}]$ git clone https://github.com/moollaza/zeroclickinfo-goodies.git
    ```
7. Now, move to that directory, by typing **`cd zeroclickinfo-goodies`** and press "**Enter**". The command-line prompt should change to show you that you're now in the **zeroclickinfo-goodies** folder:
    ```
    [07:39 PM codio@buffalo-pixel workspace {master}]$ cd zeroclickinfo-goodies
    [07:39 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$
    ```

Congrats! You've now cloned your fork of the Goodie repo onto your Codio machine. Now, let's code our first Goodie and run it!

------

*Curious to know what we just did?*

You just used a program called **Git**, to **clone** (copy) the Git repository (a special file containing all the code) located at "https://github.com/<your_username>/zeroclickinfo-goodies.git" onto your Codio machine. Git automatically creates a new folder based on the name of the repository it's cloning and copies the code into it. In our case, Git create a folder, "zeroclickinfo-goodies", and copied all the code into there. Then we used the program called "**cd**" (short for "change directory") to move into the folder we just created!


## Creating Your First Goodie

Now we're going to create our first Goodie! We'll be using the DuckPAN tool to generate some boilerplate code for us to make things easier.

<!-- Note: At this point you should be in the root of the **"zeroclickinfo-goodies"** repository, which is where we left off in the last section. -->

1. Type **`duckpan new`** and press "**Enter**". You should see the terminal change, prompting you to enter a name for your Instant Answer.
2. Type "**MyFirstGoodie::<your GitHub username>**", replacing "<your GitHub username>" with your actual GitHub username:
    ```
    [08:31 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ duckpan new
    Please enter a name for your Instant Answer: MyFirstGoodie::Moollaza
    ```
3. 



![Codio Server](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckpan/assets/codio_server.png)
5. You're all set!
![Codio Success](https://raw.githubusercontent.com/duckduckgo/duckduckgo-documentation/master/duckpan/assets/codio_success.png)

Try typing in queries like "define hello," and see if it works for you. You might be wondering why there are no search results in the page. It's because DuckPAN isn't configured to work with search results—it's only for testing instant answers.
