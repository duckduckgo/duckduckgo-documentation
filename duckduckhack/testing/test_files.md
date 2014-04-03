# Test Files
Good test files can help you quickly test code iterations. They also serve as a functional specification for your code. This specification helps everyone quickly understand and verify the expected behavior of the tested code, improving the quality of the feedback you receive and accelerating the review process.

Every instant answer must include a test file in the `t` directory. The test files are run automatically before each release to ensure that all instant answers are functioning properly.  Properly functioning instant answers:

- ignore any unsuitable queries,
- trigger on the expected queries, and
- provide appropriate answers for the queries handled.

At a minimum, your tests should cover all of your primary and secondary example queries. If possible, you should also include examples of similar queries on which your code does **not** trigger.  If your answer depends on the user's location, please review the [Location API testing guide](https://github.com/duckduckgo/duckduckgo-documentation/blob/master/duckduckhack/testing/testing_location_api.md) for help in developing your tests. If your answer depends on the time of day or year, please be sure that your tests will continue to pass no matter when they are run.

## Creating Test Files

If you used `duckpan new` to start your project, a simple test file was automatically created for you. Otherwise, copying the test file from a similar instant answer is an easy way to get started. Either way, you are a few well-placed edits from a test file suitable for your instant answer.

Your test file should be named like the package which it tests.  For example, `DDG::Goodie::Fortune` has its tests in `t/Fortune.t`.  The Goodie and Spice repositories have libraries (`DDG::Test::Goodie` and `DDG::Test::Spice`, respectively) which make it easy to quickly develop tests.

## Running Test Files

Tests are run from the root of the repository using the `prove` command included in your Perl distribution. During development, you can quickly run a single test file to verify your changes:

```shell
prove -Ilib t/TestName.t
```

Or all of the tests in the repository's `t` directory:

```shell
prove -Ilib t/
```

To ensure that you have not inadvertently changed the behavior of other code, you should run the full test suite before submitting your instant answer. This is easily accomplished via `duckpan`:

```shell
duckpan test
```
