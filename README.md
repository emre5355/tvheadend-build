![License MIT](https://img.shields.io/badge/license-MIT-blue.svg)

## dreamcat4/tvh.ubuntu.build.*
**_Builders for Ubuntu .deb binary pkgs of Tvheadend server_**

Reference guide for package maintainers, starts here:

- [dreamcat4/tvh.ubuntu.build.*](ubuntu/0. maintainers-guide.md)

### Making pkgs for other Distros

So we've made packages for ubuntu. But what about Debian, openSUSE, Fedora, CentOS, Arch and whatever other distros ?

* Copy/rename the whole folder, from `ubuntu/`
  * To e.g. `centos/` etc.

* In the new base image `deps/` Dockerfile
  * Change the 1st line:
    * `FROM: ubuntu-debootstrap:14.04` ---> a decent minimal official docker base image of `centos` or `debian` etc. whatever.
  * Change the `apt-get install` ---> commands specific to your distro's package manager.

* In the `master/` and `stable/` `Dockerfile`s of the actual builder images
  * Change the 1st line:
    * `FROM: dreamcat4/tvh.build.ubuntu.deps` ---> `FROM: yourUsername/tvh.build.centos.deps`
  * Change the `Autobuild.sh` line, which builds a `.deb` file, to instead make your rpm or whatever other kind of pkg.
    * Try to keep all the same `./configure` args such as `----enable-libffmpeg_static` etc.
  * At bottom, when uploading `/out` files to your bintray repo:
    * You may need to change the file `find` commands, for example:
      * tvh_deb="$(find /out -name 'tvheadend_*.deb')" - matches on `.deb` file (not rpm, like you need it to).

And follow all the the other steps in the Ubuntu guide mostly the same. Just substituting different repo names / labels whenever needed.
