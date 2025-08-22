TARGET = makeip

VERSION = 2.0.0

OBJECTS = utils.o vector.o crc.o mr.o field.o ip.o main.o

CC = gcc
STRIP = strip
uname_s := $(shell uname -s)
uname_r := $(shell uname -r)
uname_m := $(shell uname -m)
ifeq ($(uname_s),Darwin)
HOMEBREW:= $(shell command -v homebrew)
MACPORT := $(shell command -v port)
  ifeq ($(uname_m),arm64)
    $(info Fixing up MacOS arm64 environment variables)
ifdef HOMEBREW
CFLAGS = -O2 -Wall -DMAKEIP_VERSION=\"$(VERSION)\" -I/opt/homebrew/include
LDFLAGS = -L/opt/homebrew/lib -lpng -lz
endif
ifdef MACPORT
MACPORT_BASE=$(shell command -v port|sed s\#/bin\/port\#\#g)
CFLAGS = -O2 -Wall -DMAKEIP_VERSION=\"$(VERSION)\" -I$(MACPORT_BASE)/include
LDFLAGS = -L$(MACPORT_BASE)/lib -lpng -lz
endif
  endif
  ifeq ($(uname_m),x86_64)
    $(info Fixing up MacOS x86_64 environment variables)
ifdef HOMEBREW
CFLAGS = -O2 -Wall -DMAKEIP_VERSION=\"$(VERSION)\" -I/usr/local/include
LDFLAGS = -L/usr/local/lib -lpng -lz
endif
ifdef MACPORT
MACPORT_BASE=$(shell command -v port|sed s\#/bin\/port\#\#g)
CFLAGS = -O2 -Wall -DMAKEIP_VERSION=\"$(VERSION)\" -I$(MACPORT_BASE)/include
LDFLAGS = -L$(MACPORT_BASE)/lib -lpng -lz
endif
  endif
else
CFLAGS = -O2 -Wall -DMAKEIP_VERSION=\"$(VERSION)\" -I/usr/local/include
LDFLAGS = -L/usr/local/lib -lpng -lz
endif

INSTALLDIR = ..

EXECUTABLEEXTENSION =
ifeq ($(shell echo $(OS)),Windows_NT)
  EXECUTABLEEXTENSION := .exe
endif

OUTPUT = $(TARGET)$(EXECUTABLEEXTENSION)

all: $(TARGET)

$(TARGET): $(OBJECTS)
	$(CC) -o $(OUTPUT) $(CFLAGS) $(OBJECTS) $(LDFLAGS)
	$(STRIP) $(OUTPUT)

install:
	mkdir -p $(INSTALLDIR)
	mv $(OUTPUT) $(INSTALLDIR)

.PHONY: clean
clean:
	-rm -f $(OUTPUT) *.o
