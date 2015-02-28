# DuckDuckHack Rewrite Proposal

This is a short, quick proposal about how I would restructure DuckDuckHack’s documentation to **raise the number of open source contributors of all levels**.

I’ve outlined changes to the introductory sections as well as to Goodie. If you guys like the approach, we’ll proceed to the rest of the documentation.

I believe in these principles:
- **Always begin with the big picture.** Show context, similarities, and contrast to what the contributor has already understood. 
- **Inspire.** Whether someone gets through the documentation or not is as much about their desire to make it happen as accessibility. Every section should do its part in getting contributors excited and their imaginations revved up. This is present on the DDH landing page, but sorely missing from the docs.
- **Be explicit and clear.** Every section should neither make any assumptions nor skip any steps. All instructions should be broken down into painfully simple steps, giving contributors a feeling of progress and mastery. 

## Getting Started

### Welcome

This is the first section people reach after DuckDuckHack.com. That landing page is full of inspiration and **this page should continue the excitement.** 
- Reiterate the big picture of Instant Answers. Why is it important? What does it mean for the world? Why is it a great introduction to open source? Why DDG?
- Show several more exciting examples beyond the flight tracker app. Briefly talk about where each idea came from. Highlight person behind each example, their background, and their picture. Talk about the high level mechanic that allows the particular instant answer to operate, and hint at what kind of Instant Answer type is involved. 
- Challenge and inspire the contributor - what ideas do you have? What has always frustrated you? What do you think you can add value that most people can’t? What are you really smart about? Could you make an Instant Answer as a gift or gesture to someone that provides value to many others as well? What means a lot to you? 
- Invoke the vision of DDG and how we can have an instant answer for every search term and what that would do for the world.
	- Why DDG is a great platform to make the world a better place. And why Instant Answers is one of the best ways to make that happen; any metrics that prove the significance of Instant Answers and why it’s getting so much attention and driving DDG’s growth.
	- Why it all comes down to YOU as a contributor. All of these came from a community of developers. This isn't some closed app ecosystem; this is an open source community that rides on DDG as a platform for distribution.

### Overview of Contributing Your Instant Answer

This short section would focus on the **high level process** of creating an Instant Answer. It may feel redundant if you already know this, but to someone reading for the first time, we should err on the side of them feeling smart rather than lost.

1. Come up with an idea
2. Determine what kind of Instant Answer will help you make it a reality
3. Ping us for approval (put the sample template email here) - we answer super fast. 
4. Set up your development environment (don’t worry, we use great tools to make this fast and easy)
5. Write your Instant Answer and, most importantly, its tests.
6. Notify us that you’re done and that we can approve your contribution to the live DuckDuckGo search engine. (We’ll explain how this works, it’s a very efficient process) 
7. Go to bed at night knowing that your contribution being used by millions

It’s a simple section but transparency and being explicit goes a long way for the uninitiated.
Cartoon illustrations could really enhance these steps. Or pictures of actual DDG contributors and staff posing dramatically acting out each step. (Anything to humanize and show there are real people in this community to someone who hasn’t yet experienced the open source world or the DDG community).

### Brainstorm Your Instant Answer

This is a short section that gives people ideas on what kind of instant answers they might be passionate about.

Having a section like this may seem unrelated, but our overall goal here is to raise the number of contributors. That comes from **inherent motivation and personal excitement to create**. 

If we dedicate time to the inspiration part and don’t just dive right into the technical details, DDH will see a much higher number of contributors.

I’d encourage the reader to reflect on what they uniquely bring to the community:

- Think of the common searches you personally make. What has always frustrated you? What do you wish “just worked?”
- What do you know a lot about? What are you passionate about? What feature of DDG might help you pursue that passion? For example, as a surfer, would it be useful to have swell ratings directly from Surfline.com? As a triathlete would it be useful to have a bla-bla-bla calculator? (I’m not a triathlete.)
- What is something you really care about? Could you make an Instant Answer that might make certain people’s lives better with this? For example, could you help people counting calories quickly look up a food type and a serving? (There was braille idea example on the listserve today.)

### Determine Your Instant Answer Type

The current flow diagram is a step in the right direction but it is very dense in information. It’s a good summary for someone who already understands.

I would focus on one IA type at a time and explain, in almost story form, what each one is. Right now it’s very tech-oriented differences, but those can easily be rephrased as benefits-oriented.

I would start with an example: Ernesto wants to create an instant answer that helps his grandfather know the side effects of various medications, when he types “side effects” trigger words in the search bar.

Then I would describe each kind of IA and how close that might let Ernesto get to his goal - and why. Some might fall short, but allow him to do something simpler. Others might help him go above and beyond his original idea. I would also list the tradeoffs to capability - why would Ernesto not choose one over another?

