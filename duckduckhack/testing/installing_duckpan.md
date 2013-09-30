# Installing DuckPAN

**\*\*Note**: You don't need to install DuckPAN if you're using our DuckDuckHack virtual machine. It's already installed for you!

To install DuckPan, open your terminal and run:

```shell
curl http://duckpan.org/install.pl | perl
```

[This script](https://github.com/duckduckgo/p5-duckpan-installer) will setup [local::lib](https://metacpan.org/module/local::lib), which is a way to install Perl modules without changing your base Perl installation. If you already use local::lib or [perlbrew](https://metacpan.org/module/perlbrew), don't worry, this script will intelligently use what you already have.

If you didn't have a local::lib before running the install script, you will need to run the script twice. It should tell you when like this:

```shell
please now re-login to your user account and run it again!
```

If everything works, you should see this at the end:

```shell
EVERYTHING OK! You can now go hacking! :)
```

Note that with local::lib now installed, you can easily install [Perl modules](http://search.cpan.org/) with [cpanm](https://metacpan.org/module/cpanm).

```shell
cpanm App::DuckPAN
App::DuckPAN is up to date.
```

### Dealing With Installation Issues
If during the course of your DuckPAN install you run into errors, don't panic, there are a few things you can try.

First, try running the install command again (`curl http://duckpan.org/install.pl | perl`), this often solves issues related to any dependencies.

If that doesn't work, you should investigate the build.log and see what's wrong. It might be a depencency issue which you can resolve by manually installing whichever dependency is missing via `cpanm`.

If it still won't install with `cpanm` try adding `--notest` to the cpanm command:

```shell
cpanm Test::More --notest
```

If that still doesn't work, you can also try using `--force`:

```shell
cpanm Test::More --force
```

If this ***still*** doesn't work, please create a GitHub Issue in the DuckPAN Repo [here](https://github.com/duckduckgo/p5-app-duckpan/issues). Be sure to paste the contents of your `build.log` and also let us know the details of your OS (`$ uname -a` is great). Once you've made the issue, we'll work with you to try and solve any problems you're having.