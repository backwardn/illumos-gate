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
# Copyright 2009 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
#

include $(SRC)/Makefile.psm

LIBRARY=	libfruaccess.a
VERS=		.1

OBJECTS=	libfruaccess.o

# include library definitions
include $(SRC)/lib/Makefile.lib

ROOT_PLATFORM = $(USR_PLAT_DIR)/SUNW,Netra-T12

include	$(SRC)/cmd/picl/plugins/Makefile.com

CPPFLAGS +=	-D_REENTRANT
CPPFLAGS +=	-I$(SRC)/uts/sun4u/ -I$(SRC)/uts/common/

SRCS=		$(OBJECTS:%.o=%.c)

LIBS =		$(DYNLIB)

ROOTLIBDIR	= $(ROOT_PLAT_LIBDIR)

CFLAGS +=	$(CCVERBOSE)
CPPFLAGS +=	-I$(SRC)/uts/sun4u/lw8
CPPFLAGS +=	-I$(SRC)/cmd/picl/plugins/sun4u/lib/fruaccess
DYNFLAGS +=	-R/usr/platform/\$$PLATFORM/lib/picl/plugins:/usr/platform/sun4u/lib/picl/plugins:/usr/lib/picl/plugins
LDLIBS +=	-L$(SRC)/lib/libptree/$(MACH)
LDLIBS +=	-L$(ROOT)/usr/lib/picl/plugins
LDLIBS +=	-lc -lpicltree

.KEEP_STATE:

SUBDIRS=

all :=		TARGET= all
install :=	TARGET= install
clean :=	TARGET= clean
clobber :=	TARGET= clobber
_msg :=		TARGET= _msg

POFILE= libfruaccess.po

all: $(LIBS) $(LIBLINKS)

install:	$(ROOTLIBDIR) all  $(ROOTLIBS) $(ROOTLINKS)

_msg:	$(MSGDOMAIN) $(POFILE)
	$(RM) $(MSGDOMAIN)/$(POFILE)
	$(CP) $(POFILE) $(MSGDOMAIN)/lw8_$(POFILE)

$(MSGDOMAIN):
	$(INS.dir)

$(LIBLINKS):    FRC
	rm -f $(LIBLINKS); ln -s $(DYNLIB) $(LIBLINKS)

# include library targets
include	$(SRC)/cmd/picl/plugins/Makefile.targ
include $(SRC)/lib/Makefile.targ

lint :

$(SUBDIRS): FRC
	@cd $@; pwd; $(MAKE) $(TARGET)

FRC:
