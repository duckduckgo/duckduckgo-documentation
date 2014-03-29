# Test Files
Good test files not only help you quickly test your code iterations; they also serve as sort of functional specification. This helps others quickly understand and verify the expected behavior of your code. This, in turn, improves the quality of the feedback you receive and accelerates the review process.

Every instant answer must include a test file in the `t` directory. These test files are run automatically before each release to ensure that all instant answers are triggering properly.

At a minimum, your tests should cover all of your primary and secondary example queries. If possible, you should also include examples of similar queries on which your code does **not** trigger.  If your answer depends on the user's location, please use the [Location API testing guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/testing_location_api.md) to help in developing your tests. If your answer depends on the time of day or year, please be sure that your tests will continue to pass no matter when they are run.

## Creating Test Files

Your test file should be named like the package which it tests.  For example, `DDG::Goodie::Fortune` has its tests in `t/Fortune.t`.

The Goodie and Spice repositories have libraries (`DDG::Test::Goodie` and `DDG::Test::Spice`, respectively) which make it easy to quickly develop tests.  Probably the most common way to get started on your test file is to copy the test file for a similar instant answer and edit it to suit your code.

## Running Test Files

Tests are run from the root of the repository using the `prove` command included in your Perl distribution. During development, you can quickly run a test file to verify your changes:

```perl
prove -Ilib t/TestName.t
```

To ensure that you have not inadvertently changed the behavior of other code, you should run all of the files in the repository's `t` directory before submitting your instant answer:

```perl
prove -Ilib t/
```

