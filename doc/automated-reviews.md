# Automated reviews of oi-userland

This file contains a list of all checks currently being controlled in [Dangerfile](https://github.com/OpenIndiana/oi-userland/blob/oi/hipster/doc/automated-reviews.md). Comments are divided into the following categories:

* **component changes** - any change in [components/](https://github.com/OpenIndiana/oi-userland/blob/oi/hipster/components) directory
* **documentation changes** - any change in [doc/](https://github.com/OpenIndiana/oi-userland/blob/oi/hipster/doc) directory
* **build system changes** - any change in [make-rules/](https://github.com/OpenIndiana/oi-userland/blob/oi/hipster/make-rules) directory
* **tools changes** - any change in [tools/](https://github.com/OpenIndiana/oi-userland/blob/oi/hipster/tools) directory
* **transform changes** - change in [transforms/](https://github.com/OpenIndiana/oi-userland/blob/oi/hipster/doc) directory

Currently, only component, documentation and build system changes are being reviewed. The aim of these checks is to offload developers
from reviews and enforce unified style of oi-userland assets, e.g. Makefiles.

## Implementation

Automated reviews are implemented via [Dangerfile](https://danger.systems) and [Travis CI](https://www.travis-ci.org), which is run
for every new PR opened.
