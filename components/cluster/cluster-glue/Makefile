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
# Copyright (c) 2013 Adam Stevko <adam.stevko@gmail.com> 
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		glue
COMPONENT_VERSION=	1.0.11
COMPONENT_HG_REV=	02bdcf58f9a0
COMPONENT_SRC=		Reusable-Cluster-Components-$(COMPONENT_NAME)--$(COMPONENT_HG_REV)
COMPONENT_ARCHIVE=	$(COMPONENT_HG_REV).tar.gz
COMPONENT_ARCHIVE_HASH= sha256:7a7eafedeffe7389af248cf33db874398a04f5306f5b15251f49d9744a15ca7f
COMPONENT_PROJECT_URL=	http://linux-ha.org/wiki/Cluster_Glue
COMPONENT_ARCHIVE_URL=	http://hg.linux-ha.org/glue/archive/$(COMPONENT_ARCHIVE)

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

CONFIGURE_OPTIONS += --sysconfdir=/etc
CONFIGURE_OPTIONS += --libexecdir=/usr/lib
#CONFIGURE_OPTIONS += --sharedstatedir=/var/cluster
CONFIGURE_OPTIONS += --localstatedir=/var
CONFIGURE_OPTIONS += --enable-ansi=no
CONFIGURE_OPTIONS += --enable-fatal-warnings=no
CONFIGURE_OPTIONS += --with-daemon-user=hacluster
CONFIGURE_OPTIONS += --with-daemon-group=haclient
CONFIGURE_OPTIONS += --with-ocf-root=$(CONFIGURE_PREFIX)/lib/ocf
CONFIGURE_OPTIONS += --enable-libnet

COMPONENT_PREP_ACTION=(cd $(SOURCE_DIR); perl -pi -e 's/-Wunsigned-char//g' configure.ac; \
					perl -pi -e 's/-fstack-protector-all//g' configure.ac; \
					perl -pi -e 's/\$$\(XSLTPROC\) \\/\$$\(XSLTPROC\) --novalid \\/g' doc/Makefile.am; \
					./autogen.sh)

build:          $(BUILD_32)

install:        $(INSTALL_32)

test:           $(TESTS_32)
