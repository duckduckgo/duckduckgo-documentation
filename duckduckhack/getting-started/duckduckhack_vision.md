# DuckDuckHack Vision

###The goal of DuckDuckHack is to provide users with relevant and useful instant answers.

In order to make sure these instant answers are worthy of being displayed, there are a few conditions that each and every instant answer must meet:

1. **Better Than Links**.  
    Since instant answers are above the traditional links, they should be unambiguously better than them. For example, the [Yummly integration](https://ddg.gg/?q=garlic+steak+recipe) shows recipes and pictures of the food, which is better than sorting through the organic links below it.
    ![better than links](https://s3.amazonaws.com/ddg-assets/docs/better_than_links.png)

2. **No False Positives**.  
    A false positive is an irrelevant instant answer. Only return an instant answer when you know it is good, and otherwise return nothing. For example, the [Quixey instant answer](http://ddg.gg/?q=flight+search+app) shouldn't show an answer for a query like ["how to build a simple ipad app"](https://duckduckgo.com/?q=how+to+build+a+simple+ipad+app).

3. **Minimal Vertical Space**.  
     Only include the most important information and then offer the user to click through for more if needed.  
    ![minimize space](https://s3.amazonaws.com/ddg-assets/docs/minimize_space.png)

4. **Consistent Design**.  
    In order to display instant answers, we have four different instant answer types: **Goodie**, **Spice**, **Fathead** and **Longtail**. Although each instant answer type serves a different purpose, the instant answers they provide should look and feel similar. When in doubt, copy what already exists or ask us! We already have a few cool designs, like [this one](https://duckduckgo.com/?q=movies) and [this one](https://duckduckgo.com/?q=garlic+steak+recipe).

These four points encompass the basic idea behind our instant answers, but in order to thoroughly describe how instant answers should be designed, we've also written comprehensive [**DuckDuckHack Instant Answer Design Guidelines**](https://github.com/duckduckgo/DuckDuckGo-Documentation/blob/master/DuckDuckHack/Styleguide/design_styleguide.md). You should keep these guidelines handy and turn to them often while you create your instant answer to ensure your instant answer design is appropriate and meets our expectations.