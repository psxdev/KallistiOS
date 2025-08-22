
# Makefile stolen from the kmgenc program.
uname_s := $(shell uname -s)
uname_r := $(shell uname -r)
uname_m := $(shell uname -m)
ifeq ($(uname_s),Darwin)
HOMEBREW:= $(shell command -v homebrew)
MACPORT := $(shell command -v port)
  ifeq ($(uname_m),arm64)
    $(info Fixing up MacOS arm64 environment variables)
ifdef HOMEBREW
CFLAGS = -O2 -Wall -I/opt/homebrew/include
LDFLAGS = -s -lpng -ljpeg -lm -lz -L/opt/homebrew/lib
endif
ifdef MACPORT
MACPORT_BASE=$(shell command -v port|sed s\#/bin\/port\#\#g)
CFLAGS = -O2 -Wall -I$(MACPORT_BASE)/include
LDFLAGS = -s -lpng -ljpeg -lm -lz -L$(MACPORT_BASE)/lib
endif
  endif
  ifeq ($(uname_m),x86_64)
    $(info Fixing up MacOS x86_64 environment variables)
ifdef HOMEBREW
CFLAGS = -O2 -Wall -I/usr/local/include
LDFLAGS = -s -lpng -ljpeg -lm -lz -L/usr/local/lib
endif
ifdef MACPORT
MACPORT_BASE=$(shell command -v port|sed s\#/bin\/port\#\#g)
CFLAGS = -O2 -Wall -I$(MACPORT_BASE)/include
LDFLAGS = -s -lpng -ljpeg -lm -lz -L$(MACPORT_BASE)/lib
endif
  endif
else
CFLAGS = -O2 -Wall -I/usr/local/include
LDFLAGS = -s -lpng -ljpeg -lm -lz -L/usr/local/lib
endif

all: dcbumpgen

dcbumpgen: dcbumpgen.o get_image.o get_image_jpg.o get_image_png.o readpng.o
	$(CC) -o $@ $+ $(LDFLAGS)

clean:
	rm -f dcbumpgen *.o

