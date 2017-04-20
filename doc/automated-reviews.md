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


### Rules

#### Components

##### No copyright found

**Cause**: This check will be triggered if no copyright claim could be found.

**Fix**: Add your copyright to the mentioned file.

##### Usage of 'depend.mk' / 'BUILD_PKG_DEPENDENCIES'

**Cause**: depend.mk was a former way how to track build dependencies, but it was never widely used. This functionality
got replaced by REQUIRED_PACKAGES.

**Fix**: Remove line containing reference to depend.mk or BUILD_PKG_DEPENDENCIES.

##### WS_MAKE_RULES not found

**Cause**: Makefile includes are not using $(WS_MAKE_RULES) macro. This does not apply to shared-macros.mk include!

**Fix**: Switch every include line to use $(WS_MAKE_RULES) macro.

##### REQUIRED_PACKAGES presence

**Cause**: Some components have build-time/run-time dependencies and they have to be mentioned in the Makefile, so we
can rebuild component every time with the same feature set.

**Fix**: Run 'gmake REQUIRED_PACKAGES' to automatically guess dependencies. Any other dependencies needed for package building
shall be added manually.

##### COMPONENT_REVISION or COMPONENT_VERSION not bumped

**Cause**: COMPONENT_REVISION should be increased in Makefile if a new patch is added, Makefile was modified, a patch was removed,
IPS p5m manifest file was modified or removed. This is needed, so the Jenkins build can be retriggered for the component and built
with the change. If COMPONENT_VERSION is bumped, any line with COMPONENT_REVISION shall be removed.

**Fix**: Bump either COMPONENT_REVISION or COMPONENT_REVISION in the Makefile.

##### Component license file could not be found

**Cause**: Component license file is not present in the change.

**Fix**: Provide license file for component.
