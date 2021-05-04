ifneq (, $(shell command -v opam))
PKG_CONFIG_PATH ?= $(shell opam var prefix)/lib/pkgconfig
endif

EXISTS := $(shell PKG_CONFIG_PATH=$(PKG_CONFIG_PATH) pkg-config --exists ocaml-freestanding; echo $$?)

.PHONY: all clean
all: libprovision_freestanding_stubs.a

ifeq ($(EXISTS), 1)
libprovision_freestanding_stubs.a:
	touch $@
else
CC ?= cc
FREESTANDING_CFLAGS := $(shell PKG_CONFIG_PATH=$(PKG_CONFIG_PATH) pkg-config --cflags ocaml-freestanding)
CFLAGS := $(FREESTANDING_CFLAGS)

OBJS=load.o

libprovision_freestanding_stubs.a: $(OBJS)
	$(AR) r $@ $^
endif

clean:
	$(RM) $(OBJS) libprovision_freestanding_stubs.a
