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
# Copyright 2013 Adam Stevko. All right reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		libesmtp
COMPONENT_VERSION=	1.0.6
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= sha256:3b4143ecaeacbbff3ed0f2a16da6fc5bfb4f778ea73914009a8be0a3020dc6a9
COMPONENT_PROJECT_URL=	http://www.stafford.uklinux.net/libesmtp
COMPONENT_ARCHIVE_URL=	http://www.stafford.uklinux.net/libesmtp/$(COMPONENT_ARCHIVE)

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

CFLAGS=-std=c89 -D__EXTENSIONS__ -DNAME_MAX=255 -DHOST_NAME_MAX=255

COMPONENT_PREP_ACTION=(cd $(SOURCE_DIR); mkdir m4; $(AUTORECONF) -i)

COMPONENT_PRE_CONFIGURE_ACTION=($(CLONEY) $(SOURCE_DIR) $(@D))
COMPONENT_POST_CONFIGURE_ACTION=(cd $(@D); perl -pi -e 's|// TODO: handle GEN_IPADD||' smtp-tls.c)
CONFIGURE_SCRIPT=$(@D)/configure

build:          $(BUILD_32)

install:        $(INSTALL_32)

test:           $(TESTS_32)
