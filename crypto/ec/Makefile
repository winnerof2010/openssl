#
# crypto/ec/Makefile
#

DIR=	ec
TOP=	../..
CC=	cc
INCLUDES= -I.. -I$(TOP) -I../include -I../../include
CFLAG=-g
MAKEFILE=	Makefile
AR=		ar r

CFLAGS= $(INCLUDES) $(CFLAG)
ASFLAGS= $(INCLUDES) $(ASFLAG)
AFLAGS= $(ASFLAGS)

GENERAL=Makefile

LIB=$(TOP)/libcrypto.a
LIBSRC=	ec_lib.c ecp_smpl.c ecp_mont.c ecp_nist.c ec_cvt.c ec_mult.c\
	ec_err.c ec_curve.c ec_check.c ec_print.c ec_asn1.c ec_key.c\
	ec2_smpl.c ec2_mult.c ec_ameth.c ec_pmeth.c eck_prn.c \
	ecp_nistp224.c ecp_nistp256.c ecp_nistp521.c ecp_nistputil.c \
	ecp_oct.c ec2_oct.c ec_oct.c ec_kmeth.c ecdh_ossl.c ecdh_kdf.c \
	ecdsa_ossl.c ecdsa_sign.c ecdsa_vrf.c

LIBOBJ=	ec_lib.o ecp_smpl.o ecp_mont.o ecp_nist.o ec_cvt.o ec_mult.o\
	ec_err.o ec_curve.o ec_check.o ec_print.o ec_asn1.o ec_key.o\
	ec2_smpl.o ec2_mult.o ec_ameth.o ec_pmeth.o eck_prn.o \
	ecp_nistp224.o ecp_nistp256.o ecp_nistp521.o ecp_nistputil.o \
	ecp_oct.o ec2_oct.o ec_oct.o ec_kmeth.o ecdh_ossl.o ecdh_kdf.o \
	ecdsa_ossl.o ecdsa_sign.o ecdsa_vrf.o $(EC_ASM)

SRC= $(LIBSRC)

HEADER=	ec_lcl.h

ALL=    $(GENERAL) $(SRC) $(HEADER)

top:
	(cd ../..; $(MAKE) DIRS=crypto SDIRS=$(DIR) sub_all)

all:	lib

lib:	$(LIBOBJ)
	$(AR) $(LIB) $(LIBOBJ)
	$(RANLIB) $(LIB) || echo Never mind.
	@touch lib

ecp_nistz256-x86.s:	asm/ecp_nistz256-x86.pl
	$(PERL) asm/ecp_nistz256-x86.pl $(PERLASM_SCHEME) $(CFLAGS) $(PROCESSOR) > $@

ecp_nistz256-x86_64.s: asm/ecp_nistz256-x86_64.pl
	$(PERL) asm/ecp_nistz256-x86_64.pl $(PERLASM_SCHEME) > $@

ecp_nistz256-avx2.s:   asm/ecp_nistz256-avx2.pl
	$(PERL) asm/ecp_nistz256-avx2.pl $(PERLASM_SCHEME) > $@

ecp_nistz256-sparcv9.S:	asm/ecp_nistz256-sparcv9.pl
	$(PERL) asm/ecp_nistz256-sparcv9.pl $(CFLAGS) > $@

ecp_nistz256-%.S:	asm/ecp_nistz256-%.pl;  $(PERL) $< $(PERLASM_SCHEME) $@
ecp_nistz256-armv4.o:	ecp_nistz256-armv4.S
ecp_nistz256-armv8.o:	ecp_nistz256-armv8.S

files:
	$(PERL) $(TOP)/util/files.pl Makefile >> $(TOP)/MINFO

tags:
	ctags $(SRC)

tests:

lint:
	lint -DLINT $(INCLUDES) $(SRC)>fluff

update: depend

depend:
	@[ -n "$(MAKEDEPEND)" ] # should be set by upper Makefile...
	$(MAKEDEPEND) -- $(CFLAG) $(INCLUDES) $(DEPFLAG) -- $(PROGS) $(LIBSRC)

