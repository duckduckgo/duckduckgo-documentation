Please use this template as a starting point for any CONTRIBTUTING.md's. Make sure to replace "*\<repo\_name\>*" with the correct repository name.

------

# Contributing to *\<repo\_name\>*

At DuckDuckGo, we truly appreciate our community members taking the time to contribute to our open-source repositores. In an effort to ensure contributions are easy for you to make and for us to manage, we have written some guidelines that we ask our contributors to follow so that we can handle pull requests in a timely manner with as little friction as possible.

## Getting Started

* Make sure you have a [GitHub account](https://github.com/signup/free)

If submitting a **bug/suggestion**:
* Check if a GitHub issue already exists for the given bug/suggestion
    * If one doesn't exist, create a GitHub issue in the *\<repo\_name\>* repository
        * Clearly describe the bug/improvemnt, including steps to reproduce when it is a bug.
    * If one already exists, please add any aditional comments you have regarding the matter

If submitting a **pull request** (bugfix/addition):
* Fork the *\<repo\_name\>* repository on GitHub

## Making Changes

* Before making and changes, refer to the *\<repo\_name\>* repository's StyleGuide to assure your changes are made in the correct fashion
* Make sure your commits are of a reasonable size. They shouldn't be too big (or too small)
* Make sure your commit messages effectively explain what changes have been made:

    ```
    CONTRIBUTING.md - Added the example commit message because it was missing
    ```

* Make sure you have added the necessary tests for your changes.
* Run `dzil test` to assure nothing else was accidentally broken (when needed).

## Submitting Changes

* Push your changes to your fork of the repository.
* Submit a pull request to the *\<repo\_name\>* repository.
    * Make sure to use the *\<repo\_name\>* repository's Pull Request template