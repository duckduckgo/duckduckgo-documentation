# Preparing to Submit

Any contribution to DuckDuckHack is a significant and impressive undertaking. Your contribution has the potential to appear on hundreds of devices, across millions of searches.

Our mission as a community is to cover every topic with an Instant Answer. *Every topic.* That involves an enormous number of people, contributors, and submissions. 

To support as many contributors as possible, we've evolved a review process that is stringent and efficient. To undergo review, contributions must first satisfy a non-negotiable set of prerequisites. **The fastest way to get your contribution approved is to follow these requirements carefully.**

Don't worry if that sounds daunting - we're always going to be as transparent as possible about any requirements. Also, the community is chock-full of leaders and contributors happy to pair up and help you prepare for review. Overall, this leads to a productive, interconnected DuckDuckHack community.

## Pull Request Checklist

The culmination of your contribution comes in the form of a pull request to the Github repository for your Instant Answer type.

Before proceeding, make sure you've done the following steps.

- [Contacted us](mailto:open@duckduckgo.com) to let us know what you're working on

	By involving us, we can provide guidance and potentially save you a lot of time and effort. Email us at [open@duckduckgo.com](mailto:open@duckduckgo.com) with what idea you're working on and how you're thinking of going about it.

- Determined your Instant Answer type (we will have helped you determine this, in addition to this [helpful guide](https://duck.co/duckduckhack/determine_your_instant_answer_type))	
- Forked the [correct repository](https://duck.co/duckduckhack/setup_dev_environment) on Github
- Written and committed the code for your Instant Answer
- Make sure you comment your code well so that it's easier for other people to maintain.
- [Manually tested](https://duck.co/duckduckhack/testing_triggers) your Instant Answer
- Written a comprehensive automatic [test file](https://duck.co/duckduckhack/test_files) for your Instant Answer
- Manually verified that everything works.
- Make sure your [tab name](https://duck.co/duckduckhack/display_reference#codenamecode-emstringem-required) is well-chosen and consistent with the guidelines
- If you wrote custom CSS, did you namespace the CSS? Every Instant Answer should be contained in a `<div>` with a unique id. This id should be used to target your styles and avoid overwriting any global styles.
- Confirmed the Instant Answer adheres to the [code style guide](https://duck.co/duckduckhack/code_styleguide)
- Added yourself to the attribution (if updating an existing Instant Answer).
- Can this Instant Answer return unsafe content (bad words, etc.)
    - Did you set `is_unsafe` to true?
- Can this Instant Answer return an HTML response?
    - Have you guaranteed that the response does not contain unsanitized user-supplied strings (e.g., the query string) which could lead to [cross-site scripting attacks](https://duckduckgo.com/Cross-site_scripting?ia=about)?

## Proceed to Adding Metadata

Checked everything off the list? Congratulations - you are now ready to [add metadata](https://duck.co/duckduckhack/metadata) to your Instant Answer which will help us to understand it a little better.