INSTALL = /usr/bin/ginstall -c -D
INSTALL_PROGRAM = ${INSTALL} -D
INSTALL_DATA = ${INSTALL} -m 644 -D

srcdir = ../src
BUILD =  ../build
prefix = $(BUILD)
exec_prefix = ${prefix}

SHAREDOPT = -shared -shared -fPIC,-Wl,-soname,libcgi.so.0
libdir = $(prefix)/lib
incdir = $(prefix)/include/libcgi
mandir	= $(prefix)/man/man3
SHELL = /bin/sh
EXTRA_LIBS =

INCS =  -I$(srcdir)
FLAGS = -Wall -D_REENTRANT



OBJS = $(BUILD)/error.o $(BUILD)/cgi.o $(BUILD)/session.o $(BUILD)/base64.o $(BUILD)/md5.o \
	$(BUILD)/string.o $(BUILD)/general.o $(BUILD)/list.o $(BUILD)/cookie.o

SHOBJS = $(OBJS:.o=.sh.o)

$(BUILD)/%.o: $(srcdir)/%.c
	$(CC) $(FLAGS) -c $(srcdir)/$*.c -o $@

$(BUILD)/%.sh.o: $(srcdir)/%.c
	$(CC) $(FLAGS) -fPIC -c $(srcdir)/$*.c -o $@

all: $(BUILD)/libcgi.so $(BUILD)/libcgi.a test

test: test.c $(BUILD)/libcgi.so
	$(CC) $(FLAGS) test.c -L$(BUILD) -lcgi -o test -Wl,-rpath=\$$ORIGIN/$(BUILD)


	@echo ""
	@echo ""
	@echo ""
	@echo "+---------------------------------------+"
	@echo "|       Thanks for using LibCGI         |"
	@echo "+---------------------------------------+"
	@echo "| LibCGI is getting better because      |"
	@echo "| people like you are using it. So, if  |"
	@echo "| LibCGI is helping you in some way,    |"
	@echo "| please help us to improve it, sending |"
	@echo "| suggestions, bug reports, bug fixes,  |"
	@echo "| and specially improvment code.        |"
	@echo "| You can subscribe to the mailing list |"
	@echo "| or send a mail to the author.         |"
	@echo "+---------------------------------------+"
	@echo ""


shared: $(BUILD)/libcgi.so
	$(INSTALL) -m 0644 $(BUILD)/libcgi.so $(DESTDIR)$(libdir)

$(BUILD)/libcgi.a: $(OBJS)
	$(AR) rc $(BUILD)/libcgi.a $(OBJS)

$(BUILD)/libcgi.so: $(SHOBJS)
	$(CC) $(SHAREDOPT) -o $(BUILD)/libcgi.so $(SHOBJS) $(EXTRA_LIBS)

install:
	$(INSTALL) -m 0644 $(BUILD)/libcgi.a $(DESTDIR)/$(libdir)/libcgi.a
	$(INSTALL) -m 0644 $(BUILD)/libcgi.so $(DESTDIR)/$(libdir)/libcgi.so
	$(INSTALL) -m 0644 $(srcdir)/cgi.h $(DESTDIR)/$(incdir)/cgi.h
	$(INSTALL) -m 0644 $(srcdir)/session.h $(DESTDIR)/$(incdir)/session.h

$(BUILD)/error.o: $(srcdir)/error.c $(srcdir)/error.h
$(BUILD)/cgi.o: $(srcdir)/cgi.c $(srcdir)/cgi.h
$(BUILD)/session.o: $(srcdir)/session.c $(srcdir)/session.h
$(BUILD)/base64.o: $(srcdir)/base64.c
$(BUILD)/md5.o: $(srcdir)/md5.c
$(BUILD)/string.o: $(srcdir)/string.c
$(BUILD)/cookie.o: $(srcdir)/cookie.c
$(BUILD)/general.o: $(srcdir)/general.c
$(BUILD)/list.o: $(srcdir)/list.c

clean:
	find $(BUILD)/ -name *.o -exec rm -f {} \;
	find $(BUILD)/ -name *.a -exec rm -f {} \;
	find $(BUILD)/ -name *.so -exec rm -f {} \;

uninstall: clean
	rm -f $(libdir)/libcgi.*
	rm -f $(incdir)/cgi.h
	rm -f $(incdir)/session.h
	rm -f $(mandir)/libcgi*

install_man:
	cp doc/man/man3/libcgi_base64.3 $(DESTDIR)$(mandir)
	cp doc/man/man3/libcgi_cgi.3 $(DESTDIR)$(mandir)
	cp doc/man/man3/libcgi_general.3 $(DESTDIR)$(mandir)
	cp doc/man/man3/libcgi_string.3 $(DESTDIR)$(mandir)
	cp doc/man/man3/libcgi_session.3 $(DESTDIR)$(mandir)
	cp doc/man/man3/libcgi_cookie.3 $(DESTDIR)$(mandir)

