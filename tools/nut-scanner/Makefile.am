BUILT_SOURCES = nutscan-usb.h nutscan-snmp.h

nutscan-usb.h nutscan-snmp.h:
	cd ..; $(MAKE) $(AM_MAKEFLAGS) nut-scanner-deps

# Only build nut-scanner, and its library, if libltdl was found (required!)
if WITH_LIBLTDL
 bin_PROGRAMS = nut-scanner
 lib_LTLIBRARIES = libnutscan.la
endif
libnutscan_la_SOURCES = scan_nut.c scan_ipmi.c \
			nutscan-device.c nutscan-ip.c nutscan-display.c \
			nutscan-init.c  scan_usb.c scan_snmp.c scan_xml_http.c \
			scan_avahi.c scan_eaton_serial.c nutscan-serial.c \
			../../drivers/serial.c \
			../../drivers/bcmxcp_ser.c \
			../../common/common.c
libnutscan_la_LIBADD = $(NETLIBS) $(LIBLTDL_LIBS)
libnutscan_la_LDFLAGS = $(SERLIBS) -version-info 1:0:0
libnutscan_la_CFLAGS = -I$(top_srcdir)/clients -I$(top_srcdir)/include $(LIBLTDL_CFLAGS) -I$(top_srcdir)/drivers

nut_scanner_SOURCES = nut-scanner.c
nut_scanner_CFLAGS = -I$(top_srcdir)/clients -I$(top_srcdir)/include
nut_scanner_LDADD = libnutscan.la ../../common/libcommon.la

if WITH_SSL
  libnutscan_la_CFLAGS += $(LIBSSL_CFLAGS)
  libnutscan_la_LIBADD += $(LIBSSL_LIBS)
endif
if WITH_USB
  libnutscan_la_CFLAGS += $(LIBUSB_CFLAGS)
endif
if WITH_SNMP
  libnutscan_la_CFLAGS += $(LIBNETSNMP_CFLAGS)
endif
if WITH_NEON
  libnutscan_la_CFLAGS += $(LIBNEON_CFLAGS)
endif
if WITH_AVAHI
  libnutscan_la_CFLAGS += $(LIBAVAHI_CFLAGS)
endif
if WITH_IPMI
  libnutscan_la_CFLAGS += $(LIBIPMI_CFLAGS)
endif

dist_noinst_HEADERS = nutscan-usb.h nutscan-snmp.h

if WITH_DEV
 include_HEADERS = nut-scan.h nutscan-device.h nutscan-ip.h nutscan-init.h
else
 dist_noinst_HEADERS += nut-scan.h nutscan-device.h nutscan-ip.h nutscan-init.h nutscan-serial.h
endif

CLEANFILES = nutscan-usb.h nutscan-snmp.h

