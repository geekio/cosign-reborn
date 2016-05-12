################## Some of this may need to be edited ##################

INCPATH=         -I/usr/local/include -I../libsnet -I.
CC=             gcc

OPTOPTS=	-Wall -Wmissing-prototypes 
CFLAGS=         ${DEFS} ${OPTOPTS} -fPIC ${INCPATH}

################ Nothing below should need editing ###################

SRC= argcargv.c conf.c fbase64.c mkcookie.c rate.c wildcard.c
COMMONOBJ= argcargv.o conf.o fbase64.o mkcookie.o rate.o wildcard.o

all : ${COMMONOBJ}

clean :
	rm -f a.out core* *.o *.bak *[Ee]rrs tags

