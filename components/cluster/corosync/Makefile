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

COMPONENT_NAME=		corosync
COMPONENT_VERSION=	2.3.1
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	v$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_HASH= sha256:ceb90c2b57c4d9dc07e0f0220a2971c7ab9f4a33cc4e165ebff44d526982fd12
COMPONENT_PROJECT_URL=	https://github.com/corosync/corosync
COMPONENT_ARCHIVE_URL=	https://github.com/corosync/corosync/archive/$(COMPONENT_ARCHIVE)

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

CONFIGURE_ENV += MAKE="$(GMAKE)"
CONFIGURE_ENV += nss_LIBS="-R/usr/lib/mps -L/usr/lib/mps -lnss3 -lnspr4"

CONFIGURE_OPTIONS += --sysconfdir=/etc/corosync
CONFIGURE_OPTIONS += --localstatedir=/var
CONFIGURE_OPTIONS += --enable-monitoring
CONFIGURE_OPTIONS += --enable-testagents
CONFIGURE_OPTIONS += --enable-augeas

COMPONENT_PREP_ACTION=(cd $(SOURCE_DIR); \
			./autogen.sh)

build:          $(BUILD_32)

install:        $(INSTALL_32)

test:           $(TESTS_32)
