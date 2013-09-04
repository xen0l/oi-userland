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

COMPONENT_NAME=		resource-agents
COMPONENT_VERSION=	3.9.5
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	v$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_HASH= sha256:da9f29418f1871f4545b0e44629630766e31a8d607209ab883764da3ba4d73c3
COMPONENT_PROJECT_URL=	https://github.com/ClusterLabs/resource-agents
COMPONENT_ARCHIVE_URL=	https://github.com/ClusterLabs/resource-agents/archive/$(COMPONENT_ARCHIVE)

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

PATH=/usr/perl5/5.16/bin:/usr/bin:/usr/gnu/bin

CFLAGS += "-lnsl"

CONFIGURE_ENV += MAKE="$(GMAKE)"

CONFIGURE_OPTIONS += --sysconfdir=/etc
CONFIGURE_OPTIONS += --localstatedir=/var
CONFIGURE_OPTIONS += --enable-fatal-warnings=no
CONFIGURE_OPTIONS += --with-ocf-root=/usr/lib/ocf

CONFIGURE_SCRIPT = $(@D)/configure

COMPONENT_PREP_ACTION=(cd $(SOURCE_DIR); \
			perl -pi -e 's/unsigned-char//g' configure.ac; \
			perl -pi -e 's/\$$\(XSLTPROC\) \\/\$$\(XSLTPROC\) --novalid \\/g' doc/man/Makefile.am; \
			./autogen.sh)

COMPONENT_PRE_CONFIGURE_ACTION=($(CLONEY) $(SOURCE_DIR) $(@D))

build:          $(BUILD_32)

install:        $(INSTALL_32)

test:           $(TESTS_32)
