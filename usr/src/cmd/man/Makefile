#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2012 Nexenta Systems, Inc. All rights reserved.
# Copyright 2014 Garrett D'Amore <garrett@damore.org>
# Copyright 2019 OmniOS Community Edition (OmniOSce) Association.
#

PROG=		man
LINKS=		apropos whatis catman
LIBLINKS =	makewhatis
OBJS=		makewhatis.o man.o stringlist.o
MANIFEST=	update-man-index.xml
SVCMETHOD=	update-man-index

include		$(SRC)/cmd/Makefile.cmd

ROOTMANIFESTDIR=	$(ROOTSVCSYSTEM)

CFLAGS +=	$(CCVERBOSE)

ROOTLINKS=	$(LINKS:%=$(ROOTBIN)/%) $(LIBLINKS:%=$(ROOTLIB)/%)

.KEEP_STATE :

all:		$(PROG)

clean:
		$(RM) $(OBJS)

install:	all $(ROOTPROG) $(ROOTLINKS) $(ROOTMANIFEST) $(ROOTSVCMETHOD)

check:		$(CHKMANIFEST)

$(PROG):	$(OBJS)
		$(LINK.c) $(OBJS) -o $@ $(LDLIBS)
		$(POST_PROCESS)

$(ROOTLINKS):	$(ROOTPROG)
		$(RM) $@; $(LN) $(ROOTPROG) $@

include		$(SRC)/cmd/Makefile.targ
