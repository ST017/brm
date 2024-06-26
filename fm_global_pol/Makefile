###########
#
# @(#)% full_filespec: Make.user~21 %
#
# Copyright (c) 1996, 2017, Oracle and/or its affiliates. All rights reserved.
#
#      This material is the confidential property of Oracle
#      Corporation or its licensors and may be used, reproduced,
#      stored or transmitted only in accordance with a valid
#      Oracle license or sublicense agreement.
#
###########

OS=linux
VERSION=7.5

##########

PINDIR=/app/local/oracle/product/pin01/brm12/BRM
INCDIR=$(PINDIR)/PortalDevKit/include
LIBDIR=$(PINDIR)/lib


##########
CC_solaris = cc
CC_hpux = cc
CC_hpux_ia64 = cc
CC_aix = xlc_r
CC_linux = gcc 
CC = $(CC_$(OS))

###########

CFLAGS_solaris= -g
CFLAGS_hpux= -g -Ae +Z +DAportable
CFLAGS_hpux_ia64= -g -Ae +Z
CFLAGS_aix= -g -Drs6000 -D__aix -Dunix -D__unix
CFLAGS_linux= -m32 -fPIC
CFLAGS= $(CFLAGS_$(OS)) -DFOR_CM -DFM_CUST_POL_DLL

CPPFLAGS = -I$(INCDIR) -DPCMCPP_CONST_SAFE -DFOR_CM -DFM_CUST_POL_DLL

LDFLAGS_solaris= -G
LDFLAGS_hpux= -b
LDFLAGS_hpux_ia64= -b
LDFLAGS_aix= -G -bnoentry -bexpall -brtl -lc
LDFLAGS_linux= -m elf_i386 -shared -L/usr/lib 
LDFLAGS = $(LDFLAGS_$(OS)) -L$(LIBDIR)


SL_EXT_solaris= so
SL_EXT_hpux= sl
SL_EXT_hpux_ia64= so
SL_EXT_aix= a 
SL_EXT_linux= so
SL_EXT= $(SL_EXT_$(OS))

##########

INCFILES= $(INCDIR)/pin_cust.h $(INCDIR)/pcm.h \
	$(INCDIR)/pin_errs.h $(INCDIR)/pinlog.h 

#
FILES= fm_global_pol_config.c \
       fm_global_pol.c  
	


OBJECTS= fm_global_pol_config.o \
        fm_global_pol.o 



#

LIBCUST=fm_global_pol.$(SL_EXT)

###########

all: $(LIBCUST)

clean:
	rm -f $(OBJECTS) core

clobber: clean
	rm -f $(LIBCUST)

lint:
	lint $(CPPFLAGS) $(FILES)

tags: FRC

###########

$(LIBCUST): $(OBJECTS) $(INCFILES) Makefile
	$(LD) -o $(LIBCUST) $(LDFLAGS) $(OBJECTS) -lpin_cc -lm -lpsiu_for_cm -lregex -ldl 

$(OBJECTS): $(INCFILES) Makefile
	$(CC) -c $(CFLAGS) $(CPPFLAGS) $(FILES)

#

FRC:
