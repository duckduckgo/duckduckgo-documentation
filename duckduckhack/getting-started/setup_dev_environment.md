# Setting Up Your Development Environment

To develop an Instant Answer, you need a GitHub account and the DuckDuckHack developer tool, DuckPAN. We also recommend using the Codio development environment. We'll go through the steps to get your development environment set up below, but **before you start**:
 - Have you been in touch about your Instant Answer idea and heard back about it?
  - *If not, email [open@duckduckgo.com](mailto:open@duckduckgo.com) or post in the [forum](https://duck.co/ideas) before you continue.*
 - Have you figured out what type of Instant Answer you're making?
  - *If not, use the [flowchart](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/getting-started/determine_your_instant_answer_type.md) to do that before you continue.*

Once you've had feedback confirming your new Instant Answer is good to go - and you know which type you're creating (**Goodie**, **Spice**, **Fathead** or **Longtail**), read on to get yourself set-up for developing it!

## Development Options

We strongly recommend that you use Codio, a web-based IDE that greatly simplifies the set-up and development process. If you prefer using a local text editor, that's cool, but it's still worth using Codio as the software you'll need is already installed and ready to go. 

You can [develop and test locally](https://github.com/duckduckgo/p5-app-duckpan#installing-duckpan-locally) ***if you're using Mac OS/Ubuntu***, or install a [pre-configured virtual machine](https://github.com/duckduckgo/p5-app-duckpan#vagrant-virtual-environment), but these options do require more time and effort. If you're a ***Windows*** user, you'll need to use Codio, or the virtual machine - local development is unfortunately not possible.

## 1. Sign up for GitHub

*Already have a GitHub account? Perfect, move on to [the next step](#2-sign-up-for-codio)!*

GitHub is a hugely popular platform for collaborative software projects. Many individuals and companies store their code in public GitHub repositories, particularly for open source projects. This allows anyone to potentially make a contribution to these projects - and lets you see how functionality has been implemented, making it a great learning resource.

To sign up for Github: 

 - Go to https://github.com/join - enter a username, email and password, then click **Create an account**.
 - Select a **Free** account and click **Finish Signup**.

You're now on GitHub!

Your GitHub account will allow you to create your Instant Answer by cloning the existing code, making your additions on your copy, then making a request to have your changes merged into the main repository - after which they'll go live on DuckDuckGo! Each type of Instant Answer has its own repository, as you'll see below.

## 2. Sign up for Codio

*Already have a Codio Account? Perfect, move on to [the next step](#3-fork-the-duckduckhack-project-on-codio)!*

To sign up for Codio:

 - Go to https://codio.com and click **Sign Up**, at the top right corner.
 - Click **Sign Up via GitHub**.
 - Enter your GitHub login details, then click **Sign In**.
 - Click **Authorize Application** to continue.
 - In the new screen, enter the required details and click **Create Account**.

You're now on Codio!

*You didn't need to provide a password because you've logged into Codio using your GitHub account - one less password to remember!*

Your Codio account will allow you to work on your cloned copy of the GitHub repo in an environment that's set-up for developing Instant Answers, with development and testing utilities all provided in the browser. You'll be able to write your code, see it running and test it all within the same environment.

## 3. Fork the DuckDuckHack Project on Codio

Now you need the DuckDuckHack project added to your Codio account - this provides the tools you'll need to develop any of the Instant Answer types.

### Step 1

Go to https://codio.com/duckduckgo/duckduckhack - select the **Project** menu and choose **Fork**:

![Codio Fork](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fduck_fork.png&f=1)

In the pop-up window, select **Box & Project**, then click **Continue**:

![Codio Fork Both](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fbox_project.png&f=1)
    
![Codio Fork Both](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fforked.png&f=1)

Wait a minute while the project forks...

You should now see **DuckDuckHack** at the top of the left pane in the window:

![Codio Fork Both](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fddh_open.png&f=1)

You've now successfully forked the DuckDuckHack environment and are ready to clone the GitHub repo for your Instant Answer type - then you can get developing!

## 4. Fork the DuckDuckHack GitHub repository for your Instant Answer type

To create and test your own Instant Answer you'll need the code that DuckDuckGo hosts on GitHub. We have a repo for each Instant Answer type - next you'll "fork" that code, creating your own personal copy to work on. When you're done you'll open a "Pull Request", asking for your new code to be merged into the main repo. *Normally this will involve a bit of back and forth between yourself and others in the DuckDuckGo community, as well as staff - we're a friendly crowd and will be excited to help you get your Instant Answer ready for merging!*

You should have already [determined the Instant Answer type](https://duck.co/duckduckhack/determine_your_instant_answer_type) you're going to build.

### Step 1

Go to the Instant Answer repo for the correct type:
 - [Goodies](https://github.com/duckduckgo/zeroclickinfo-goodies)
 - [Spice](https://github.com/duckduckgo/zeroclickinfo-spice)
 - [Fathead](https://github.com/duckduckgo/zeroclickinfo-fathead)
 - [Longtail](https://github.com/duckduckgo/zeroclickinfo-longtail)

### Step 2

Do you see your username in the top right corner?
 - Yes? Perfect. Move on to the next step.
 - No? **Sign In** to GitHub to continue.

### Step 3

On the repo homepage, click **Fork**, near the top-right corner.

Wait while the repo forks...

You should see a page that looks nearly identical to the repo home page you were just on. The URL should be different though, it should have your username in it (**`https://github.com/yourGitHubUsername/zeroclickinfo-xxxxx`**). This is the URL for your personal copy of the DuckDuckHack code. You can make changes on your forked copy without worrying about making mistakes or messing anything up so relax and have fun with it!

**Keep the URL for your forked repo handy (or just keep it open in a browser tab), you'll be using it in a minute!**

## 5. Clone your Forked Repository onto your Codio Machine

Now you need to "clone" the code from your GitHub fork to your Codio box so that you can work on it and test it out.

### Step 1

Go to the [Codio projects page](https://codio.com/home/projects).
 - See a **Sign In** pop-up? Use the **Sign in via GitHub** method like you did before.

Select the **DuckDuckHack** project:

![Codio Fork Both](https://images.duckduckgo.com/iu/?u=https%3A%2F%2Fraw.githubusercontent.com%2Fduckduckgo%2Fduckduckgo-documentation%2Fmaster%2Fduckduckhack%2Fassets%2Fproject_home.png&f=1)

### Step 2

You should now see the DuckDuckHack project as you did earlier. You can alter the layout using **Ctrl+Alt+R** (*Cmd+Alt+R on a Mac*) or the **View &gt; Layouts &gt; Default** menu options. *The pane on the left allows you to explore the project structure - in the pane on the right, you'll write your code and commands into the files and terminals you open.*

### Step 3

Press **Shift+Alt+T** or choose **Tools &gt; Terminal** to open a new Terminal. You should see the right side pane change into a black command prompt. 

Type **`git clone <Your-GitHub-URL-Here>.git`** into the Terminal, inserting the URL for your forked GitHub repo. It should look something like this for a Goodie:

    ```
    [04:30 PM codio@buffalo-pixel workspace {master}]$ git clone https://github.com/githubusername/zeroclickinfo-goodies.git
    ```

Press **Enter**. You should see the Terminal print out some text that looks like this:

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

The file tree on the left side should update to include a folder for the copied repo. There should be a new **zeroclickinfo-goodie**, **zeroclickinfo-spice**, **zeroclickinfo-fathead** or **zeroclickinfo-longtail** directory.

You've now cloned the DuckDuckHack code for an Instant Answer onto your Codio machine and are ready to get coding!

## Start Coding!

You've now created your own copy of the Instant Answer repo you want to add to, cloned it into your Codio account and set-up the DuckDuckHack development tools. You're now ready to start learning about the type of Instant Answer you're creating:

- For **Goodies**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/goodie/goodie_overview.md)

- For **Spice**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/spice/spice_overview.md)

- For **Fathead**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/fathead/fathead_overview.md)

- For **Longtail**, [start here](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/longtail/longtail_overview.md)

It's also a great idea to explore the code for existing Instant Answers on GitHub, before you start and also while you're coding. If you come up against a task you're unsure how to approach, you will likely find that another Instant Answer already does something similar.
