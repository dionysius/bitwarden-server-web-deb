# deb packaging for bitwarden server web vault

This debian source package builds [bitwarden web vault](https://github.com/bitwarden/clients/) natively on your build environment. It is managed with [git-buildpackage](https://wiki.debian.org/PackagingWithGit) and aims to be a pretty good quality debian source package. You can find the maintaining command summary in [debian/gbp.conf](debian/gbp.conf).

You will also need [bitwarden-server-deb](https://github.com/dionysius/bitwarden-server-deb).

## Download prebuilt packages

Prebuild deb and src packages are automatically built in [Github Actions](https://github.com/dionysius/bitwarden-server-web-deb/actions) for the latest Ubuntu LTS and Debian stable in various architectures (if applicable).

For manual installation they are available in the [releases section](https://github.com/dionysius/bitwarden-server-web-deb/releases) and you can verify the signatures with this [signing-key](signing-key.pub).

## Requirements

- Installed `git-buildpackage` from your apt
- Installed build dependencies as defined in [debian/control `Build-Depends`](debian/control) (will notify you in the build process otherwise)
  - [`mk-build-deps`](https://manpages.debian.org/testing/devscripts/mk-build-deps.1.en.html) can help you automate the installation
- If `nodejs`/`npm` is not recent enough
  - Don't forget to look into your `*-updates`/`*-backports` apt sources for newer versions
  - Use a package from [nodesource](https://github.com/nodesource/distributions/blob/master/README.md)
  - This debian source also supports those installed with help of [`nvm`](https://github.com/nvm-sh/nvm)
    - Requires preloaded `nvm use <version>` before invoking packaging

## Packaging

- Clone with git-buildpackage: `gbp clone https://github.com/dionysius/bitwarden-server-web-deb.git`
- Switch to the folder: `cd bitwarden-server-web-deb`
- Build with git-buildpackage: `gbp buildpackage`
  - There are many arguments to fine-tune the build (see `gbp buildpackage --help` and `dpkg-buildpackage --help`)
  - Notable options: `-b` (binary-only, no source files), `-us` (unsigned source package), `-uc` (unsigned .buildinfo and .changes file), `--git-export-dir=<somedir>` (before building the package export the source there), `-d` if you need to ignore build-depends (you probably still need them installed from a debian package)
