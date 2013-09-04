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

COMPONENT_NAME=		libstatgrab
COMPONENT_VERSION=	0.17
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= sha256:bbaa88c6bde8bd3cf2720b81a26528cc055a7e83e4ea3bdb1d0a3c4287cceb88
COMPONENT_PROJECT_URL=	http://www.i-scream.org/libstatgrab
COMPONENT_ARCHIVE_URL=	http://dl.ambiweb.de/mirrors/ftp.i-scream.org/libstatgrab/$(COMPONENT_ARCHIVE)

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

COMPONENT_POST_CONFIGURE_ACTION=(cd $(SOURCE_DIR); \
			perl -pi -e 's/libstatgrab_la_LIBADD =/libstatgrab_la_LIBADD = -lkstat -ldevinfo/g'  ./src/libstatgrab/Makefile)

build:          $(BUILD_32)

install:        $(INSTALL_32)

test:           $(TESTS_32)
