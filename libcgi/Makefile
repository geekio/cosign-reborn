CC= gcc
DEFS= 
OPTOPTS= 
CFLAGS= -g $(DEFS) ${OPTOPTS} -fPIC
LDFLAGS= 
SRC= cgi.c
OBJ= cgi.o

RM= /bin/rm -f

all: libcgi.a

libcgi.a libcgi_p.a: $(OBJ)
	@echo "building normal libcgi.a"
	@ar cru libcgi.a $(OBJ)
	@ranlib libcgi.a

clean:
	rm -f libcgi.a cgi.o

distclean: clean
	rm -f config.log config.status
