prefix=/var/lib/cosign
exec_prefix=${prefix}
SBINDIR=/usr/local/sbin
CGIDIR  = /var/lib/cosign/cgi-ssl
HTMLDIR  = /var/lib/cosign/html
COSIGNCADIR=/etc/cosign/certs/CA
COSIGNCERT=/etc/cosign/certs/cosignd.crt
COSIGNKEY=/etc/cosign/certs/cosignd.key
COSIGNHOST = cosign.example.edu
COSIGNLOGOUTURL = http://cosign.example.edu
COSIGNLOGOUTREGEX = http://.+\.example\.edu
COSIGNLOOPURL = http://cosign.example.edu/looping.html
COSIGNTMPLDIR = /var/lib/cosign/templates
COSIGNTICKETCACHE = /ticket
COSIGNCONF= /etc/cosign/cosign.conf
KEYTABPATH = 
FRIEND_MYSQL_DB = localhost
FRIEND_MYSQL_LOGIN = friend
FRIEND_MYSQL_PASSWD = 

INCPATH=      -I/usr/local/include   -I../common -I../libsnet -I../libcgi
OPTOPTS=     -Wall -Wmissing-prototypes 
CC=          gcc
DEFS=
LIBS=        -lsnet -lcgi  -lssl -lcrypto  
LDFLAGS=     -L../libsnet/.libs -L../libcgi  -L/usr/local/lib   ${LIBS}
INSTALL=     /usr/bin/install -c

CFLAGS=      ${DEFS} ${OPTOPTS} -fPIC ${INCPATH}


OBJ     = network.o subfile.o ../common/mkcookie.o ../common/fbase64.o \
	../common/conf.o ../common/wildcard.o ../common/argcargv.o \
	../version.o 
TARGETS = logout cosign.cgi

all: ${TARGETS}

login.o:	login.c
	${CC} ${CFLAGS} \
	-D_COSIGN_TICKET_CACHE=\"${COSIGNTICKETCACHE}\" \
	-D_KEYTAB_PATH=\"${KEYTABPATH}\" \
	-D_FRIEND_MYSQL_DB=\"${FRIEND_MYSQL_DB}\" \
	-D_FRIEND_MYSQL_LOGIN=\"${FRIEND_MYSQL_LOGIN}\" \
	-D_FRIEND_MYSQL_PASSWD=\"${FRIEND_MYSQL_PASSWD}\" \
	-c login.c

cgi.o:	cgi.c
	${CC} ${CFLAGS} \
	-D_COSIGN_HOST=\"${COSIGNHOST}\" \
	-D_COSIGN_LOOP_URL=\"${COSIGNLOOPURL}\" \
	-D_COSIGN_TLS_CADIR=\"${COSIGNCADIR}\" \
	-D_COSIGN_TLS_CERT=\"${COSIGNCERT}\" \
	-D_COSIGN_TLS_KEY=\"${COSIGNKEY}\" \
	-D_COSIGN_CONF=\"${COSIGNCONF}\" \
	-D_COSIGN_TMPL_DIR=\"${COSIGNTMPLDIR}\" \
	-c cgi.c

cosign.cgi: cgi.o login.o factor.o $(OBJ)
	${CC} ${CFLAGS} -o cosign.cgi cgi.o login.o factor.o $(OBJ) $(LDFLAGS)

logout.o:	logout.c
	${CC} ${CFLAGS} \
	-D_COSIGN_HOST=\"${COSIGNHOST}\" \
	-D_COSIGN_LOGOUT_URL=\"${COSIGNLOGOUTURL}\" \
	-D_COSIGN_LOGOUT_RE=\"${COSIGNLOGOUTREGEX}\" \
	-D_COSIGN_TLS_CADIR=\"${COSIGNCADIR}\" \
	-D_COSIGN_TLS_CERT=\"${COSIGNCERT}\" \
	-D_COSIGN_TLS_KEY=\"${COSIGNKEY}\" \
	-D_COSIGN_CONF=\"${COSIGNCONF}\" \
	-D_COSIGN_TMPL_DIR=\"${COSIGNTMPLDIR}\" \
	-c logout.c

logout: logout.o $(OBJ)
	${CC} ${CFLAGS} -o logout logout.o $(OBJ) $(LDFLAGS)

clean:
	/bin/rm -rf *.o ${TARGETS}

install : all
	-mkdir -p ${DESTDIR}${exec_prefix}
	-mkdir -p ${DESTDIR}${CGIDIR};
	${INSTALL} -m 0755 -c cosign.cgi ${DESTDIR}${CGIDIR}/;
	${INSTALL} -m 0755 -c logout ${DESTDIR}${CGIDIR}/;
