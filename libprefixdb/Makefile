# This file is part of the PrefixDB library
# Copyright (c) 2014 Pierre-Yves Kerembellec <py.kerembellec@gmail.com>

PREFIX=/usr/local
CFLAGS=-Wall -O3 -I. -L.

test: libprefixdb.so.1 libprefixdb.a prefixdb
	./prefixdb bench

libprefixdb.so.1: libprefixdb.h libprefixdb.c
	$(CC) $(CFLAGS) -fpic -c -o libprefixdb-shared.o libprefixdb.c
	$(CC) $(CFLAGS) -shared -o libprefixdb.so.1 libprefixdb-shared.o

libprefixdb.a: libprefixdb.h libprefixdb.c
	$(CC) $(CFLAGS) -fpic -c -o libprefixdb-static.o libprefixdb.c
	$(AR) r libprefixdb.a libprefixdb-static.o

prefixdb: prefixdb.c libprefixdb.a
	$(CC) $(CFLAGS) -o prefixdb prefixdb.c libprefixdb.a

clean:

distclean:
	rm -f prefixdb *.o *.so* *.a

deb:
	debuild -i -us -uc -b

debclean:
	debuild clean

install: libprefixdb.h libprefixdb.so.1 libprefixdb.a prefixdb
	install -m 0755 prefixdb $(PREFIX)/bin
	install -m 0644 libprefixdb.so.1 libprefixdb.a $(PREFIX)/lib
	install -m 0644 libprefixdb.h $(PREFIX)/include

.PHONY: install