dclean:
	$(PERL) -pe 'if (/^# DO NOT DELETE THIS LINE/) {print; exit(0);}' $(MAKEFILE) >Makefile.new
	mv -f Makefile.new $(MAKEFILE)

clean:
	rm -f *.s *.o */*.o *.obj lib tags core .pure .nfs* *.old *.bak fluff

# DO NOT DELETE THIS LINE -- make depend depends on it.

ec2_mult.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec2_mult.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ec2_mult.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec2_mult.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ec2_mult.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ec2_mult.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec2_mult.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec2_mult.o: ../../include/openssl/symhacks.h ../include/internal/bn_int.h
ec2_mult.o: ec2_mult.c ec_lcl.h
ec2_oct.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec2_oct.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ec2_oct.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec2_oct.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ec2_oct.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ec2_oct.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec2_oct.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec2_oct.o: ../../include/openssl/symhacks.h ec2_oct.c ec_lcl.h
ec2_smpl.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec2_smpl.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ec2_smpl.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec2_smpl.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ec2_smpl.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ec2_smpl.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec2_smpl.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec2_smpl.o: ../../include/openssl/symhacks.h ../include/internal/bn_int.h
ec2_smpl.o: ec2_smpl.c ec_lcl.h
ec_ameth.o: ../../e_os.h ../../include/openssl/asn1.h
ec_ameth.o: ../../include/openssl/asn1t.h ../../include/openssl/bio.h
ec_ameth.o: ../../include/openssl/bn.h ../../include/openssl/buffer.h
ec_ameth.o: ../../include/openssl/cms.h ../../include/openssl/crypto.h
ec_ameth.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec_ameth.o: ../../include/openssl/err.h ../../include/openssl/evp.h
ec_ameth.o: ../../include/openssl/lhash.h ../../include/openssl/obj_mac.h
ec_ameth.o: ../../include/openssl/objects.h ../../include/openssl/opensslconf.h
ec_ameth.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_ameth.o: ../../include/openssl/pkcs7.h ../../include/openssl/safestack.h
ec_ameth.o: ../../include/openssl/sha.h ../../include/openssl/stack.h
ec_ameth.o: ../../include/openssl/symhacks.h ../../include/openssl/x509.h
ec_ameth.o: ../../include/openssl/x509_vfy.h ../include/internal/asn1_int.h
ec_ameth.o: ../include/internal/cryptlib.h ec_ameth.c
ec_asn1.o: ../../include/openssl/asn1.h ../../include/openssl/asn1t.h
ec_asn1.o: ../../include/openssl/bio.h ../../include/openssl/bn.h
ec_asn1.o: ../../include/openssl/crypto.h ../../include/openssl/e_os2.h
ec_asn1.o: ../../include/openssl/ec.h ../../include/openssl/err.h
ec_asn1.o: ../../include/openssl/lhash.h ../../include/openssl/obj_mac.h
ec_asn1.o: ../../include/openssl/objects.h ../../include/openssl/opensslconf.h
ec_asn1.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_asn1.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec_asn1.o: ../../include/openssl/symhacks.h ec_asn1.c ec_lcl.h
ec_check.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec_check.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ec_check.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec_check.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ec_check.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ec_check.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_check.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec_check.o: ../../include/openssl/symhacks.h ec_check.c ec_lcl.h
ec_curve.o: ../../e_os.h ../../include/openssl/asn1.h
ec_curve.o: ../../include/openssl/bio.h ../../include/openssl/bn.h
ec_curve.o: ../../include/openssl/crypto.h ../../include/openssl/e_os2.h
ec_curve.o: ../../include/openssl/ec.h ../../include/openssl/err.h
ec_curve.o: ../../include/openssl/lhash.h ../../include/openssl/obj_mac.h
ec_curve.o: ../../include/openssl/opensslconf.h
ec_curve.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_curve.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec_curve.o: ../../include/openssl/symhacks.h ec_curve.c ec_lcl.h
ec_cvt.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec_cvt.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ec_cvt.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec_cvt.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ec_cvt.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ec_cvt.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_cvt.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec_cvt.o: ../../include/openssl/symhacks.h ec_cvt.c ec_lcl.h
ec_err.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec_err.o: ../../include/openssl/crypto.h ../../include/openssl/e_os2.h
ec_err.o: ../../include/openssl/ec.h ../../include/openssl/err.h
ec_err.o: ../../include/openssl/lhash.h ../../include/openssl/opensslconf.h
ec_err.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_err.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec_err.o: ../../include/openssl/symhacks.h ec_err.c
ec_key.o: ../../e_os.h ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec_key.o: ../../include/openssl/bn.h ../../include/openssl/buffer.h
ec_key.o: ../../include/openssl/crypto.h ../../include/openssl/e_os2.h
ec_key.o: ../../include/openssl/ec.h ../../include/openssl/engine.h
ec_key.o: ../../include/openssl/err.h ../../include/openssl/evp.h
ec_key.o: ../../include/openssl/lhash.h ../../include/openssl/obj_mac.h
ec_key.o: ../../include/openssl/objects.h ../../include/openssl/opensslconf.h
ec_key.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_key.o: ../../include/openssl/pkcs7.h ../../include/openssl/safestack.h
ec_key.o: ../../include/openssl/sha.h ../../include/openssl/stack.h
ec_key.o: ../../include/openssl/symhacks.h ../../include/openssl/x509.h
ec_key.o: ../../include/openssl/x509_vfy.h ../include/internal/cryptlib.h
ec_key.o: ec_key.c ec_lcl.h
ec_kmeth.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec_kmeth.o: ../../include/openssl/bn.h ../../include/openssl/buffer.h
ec_kmeth.o: ../../include/openssl/crypto.h ../../include/openssl/e_os2.h
ec_kmeth.o: ../../include/openssl/ec.h ../../include/openssl/engine.h
ec_kmeth.o: ../../include/openssl/err.h ../../include/openssl/evp.h
ec_kmeth.o: ../../include/openssl/lhash.h ../../include/openssl/obj_mac.h
ec_kmeth.o: ../../include/openssl/objects.h ../../include/openssl/opensslconf.h
ec_kmeth.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_kmeth.o: ../../include/openssl/pkcs7.h ../../include/openssl/safestack.h
ec_kmeth.o: ../../include/openssl/sha.h ../../include/openssl/stack.h
ec_kmeth.o: ../../include/openssl/symhacks.h ../../include/openssl/x509.h
ec_kmeth.o: ../../include/openssl/x509_vfy.h ec_kmeth.c ec_lcl.h
ec_lib.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec_lib.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ec_lib.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec_lib.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ec_lib.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ec_lib.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_lib.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec_lib.o: ../../include/openssl/symhacks.h ec_lcl.h ec_lib.c
ec_mult.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec_mult.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ec_mult.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec_mult.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ec_mult.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ec_mult.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_mult.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec_mult.o: ../../include/openssl/symhacks.h ../include/internal/bn_int.h
ec_mult.o: ec_lcl.h ec_mult.c
ec_oct.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec_oct.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ec_oct.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec_oct.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ec_oct.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ec_oct.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_oct.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec_oct.o: ../../include/openssl/symhacks.h ec_lcl.h ec_oct.c
ec_pmeth.o: ../../e_os.h ../../include/openssl/asn1.h
ec_pmeth.o: ../../include/openssl/asn1t.h ../../include/openssl/bio.h
ec_pmeth.o: ../../include/openssl/bn.h ../../include/openssl/buffer.h
ec_pmeth.o: ../../include/openssl/crypto.h ../../include/openssl/e_os2.h
ec_pmeth.o: ../../include/openssl/ec.h ../../include/openssl/err.h
ec_pmeth.o: ../../include/openssl/evp.h ../../include/openssl/lhash.h
ec_pmeth.o: ../../include/openssl/obj_mac.h ../../include/openssl/objects.h
ec_pmeth.o: ../../include/openssl/opensslconf.h
ec_pmeth.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_pmeth.o: ../../include/openssl/pkcs7.h ../../include/openssl/safestack.h
ec_pmeth.o: ../../include/openssl/sha.h ../../include/openssl/stack.h
ec_pmeth.o: ../../include/openssl/symhacks.h ../../include/openssl/x509.h
ec_pmeth.o: ../../include/openssl/x509_vfy.h ../include/internal/cryptlib.h
ec_pmeth.o: ../include/internal/evp_int.h ec_lcl.h ec_pmeth.c
ec_print.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ec_print.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ec_print.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ec_print.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ec_print.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ec_print.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ec_print.o: ../../include/openssl/symhacks.h ec_lcl.h ec_print.c
ecdh_kdf.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ecdh_kdf.o: ../../include/openssl/crypto.h ../../include/openssl/e_os2.h
ecdh_kdf.o: ../../include/openssl/ec.h ../../include/openssl/evp.h
ecdh_kdf.o: ../../include/openssl/obj_mac.h ../../include/openssl/objects.h
ecdh_kdf.o: ../../include/openssl/opensslconf.h
ecdh_kdf.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ecdh_kdf.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ecdh_kdf.o: ../../include/openssl/symhacks.h ecdh_kdf.c
ecdh_ossl.o: ../../e_os.h ../../include/openssl/asn1.h
ecdh_ossl.o: ../../include/openssl/bio.h ../../include/openssl/bn.h
ecdh_ossl.o: ../../include/openssl/buffer.h ../../include/openssl/crypto.h
ecdh_ossl.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ecdh_ossl.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ecdh_ossl.o: ../../include/openssl/obj_mac.h ../../include/openssl/objects.h
ecdh_ossl.o: ../../include/openssl/opensslconf.h
ecdh_ossl.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ecdh_ossl.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ecdh_ossl.o: ../../include/openssl/symhacks.h ../include/internal/cryptlib.h
ecdh_ossl.o: ec_lcl.h ecdh_ossl.c
ecdsa_ossl.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ecdsa_ossl.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ecdsa_ossl.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ecdsa_ossl.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ecdsa_ossl.o: ../../include/openssl/obj_mac.h
ecdsa_ossl.o: ../../include/openssl/opensslconf.h
ecdsa_ossl.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ecdsa_ossl.o: ../../include/openssl/rand.h ../../include/openssl/safestack.h
ecdsa_ossl.o: ../../include/openssl/stack.h ../../include/openssl/symhacks.h
ecdsa_ossl.o: ec_lcl.h ecdsa_ossl.c
ecdsa_sign.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ecdsa_sign.o: ../../include/openssl/bn.h ../../include/openssl/buffer.h
ecdsa_sign.o: ../../include/openssl/crypto.h ../../include/openssl/e_os2.h
ecdsa_sign.o: ../../include/openssl/ec.h ../../include/openssl/engine.h
ecdsa_sign.o: ../../include/openssl/err.h ../../include/openssl/evp.h
ecdsa_sign.o: ../../include/openssl/lhash.h ../../include/openssl/obj_mac.h
ecdsa_sign.o: ../../include/openssl/objects.h
ecdsa_sign.o: ../../include/openssl/opensslconf.h
ecdsa_sign.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ecdsa_sign.o: ../../include/openssl/pkcs7.h ../../include/openssl/rand.h
ecdsa_sign.o: ../../include/openssl/safestack.h ../../include/openssl/sha.h
ecdsa_sign.o: ../../include/openssl/stack.h ../../include/openssl/symhacks.h
ecdsa_sign.o: ../../include/openssl/x509.h ../../include/openssl/x509_vfy.h
ecdsa_sign.o: ec_lcl.h ecdsa_sign.c
ecdsa_vrf.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ecdsa_vrf.o: ../../include/openssl/bn.h ../../include/openssl/buffer.h
ecdsa_vrf.o: ../../include/openssl/crypto.h ../../include/openssl/e_os2.h
ecdsa_vrf.o: ../../include/openssl/ec.h ../../include/openssl/engine.h
ecdsa_vrf.o: ../../include/openssl/err.h ../../include/openssl/evp.h
ecdsa_vrf.o: ../../include/openssl/lhash.h ../../include/openssl/obj_mac.h
ecdsa_vrf.o: ../../include/openssl/objects.h
ecdsa_vrf.o: ../../include/openssl/opensslconf.h
ecdsa_vrf.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ecdsa_vrf.o: ../../include/openssl/pkcs7.h ../../include/openssl/safestack.h
ecdsa_vrf.o: ../../include/openssl/sha.h ../../include/openssl/stack.h
ecdsa_vrf.o: ../../include/openssl/symhacks.h ../../include/openssl/x509.h
ecdsa_vrf.o: ../../include/openssl/x509_vfy.h ec_lcl.h ecdsa_vrf.c
eck_prn.o: ../../e_os.h ../../include/openssl/asn1.h
eck_prn.o: ../../include/openssl/bio.h ../../include/openssl/bn.h
eck_prn.o: ../../include/openssl/buffer.h ../../include/openssl/crypto.h
eck_prn.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
eck_prn.o: ../../include/openssl/err.h ../../include/openssl/evp.h
eck_prn.o: ../../include/openssl/lhash.h ../../include/openssl/obj_mac.h
eck_prn.o: ../../include/openssl/objects.h ../../include/openssl/opensslconf.h
eck_prn.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
eck_prn.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
eck_prn.o: ../../include/openssl/symhacks.h ../include/internal/cryptlib.h
eck_prn.o: eck_prn.c
ecp_mont.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ecp_mont.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ecp_mont.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ecp_mont.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ecp_mont.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ecp_mont.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ecp_mont.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ecp_mont.o: ../../include/openssl/symhacks.h ec_lcl.h ecp_mont.c
ecp_nist.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ecp_nist.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ecp_nist.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ecp_nist.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ecp_nist.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ecp_nist.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ecp_nist.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ecp_nist.o: ../../include/openssl/symhacks.h ec_lcl.h ecp_nist.c
ecp_nistp224.o: ../../include/openssl/opensslconf.h ecp_nistp224.c
ecp_nistp256.o: ../../include/openssl/opensslconf.h ecp_nistp256.c
ecp_nistp521.o: ../../include/openssl/opensslconf.h ecp_nistp521.c
ecp_nistputil.o: ../../include/openssl/opensslconf.h ecp_nistputil.c
ecp_oct.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ecp_oct.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ecp_oct.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ecp_oct.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ecp_oct.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ecp_oct.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ecp_oct.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ecp_oct.o: ../../include/openssl/symhacks.h ec_lcl.h ecp_oct.c
ecp_smpl.o: ../../include/openssl/asn1.h ../../include/openssl/bio.h
ecp_smpl.o: ../../include/openssl/bn.h ../../include/openssl/crypto.h
ecp_smpl.o: ../../include/openssl/e_os2.h ../../include/openssl/ec.h
ecp_smpl.o: ../../include/openssl/err.h ../../include/openssl/lhash.h
ecp_smpl.o: ../../include/openssl/obj_mac.h ../../include/openssl/opensslconf.h
ecp_smpl.o: ../../include/openssl/opensslv.h ../../include/openssl/ossl_typ.h
ecp_smpl.o: ../../include/openssl/safestack.h ../../include/openssl/stack.h
ecp_smpl.o: ../../include/openssl/symhacks.h ec_lcl.h ecp_smpl.c
