CC	   = gcc
CGI_DIR    = $(DESTDIR)/usr/lib/cgi-bin/man
SHARE_DIR  = $(DESTDIR)/usr/share/man2html
DOC_DIR    = $(DESTDIR)/usr/share/doc/man2html-base

CGIBASE	   = /cgi-bin/man
MAN_CONFIG = /etc/manpath.config

CPPFLAGS += -DMAN_CONFIG='"$(MAN_CONFIG)"'
CFLAGS   += -pipe -g -Wall -Wextra $(DEBIAN_CFLAGS)

#
# Installer program:
#
INSTALL = install


targets: mansec manwhatis man2html.cgi

utils.o: utils.c utils.h

manwhatis: manwhatis.o utils.o
	$(CC) $(LDFLAGS) $^ -o $@

mansec: manwhatis
	ln -fs $< $@

man2html.cgi: man2html.cgi.o utils.o
	$(CC) $(LDFLAGS) $^ -o $@

install: targets
	$(INSTALL) -p -m 0755 man2html.cgi $(CGI_DIR)/man2html
	$(INSTALL) -p -m 0755 mansearch $(CGI_DIR)
	$(INSTALL) -p -m 0755 manwhatis $(CGI_DIR)
	ln $(CGI_DIR)/manwhatis $(CGI_DIR)/mansec
	$(INSTALL) -p -m0644 swish++.conf  $(SHARE_DIR)
	$(INSTALL) -p -m0644 man.html $(DOC_DIR)/html


clean:
	rm -f *.o *~ core manwhatis mansec man2html.cgi

spotless: clean