Then I would display an **IA flow diagram**, but with a few changes from the current one:

- I currently do not understand the difference between Longtail and Fathead, and would assume that if anything can explain it to me, it should be this diagram.
- I would phrase it in subtly clearer terms
	- “To provide searchers with a useful answer, does your idea need to be connected to…” 
	- “…does your idea require outside data…” 
	- “…can your idea simply use a pre-generated table of…” 
	- “…can your idea be accomplished with a simple perl script…” 
- A flow diagram might be overkill. A **table or a tiered chart might be a clearer way to show this.** For example, a tiered chart might emphasize that the end result for the user looks similar, or that HTML templates can be used in all of them. 
	- Or both. Cannot be too clear for people reading this for the first time. Most people do not have search engine experience so a lot of concepts are new.

And of course, end with the recommendation to contact the community if unsure. I’d even add reassurance that response is very fast and they won’t be left hanging. The community is very welcoming to newcomers and loves helping refine new ideas in the works.

### Get the Green Light for Your Idea

I’d dedicate a short, **standalone section** to explaining how to apply for approval, what happens, who is involved, and what the criteria are. 

What are the main criteria for approval to keep in mind?

What happens in reality? 
- Do most proposals get immediately approved? 
- Do most get refined or channeled? 
- How often is an idea outright rejected and why would that be?

I’d include examples of **real, past ideas** that benefited a ton from the pre-approval process before a line of code was written. 
- Did anyone get stopped from creating a duplicate? 
- Did anyone end up enhancing an existing IA and adding more test cases? 
- Did anyone end up realizing something they didn’t know or improving the idea?

With some personal stories this make this step much more concrete and inviting. It also reinforces social proof for the process.

### Setting Up Your Development Environment

This section has the potential to be really confusing - even thought it’s sequential, it’s hard to grasp conceptually what is going on and what the environment is composed of. 

There are two big parts here: the **box** and the **repository**.
1. I’d first describe the box and explain why Codio and what’s amazing about it. Why is it necessary? What does it represent? What is DuckPAN? How is it different but related to Codio? 
2. I’d then explain that there is one Instant Answers Git repository, and you will be contributing to it and expanding it. 
	- Of course, you can’t just directly work on it, so here is the workflow to let you test your work - and us inspect it and help you - without it being part of the actual production code till it’s ready.
	- As a result we are going to fork the repository to your Github account. But that’s still on Github, not on Codio. So now it needs to be cloned to Codio.
	- When you make a change to your code, you’ll **commit** in your Codio environment, and **push** it to your corresponding github fork. From there, that joins the main repo through a **pull request.**

A diagram here of this system would be an amazing asset. The items in the diagram would be: 
- Github cloud containing the DDG account and the contributor account (plus main repo and forked repo)
- A codio cloud containing the DDG box (dotted line) and the contributor box (solid). Plus cloned repo from Github forked repo.
- We’d have to draft it to see if this helps rather than hurts but I believe it would really help.

After the big picture is explained, the **setup steps** are a lot easier to follow.
- That said, I’d still add an extra sentence of context explaining how each step connects to the big picture we explained earlier.
- I would also include screenshots of output or particular actions with cursors - the more visual, the more the text can be broken up, the better.
- If possible to do further nested subsections, I would break up the steps into different sections so that it’s easier to follow and feel accomplished.

I would minimize the “get our approval” block of text to just one line. It’s what industry professionals dub a “boner killer” and I’d minimize it to just a short line reminding not to proceed without approval. 
> “We're so close to the action! We hope you already got our approval - it would be a shame if you worked on something we couldn't launch to our millions of DDG searchers.”

## Goodie
### Overview

This section is good to keep short like now. I would make it to be more inspiring and give more context.
- Goodies are the simplest form and easiest contribution to make to the search engine.
- That said, they are powerful. Here are three examples of some of our coolest Goodies we’re proud of our community for creating. *Screenshots inline. Not just links.*
- Goodies are simple because they don’t do X, and are contained to Y. Give examples of ideas that are perfect for Goodies, and those that are not, and the technical reasons why.

I would do a parallel section like this for every Instant Answer type. Spice, for example, dives head-first into the technical definitions without addressing the big picture first and would benefit dramatically from a better overview section. I found myself re-reading the initial paragraphs over and over without getting any closer to understanding the big picture.

### Anatomy of a Goodie

Presenting the big picture of adding a Goodie would make everything else easier to process.
- Dissect an existing Goodie; show its end result first as a screenshot
- To achieve this, what is the flow diagram, from search term to resulting Instant Answer. How does it fit into the rest of DDG events? Lightly introduce the terms triggers and handle functions. Explain what about this flow is unique to a Goodie; what things are *not* happening?
- How does this manifest itself as actual files and code additions in the repository? What does each file contain? Where in the filesystem? What would a final pull request look like? (Linking to a real past pull request for that example would be great.)
- Within the pm file, what are triggers? What are handle functions? What are tests? High level.
- Reiterate the creation process end-to-end: to create a Goodie it’s simply a matter of adding this code, committing it on the Codio clone, pushing from Codio to the github fork, and then making a pull request.

I would then explain the two options that follow and what the difference is, and their relation:

I would then frame the following sections as “choose your own adventure.” You don’t have to do both - either path will get you to creating a full Goodie.
- You can complete one and ignore the other.
- You can do one and then additionally do the other. The first is excellent way to ease into for the second. 

### Option 1: Beginners’ Tutorial

[At the start I would efficiently reiterate the relation of the Beginners’ Tutorial to the In-Depth Walkthrough, similar to the above. The first is instant gratification and get up to speed; the second will acquaint you with the full power of a Goodie Instant Answer]

Instead of one long page (which can be fatiguing) I would break this tutorial up into a nested format: **multiple large steps, each with its own subsection**. That would give contributors a greater feeling of accomplishment; it feels great to reach the end of a page. Also easier to keep one’s place when switching tabs.

The steps themselves are fine - I would clean them up a tad and make them more readable:
- Break them into smaller steps whenever possible
- Include [even more] action screenshots, however tiny, when possible - like clicking on Codio buttons and menus. There’s a lot of new things - concepts, systems, terms, and interfaces - so being explicit can only help. Images also help break up the text and make it more readable.
- When shortcuts are taken, explain that they are shortcuts and what is happening. For example, the Cmd+O shortcut saved time but I understood nothing about the file structure as a result. I felt that magic was going on thus less empowered.
- Include sentences of context and relationships that reiterate what was said in the anatomy section.

The end of this should encourage beginners that they are now very qualified to complete the In-Depth Walkthrough and that it will empower them to do much more with their ideas. Explain that if they got this far they are going to definitely understand and appreciate the full power of what can be done with a Goodie.

### Option 2: In-Depth Walkthrough

[At the start I would efficiently reiterate the relation of the Beginners’ Tutorial to the In-Depth Walkthrough, similar to the above.]

The content here is presumably fine, but I would change the presentation and structure.
- At the high level of structure I would give this parallel structure to the Beginners’ Tutorial. (Right now it’s awkward because the sub-steps of the Basic Tutorial are all on a flat hierarchy with the Quick Start.) By having the **structure accurately reflect the relationship** between the two paths, the documentation will be inherently clearer.
- I would begin each section with clear context of its significance *before* diving in. For example: testing. Why is this important? Why is this *as* important as the code itself? What is the relationship between interactive testing and test pages? 

*Note: when updating testing triggers, remember to fix the shell output of **duckpan query** to reflect [this comment](https://github.com/duckduckgo/duckduckgo-documentation/pull/208) by Zaahir.*

### FAQ

Instead of anchor linking to a huge docs-wide FAQ, I would create a specific FAQ that sits right in the Goodies section. There is no reason not to break out pieces of the large FAQ out across the docs when possible.

### Confession: I Haven’t Yet Built a Goodie

Making a Goodie is my next step.

I’m sure that I will have lots of ideas for presenting the detailed steps of the two tutorials (tests, triggers, handle functions, helpers). I would probably catch a few discrepancies I could fix by actually digging into the code.

I decided to send this proposal out sooner rather than later; you probably by now extrapolate the approach I would apply to individual sections when I reach that point.



# Roadmap

Everything until now was an outline of *what* I wanted to do. This is the roadmap for how I would go about it.

## Start from Scratch

The current docs require both a structural and content overhaul. Because changes are happening on both of these fronts, incremental pull requests would be inefficient. I would prefer to collaborate over a separate repository where I essentially do a rewrite.

Technically, this could still be a fork of the *duckduckgo-documentation* repo. However, the final pull request would appear dramatic (but not actually so, since we collaborated all along the way just without making pull requests along the way). 

## Small Chunks

Rewrites always sound like great ideas but are never as ideal as they sound. 

The key to doing them right is to break down the rewrites into small chunks so the DDH docs aren’t all different overnight.

**I would first focus on 100% improving the Goodie section, end to end.** I would focus on Goodie alone, and not touch the rest of the sections. 

I’ll first spend project time digging in as a contributor and coding my own Goodie. Then I’d write the docs in the way I think they should be done. We’d get feedback on that, see that no one got hurt, and proceed.

From there, I’d repeat this code-then-rewrite approach for one Instant Answer section at a time.

Feedback!

-Tal