## Test Files
Good test files can help you quickly test code iterations. They also serve as a functional specification for your code. This specification helps everyone quickly understand and verify the expected behavior of the tested code, improving the quality of the feedback you receive and accelerating the review process.

<!-- /summary -->

Every Instant Answer must include a test file in the `t` directory. The test files are run automatically before each release to ensure that all Instant Answers are functioning properly. Properly functioning Instant Answers:

- ignore any unsuitable queries,
- trigger on the expected queries, and
- provide appropriate answers for the queries handled.

At a minimum, your tests should cover all of your primary and secondary example queries. If possible, you should also include examples of similar queries on which your code does **not** trigger. If your answer depends on the user's location, please review the [Location API testing guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/testing_location_api.md) for help in developing your tests. If your answer depends on the time of day or year, please be sure that your tests will continue to pass no matter when they are run.

## Creating Test Files

If you used `duckpan new` to start your project, a simple test file was automatically created for you. Otherwise, copying the test file from a similar Instant Answer is an easy way to get started. Either way, you are only a few well-placed edits away from a test file suitable for your Instant Answer.

Your test file should have **the same name** as the package it is testing. For example, the code in `lib/DDG/Goodie/Fortune.pm` is tested by `t/Fortune.t`.

The [standard `duckpan` installation](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/installing_duckpan.md) includes Goodie and Spice testing libraries (`DDG::Test::Goodie` and `DDG::Test::Spice`, respectively.) These libraries make it quick and easy to develop tests for your Instant Answer.

## Running Test Files

Tests are run from the root of the repository using the `prove` command included in your Perl distribution. During development, you can quickly run a single test file to verify your changes:

```shell
prove -Ilib t/TestName.t
```

<!-- /summary -->

Or all of the tests in the repository's `t` directory:

```shell
prove -Ilib t/
```

To ensure that you have not inadvertently changed the behavior of other code, you should run the full test suite before submitting your Instant Answer. This is easily accomplished via `duckpan`:

```shell
duckpan test
```
