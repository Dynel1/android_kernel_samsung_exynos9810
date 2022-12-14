LIBDIR := ../../../lib
BPFDIR := $(LIBDIR)/bpf
APIDIR := ../../../include/uapi
GENDIR := ../../../../include/generated
GENHDR := $(GENDIR)/autoconf.h

ifneq ($(wildcard $(GENHDR)),)
  GENFLAGS := -DHAVE_GENHDR
endif

CFLAGS += -Wall -O2 -I$(APIDIR) -I$(LIBDIR) -I$(GENDIR) $(GENFLAGS) -I../../../include
LDLIBS += -lcap -lelf

TEST_GEN_PROGS = test_verifier test_maps test_lru_map test_progs

TEST_GEN_FILES = test_pkt_access.o test_xdp.o test_l4lb.o

test_objs = test_tag test_lpm_map

TEST_PROGS := $(test_objs) test_kmod.sh

include ../lib.mk

BPFOBJ := $(OUTPUT)/libbpf.a

$(TEST_GEN_PROGS): $(BPFOBJ)

.PHONY: force

# force a rebuild of BPFOBJ when its dependencies are updated
force:

$(BPFOBJ): force
	$(MAKE) -C $(BPFDIR) OUTPUT=$(OUTPUT)/

CLANG ?= clang

%.o: %.c
	$(CLANG) -I../../../include/uapi -I../../../../samples/bpf/ \
		-D__x86_64__ -Wno-compare-distinct-pointer-types \
		-O2 -target bpf -c $< -o $@
