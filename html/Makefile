TEMPLATES = error.html expired_error.html login.html login_error.html verify-logout.html reauth.html
HTML = cosign_base.css cosign_js.css post_error.html looping.html
prefix=/var/lib/cosign
exec_prefix=${prefix}
TMPLDIR  = /var/lib/cosign/templates
HTMLDIR  = /var/lib/cosign/html
SERVICESDIR  = /var/lib/cosign/services
INSTALL	=	/usr/bin/install -c

all: ${TEMPLATES}

install : all
	-mkdir -p ${DESTDIR}${exec_prefix}
	-mkdir -p ${DESTDIR}${TMPLDIR}
	-mkdir -p ${DESTDIR}${HTMLDIR}
	for i in ${TEMPLATES}; do \
	    ${INSTALL} -m 0644 -c $$i ${DESTDIR}${TMPLDIR}/; \
	done
	for i in ${HTML}; do \
	    ${INSTALL} -m 0644 -c $$i ${DESTDIR}${HTMLDIR}/; \
	done
	-mkdir -p ${DESTDIR}${HTMLDIR}/images
	cp images/*.gif ${DESTDIR}${HTMLDIR}/images/
	cp images/*.png ${DESTDIR}${HTMLDIR}/images/
	-mkdir -p ${DESTDIR}${HTMLDIR}/js
	cp js/*.js ${DESTDIR}${HTMLDIR}/js/
	-mkdir -p ${DESTDIR}${SERVICESDIR}
	cp services/*.html ${DESTDIR}${SERVICESDIR}/

clean:
