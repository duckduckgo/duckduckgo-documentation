# Test Files

Every plugin includes a test file in the `t` directory. These test files include sample queries and are run automatically before every release to ensure that all goodies are triggering properly. They are also very helpful while developing plugins as a tool to quickly test code iterations. Once you've written a test file, you can test it on it's own with `perl -Ilib t/TestName.t`, or together with all other tests in the repository using `prove -Ilib`.

Goodies and Spice use a similar test structure, but test different things. Here we'll see an examples of testing files, first for Goodies, then Spice: