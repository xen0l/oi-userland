#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2013 Adam Stevko. All rights reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		libqb
COMPONENT_VERSION=	0.16.0
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= sha256:cc28de10f71853a6ae23ef1b4d6953b16d242a610b1eb8c4134e383cc6c099c3
COMPONENT_PROJECT_URL=	https://github.com/ClusterLabs/libqb
COMPONENT_ARCHIVE_URL=	https://fedorahosted.org/releases/q/u/quarterback/$(COMPONENT_ARCHIVE)

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

CONFIGURE_ENV += MAKE="$(GMAKE)"

CONFIGURE_OPTIONS += --enable-debug

COMPONENT_PREP_ACTION=(cd $(@D); $(ENV) $(CONFIGURE_ENV) $(CONFIG_SHELL) autogen.sh)

COMPONENT_PRE_CONFIGURE_ACTION=($(CLONEY) $(SOURCE_DIR) $(@D)) 
CONFIGURE_SCRIPT= $(@D)/configure

build:          $(BUILD_32)

install:        $(INSTALL_32)

test:           $(TESTS_32)
