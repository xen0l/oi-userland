#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#

#
# Copyright (c) 2019, Oracle and/or its affiliates. All rights reserved.
#

BUILD_STYLE = setup.py
BUILD_BITS = NO_ARCH

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		PyHamcrest
COMPONENT_VERSION=	1.10.1
COMPONENT_SUMMARY=	'Hamcrest framework for matcher objects'
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:f7ae19ddfd71f11a421bcec9608d708c0fab816db98b51fdbc672a6d99a30874
COMPONENT_ARCHIVE_URL=	$(call pypi_url)
COMPONENT_PROJECT_URL=	https://github.com/hamcrest/PyHamcrest
COMPONENT_CLASSIFICATION= Development/Python
COMPONENT_FMRI=	library/python/python-hamcrest
COMPONENT_LICENSE= BSD
COMPONENT_LICENSE_FILE= LICENSE.txt

PYTHON_VERSIONS = 2.7 3.4 3.5

TEST_TARGET = $(NO_TESTS)

include $(WS_MAKE_RULES)/common.mk

# Auto-generated dependencies
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += runtime/python-34
REQUIRED_PACKAGES += runtime/python-35
