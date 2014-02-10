# Installing DuckPAN

**The DuckDuckHack Testing Tool**

DuckPAN is an application built to provide developers an environment for DuckDuckHack Instant Answers. It allows you to try out your creations and preview their visual design and output. This is only required when developing Spice or Goodies.

## Disclaimer

Currently, DuckPAN has been developed on, and works well with **Ubuntu**. More specifically, we regularly build, test, and run DuckPAN on **Ubuntu 12.04**. We have also successfully installed and run DuckPAN on older and newer Ubuntu releases, e.g. Ubuntu 10.04, 12.10, and 13.04.

Developers have also been successful running DuckPAN on other Linux distros (e.g. Arch, Debian), but **we make no promises that it will work outside of Ubuntu**.

Also, **there have been reported issues with installing DuckPAN on Mac OS X and Windows**, so we don't recommend you go down that path.

That being said, we are more than willing to help you debug any installation problems, so please come to us with your problems, and we'll try to get your issues sorted out. If you'd like some help from our community, feel free to engage with them on the [DuckDuckGo forum](http://duck.co/), the [DuckDuckHack e-mail list](https://www.listbox.com/subscribe/?list_id=197814), or on our [IRC channel](http://webchat.freenode.net/?channels=duckduckgo).

## Getting Started

The easiest way to get started with DuckPAN is to use our DuckDuckHack development virtual machine image ([see below](#duckduckhack-development-virtual-machine)), but there are also other ways of doing it:

- Use the Vagrant virtual environment to run DuckDuckHack ([see below](#advanced-vagrant-virtual-environment))
- Download and install [Ubuntu](http://www.ubuntu.com/download) yourself.

**If you're going to use our virtual machine** please continue reading. 
If not, go setup your OS and continue with the DuckPAN [installation instructions](#advanced-installing-duckpan-yourself) below.

## DuckDuckHack Development Virtual Machine

Our virtual machines have everything you need to start developing your instant answers right away.

#### DDH VM Breakdown

- Ubuntu 12.04 LTS
- Perl 5.16.3 (managed by Perlbrew)
- build-essential (for make, gcc, cc, etc)
- cpanminus (managed by Perlbrew)
- App::DuckPAN
- XFCE Window Manager
- Sublime Text, Vim, and Emacs
- Firefox (configured via fixtracking.com)
- Platform specific virtualization guest tools (optimizes hardware emulation)

#### For [VirtualBox](https://www.virtualbox.org/)

MD5: 1734373cbecc5820bb7d18406eb42854  
[https://ddg-community.s3.amazonaws.com/ddh-vbox.rar](https://ddg-community.s3.amazonaws.com/ddh-vbox.rar)

#### For [VMWare](http://www.vmware.com/)

MD5: 95ad9acfacadb4b0cb0cf23ffaa3516e  
[https://ddg-community.s3.amazonaws.com/ddh-vmw.rar](https://ddg-community.s3.amazonaws.com/ddh-vmw.rar)

#### A Note on Extracting RAR Archives

We're working on making Zip archives, but for the meantime, here are some third-party applications for extracting RAR archives:

**Windows:** You can use [PeaZip](http://peazip.org/) or [7Zip](http://www.7-zip.org/).  
**Mac OS X:** You can use [The Unarchiver](http://unarchiver.c3.cx/unarchiver).  
**Linux:** You can use [PeaZip](http://peazip.org/peazip-linux.html), or you can install `unrar` which is `sudo apt-get install unrar` on Ubuntu. 

#### Roadmap

- Docker support
- Public AMI for use on EC2

### Using the Virtual Machine

To use the Virtual Machine, you will need to download and install **VirtualBox**, **VMWare Workstation**, or **VMWare Player** depending on your current OS.

#### VirtualBox

Website: https://www.virtualbox.org/  
Supports: Windows, OS X, and Linux

##### Setup Instructions

1. Download the RAR archive and decompress. This archive contains the VMDK (Virtual Machine Disk) and OVF (Open Virtualization Format) files. 

2. Open VirtualBox, click "File" and then click "Import Appliance"

3. Click "Open appliance..." and select the DuckDuckHack virtual appliance and click "Next"

4. Click "Import"

#### VMWare Player

Website: https://www.vmware.com/products/player/  
Supports: Windows and Linux

##### Setup Instructions

1. Download the RAR archive and decompress. This contains the VMDK (Virtual Machine Disk) and OVF (Open Virtualization Format) files.

2. Open VMWare Player, and click on "Open a Virtual Machine"

3. Choose a storage path for the Virtual Machine and click "Import"

#### Happy Hacking!

Once you have installed the virtual machine you should be able to startup the VM and login with the following credentials:  

- **username** : `dax`  
- **password** : `duckduckhack`

**The DuckPAN client has already been installed for you.** Skip to the next section to continue on your journey.


## Advanced: Vagrant Virtual Environment

The Vagrant-based DuckDuckHack virtual environment provides a similar sandbox to the DuckDuckHack VM. But rather than downloading a pre-built VM, Vagrant creates an environment for you based on the defined configuration. Vagrant is an awesome tool for building development environments. One command--`vagrant up`--gets you a complete working environment in minutes. Something went wrong with the environment? No messing around with snapshots. Tear the VM down and build a fresh environment. The DuckDuckHack Vagrant environment uses Chef cookbooks and the DuckPAN installer script, so configuration is transparent and easily shared.

Through the Vagrant configuration, you can easily switch back and forth between a headless-mode and the traditional VirtualBox interface. The configuration defaults to headless.

**Note:** This installation method was contributed by our amazing community. Just remember that the scripts used were not made by DuckDuckGo so any issues regarding this should be posted on [duckpan-vagrant](https://github.com/shedd/duckpan-vagrant).

##### Setup Instructions

1. Install [VirtualBox](https://www.virtualbox.org/), [Vagrant](http://docs.vagrantup.com/v2/installation/index.html), and [Bundler](http://bundler.io/#getting-started).

2. Run `git clone https://github.com/shedd/duckpan-vagrant` and then `cd duckpan-vagrant`. The repository contains the `Vagrantfile` and the Chef cookbooks that you'll need.

3. Run `sudo bundle install` to install Berkshelf, a Chef cookbook manager.

4. Run `vagrant plugin install vagrant-berkshelf` to hook Berkshelf into Vagrant.

5. Review the CUSTOM_CONFIG settings at the top of `Vagrantfile`.  You will want to customize the value of the synced directory to point to your local directory containing the DuckDuckGo code you wish to test. By default, Vagrant will load a [VirtualBox Precise64](http://files.vagrantup.com/precise64.box) machine image.  If you change this, just remember that [Ubuntu is recommended](https://github.com/duckduckgo/p5-app-duckpan#disclaimer).

6. Run `vagrant up`

The box takes some time to stand up as the duckpan-install script runs. Refer to [the duckpan-vagrant readme](https://github.com/shedd/duckpan-vagrant#installation) for more info.

Once the environment has been built, **the DuckPAN client is installed and ready to go.** You can now clone the instant answer repos and start developing/testing.

##### Quick Overview of key Vagrant commands

There are a couple of key Vagrant commands that you'll use to manage your environment.

```shell
$ vagrant

up       - Build environment from Vagrantfile or resume a previously halted environment.
ssh      - Connect to your running VM via SSH.
suspend  - Pause the VM, storing its current state to disk.
resume   - Bring a suspended VM back to life.
reload   - The equivalent of running a halt followed by an up.  Use this when you make changes to Vagrantfile.
halt     - Shut down the VM. Tries to gracefully shutdown first; if that fails, it will forcefully shut the VM down.
destroy  - Stop the currently running VM and blow everything away.
```

Run these commands from the directory containing your `Vagrantfile`.

For more information, please see the (excellent) [Vagrant docs](http://docs.vagrantup.com/).


## Advanced: Installing DuckPAN Yourself

**Note**: You don't need to install DuckPAN if you're using our DuckDuckHack virtual machine or Vagrant. It should be already installed for you!

To install DuckPan, open your terminal and run:

```shell
curl http://duckpan.org/install.pl | perl
```

[This script](https://github.com/duckduckgo/p5-duckpan-installer) will setup [local::lib](https://metacpan.org/module/local::lib), which is a way to install Perl modules without changing your base Perl installation. If you already use local::lib or [perlbrew](https://metacpan.org/module/perlbrew), don't worry. This script will intelligently use what you already have.

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

If during the course of your DuckPAN install you run into errors, don't panic. There are a few things you can try.

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

## Using DuckPAN

Running `$ duckpan` with no commands will output some help information. More details on the DuckPAN commands can be found in the [DuckPAN README](https://github.com/duckduckgo/p5-app-duckpan/blob/master/README.md).
