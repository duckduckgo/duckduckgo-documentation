## Making a Pull Request

Now that you have completed the [developer checklist](https://dukgo.com/duckduckhack/developer_checklist) and added [Metadata](https://dukgo.com/duckduckhack/metadata) to your Instant Answer, you are ready to submit a pull request.

The root of each repository contains a `pull_request_template.md` file which includes the most common questions the team will have about your contribution:

- [Cheat Sheet Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-goodies/master/pull_request_template_cheat_sheet.md)
- [Goodie Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-goodies/master/pull_request_template_goodie.md)
- [Spice Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-spice/master/pull_request_template_spice.md)
- [Fathead Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-fathead/master/pull_request_template_fathead.md)
- [Longtail Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-longtail/master/pull_request_template_longtail.md)

The contents of this file should be copied and pasted directly into the [description area](https://github-images.s3.amazonaws.com/help/pull_requests/pullrequest-description.png) of the GitHub pull request form. The completed template will help the community better understand your pull request and expedite the review process.

### Committing Your Changes

The first step in submitting your changes is to commit your changes to your local repository. Here is how to commit your code in the Codio environment:

1. Log in to [Codio](https://codio.com) and visit your [dashboard](https://codio.com/home/projects). (In the menu, click Codio > Dashboard)

2. Click on the **DuckDuckHack project**, which you previously forked and cloned.

3. Next, open a terminal window if it's not already open. (In the menu, click Tools > Terminal).

4. Enter the root directory of your forked Instant Answer repository. For example, for Goodies, enter the following into your terminal:

    ```shell
    cd zeroclickinfo-goodies 
    ```

    Then press enter.

5. To add all new files to git, type **`git add .`**, then press enter.

    *This command tells the git repository to include and track changes to the files you've created. Even though the files were physically located in the repository, we need to explicitly tell git to track them.*
    
5. We are now ready to finally commit the changes. Type **`git commit -m "Description of your changes"`** and press **`Enter`**. Git should print some text confirming the changes that have been committed.

    ```
    [04:35 PM codio@buffalo-pixel zeroclickinfo-goodies {master}]$ git commit -m "Description of your changes"
    [master 6aeb841] Description of your changes
     2 files changed, 56 insertions(+)
     create mode 100644 ...
     create mode 100644 ...
    ```

6. Now we'll upload the changes to *our* remote repository on GitHub. Once this step is done, we'll be ready to create a pull request back to the main, original DuckDuckGo repository. 

    Type **`git push`** and press **`Enter`**. Enter your GitHub Username and password, press **`Enter`** after each. Git will print some text to the Terminal letting you know that your code has been pushed to GitHub.

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


### Submitting a Pull Request

1. Open a **new browser tab** and go to your remote repository. For example, for Goodies: **`https://github.com/githubusername/zeroclickinfo-goodies`**.

2. Click the "**Pull Request**" button (grey text, middle of the screen).

    For advanced users, make sure you are on the correct branch where your changes are located.

3. Review the changes and click "**Create Pull Request**".

4. Enter a title for your pull request, "**GitHubUsername's ________ Goodie**" or similar is perfect.

11. Copy the "Pull Request Template" for your type of Instant Answer here: paste it into the text box that says "**Leave a comment**".

    - [Goodie Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-goodies/master/pull_request_template_goodie.md)
    - [Spice Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-spice/master/pull_request_template_spice.md)
    - [Fathead Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-fathead/master/pull_request_template_fathead.md)
    - [Longtail Pull Request Template](https://raw.githubusercontent.com/duckduckgo/zeroclickinfo-longtail/master/pull_request_template_longtail.md)
    
12. Answer the questions in the Pull Request Template

13. Add a screenshot of your Instant Answer to your answers
	
	Go back to your Codio.com browser tab, and open the "Terminal" tab 
	
	Type `duckpan server`, then press enter.
	
	Click the DuckPAN Server button at the top of Codio, and type in a sample search query that will trigger your Instant Answer.
	
	Save a screenshot on your computer.

	Go back to your GitHub.com browser tab.

	Drag-and-Drop your screen shot into the textbox. The picture will be uploaded and a link will be generated.
	
14. Finally, click **"Create Pull Request"**!

Congratulations! You can now sit back and relax. A Community Leader or DDG staff member will review your Goodie in turn, give you any feedback (if necessary) and merge it in. 

Once it's merged, it will be deployed to the site and should be live within a few days. **We'll be sure to let you know once it's live!**

*For more information on how to create a pull request, GitHub provides excellent [instructions](https://help.github.com/articles/creating-a-pull-request).*

## Review Process

When you submit a pull request, a community leader will assign themselves to your pull request and work with you to get your Instant Answer live on DuckDuckGo. 

All comments and suggestions for your pull request should be discussed publicly in the pull request on Github, so that others can follow the progression. Of course, you can always contact anyone from the community or team if you have questions. 

In addition to the main [open@duckduckgo.com](mailto:open@duckduckgo.com) way to reach us, here are some community leaders who are available to help out:

<!-- /summary -->

- [@bradcater](https://github.com/bradcater)
- [@loganom](https://github.com/loganom)
- [@mattr555](https://github.com/mattr555)
- [@mintsoft](https://github.com/mintsoft)
- [@TomBebbington](https://github.com/TomBebbington)
- [@killerfish](https://github.com/killerfish)
- [@MrChrisW](https://github.com/mrchrisw)
- [@javathunderman](https://github.com/javathunderman)

Here's how the whole process looks, after you submit your pull request:

1. A community leader (an experienced member of the community) will work with you on your pull request.
   - The community leader will ping [@abeyang](https://github.com/abeyang) (or [@chrismorast](https://github.com/chrismorast)) for any design/interaction feedback.
   - The community leader will test and give feedback about your code.
   - You discuss and incorporate any applicable feedback.
2. When the community leader feels that the Instant Answer is ready to go live, they ping [@jagtalon](https://github.com/jagtalon) so that he can set it up on a testing server.
3. Final review by the internal team.
4. Your pull request gets merged in and goes live!

## Thank you!  

We're excited to have you in our community and we can't wait to see your Instant Answer on DuckDuckGo.com. Your contributions are helping our search engine get better every day. We owe you our deepest gratitude. 
