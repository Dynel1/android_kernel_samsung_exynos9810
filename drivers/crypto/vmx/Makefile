obj-$(CONFIG_CRYPTO_DEV_VMX_ENCRYPT) += vmx-crypto.o
vmx-crypto-objs := vmx.o aesp8-ppc.o ghashp8-ppc.o aes.o aes_cbc.o aes_ctr.o aes_xts.o ghash.o

ifeq ($(CONFIG_CPU_LITTLE_ENDIAN),y)
override flavour := linux-ppc64le
else
override flavour := linux-ppc64
endif

quiet_cmd_perl = PERL $@
      cmd_perl = $(PERL) $(<) $(flavour) > $(@)

targets += aesp8-ppc.S ghashp8-ppc.S

$(obj)/aesp8-ppc.S: $(src)/aesp8-ppc.pl FORCE
	$(call if_changed,perl)
  
$(obj)/ghashp8-ppc.S: $(src)/ghashp8-ppc.pl FORCE
	$(call if_changed,perl)

clean-files := aesp8-ppc.S ghashp8-ppc.S
