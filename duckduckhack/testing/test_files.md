# Test Files

Every instant answer includes a test file in the `t` directory. These test files include sample queries and are run automatically before every release to ensure that all instant answers are triggering correctly. They are also very helpful while developing instant answers as a tool to quickly test code iterations. Once you've written a test file, you can test it on it's own by running:

```perl
prove -Ilib t/TestName.t
```

 or you can run all the tests in the repository by running:

```perl
prove -Ilib t/
```