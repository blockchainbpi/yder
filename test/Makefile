#
# Glewlwyd OAuth2 Authorization Server
#
# Makefile used to build the software
#
# Copyright 2016 Nicolas Mora <mail@babelouest.org>
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU GENERAL PUBLIC LICENSE
# License as published by the Free Software Foundation;
# version 3 of the License.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU GENERAL PUBLIC LICENSE for more details.
#
# You should have received a copy of the GNU General Public
# License along with this program.  If not, see <http://www.gnu.org/licenses/>.
#

CC=gcc
CFLAGS+=-Wall -D_REENTRANT -DDEBUG -g -O0 -I$(INCLUDE_LOCATION) $(CPPFLAGS)
YDER_LOCATION=../src
INCLUDE_LOCATION=../include
LIBS=-lc -lorcania -lyder $(shell pkg-config --libs check) -L$(YDER_LOCATION)

all: test

clean:
	rm -f *.o yder_test valgrind.txt

libyder.so:
	cd $(YDER_LOCATION) && $(MAKE) debug

yder_test: yder_test.c
	$(CC) $(CFLAGS) yder_test.c -o yder_test $(LIBS)

test_yder_test: libyder.so yder_test
	LD_LIBRARY_PATH=$(YDER_LOCATION):${LD_LIBRARY_PATH} ./yder_test

test: test_yder_test

memcheck: yder_test
	LD_LIBRARY_PATH=$(YDER_LOCATION):${LD_LIBRARY_PATH} valgrind --tool=memcheck --leak-check=full --show-leak-kinds=all ./yder_test 2>valgrind.txt
