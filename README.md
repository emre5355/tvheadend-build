<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
 

- [Looking for tvheadend builds?](#looking-for-tvheadend-builds)
- [Reference example: Ubuntu builds](#reference-example-ubuntu-builds)
- [Authoring packages for other Distros](#authoring-packages-for-other-distros)
- [Cross-compiling for ARM](#cross-compiling-for-arm)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)

### Looking for tvheadend builds?

We have auto builds for the following operating systems and architectures:

* Ubuntu `14.04.2` *and higher* - Debian APT.
  * `Intel x86_64`

Download and enjoy the official pre-built tvheadend packages. Available from:

https://tvheadend.org/projects/tvheadend/wiki/AptRepository

### Reference example: Ubuntu builds
**_Build chain for Ubuntu .deb binary pkgs of Tvheadend server_**

Reference guide for package maintainers, starts here:

* [Maintainers Guide - ubuntu builds](ubuntu/0. maintainers-guide.md)

### Authoring packages for other Distros

There are now packages for ubuntu. But what about Debian, openSUSE, Fedora, CentOS, Arch and whatever other distros ? You must follow / tweak the reference example to suit your needs:

* [Maintainers Guide - ubuntu builds](ubuntu/0. maintainers-guide.md)

For this example, we use the `centos` distribution. We assume you are also a user of `centos` who is familiar with it's package manager.

* Copy the whole folder, from `ubuntu/` --> `centos/` etc.
  * `git clone https://github.com/tvheadend/tvheadend-build.git`
  * `cd tvheadend-build && cp -rf ubuntu centos`

* In the new folder, find the dependancies base image `deps/Dockerfile`
  * Change the 1st line:
    * `FROM: ubuntu-debootstrap:14.04` ---> a decent minimal official docker base image of `centos` or `debian` etc. whatever.
  * Change the `apt-get install` ---> commands specific to your distro's package manager e.g. `yum`.

* In the remaining folders: `master/`, `unstable`, `testing` and `stable/` open the `Dockerfile`: 
  * Change the 1st line:
    * `FROM: dreamcat4/tvh.build.ubuntu.deps` ---> `FROM: yourDockerUsername/tvh.build.centos.deps`
  * Change the `Autobuild.sh` line, which builds a `.deb` file, to build an rpm instead.
    * Try to keep all the same `./configure` args such as `----enable-libffmpeg_static` etc.
  * At bottom, we run a script to upload the `/out` files to a bintray repo:
    * You will need modify that script `upload-to-bintray` also.

Follow all the the other steps in the Ubuntu guide - it is mostly the same. Just with different repo names, username, and so on.

* Commit changes to git.
* Push the new `centos` folder up to github.

### Cross-compiling for ARM

Dockerhub is an `x86_64` build farm. So to use Dockerhub for compiling Tvheadend for other architectures means cross compiling on intel host.

You must follow / tweak the reference example to suit your needs:

* [Maintainers Guide - ubuntu builds](ubuntu/0. maintainers-guide.md)

Some useful links for cross-compiling:

* http://vraidsys.com/2013/06/cross-compile-tvheadend-for-arm-cortex-a9/
* https://github.com/jzerbe/jzerbe.github.com/blob/master/_posts/2013-06-22-cross-compile-tvheadend-for-arm-cortex-a9.md
* http://www.holik.at/index.php?m=06&y=13&entry=entry130627-175237


