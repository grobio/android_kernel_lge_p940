#
# Makefile fragment for Linux 2.6
# Broadcom DHD Driver
#
# Copyright (C) 2008, Broadcom Corporation
# All Rights Reserved.
# 
# THIS SOFTWARE IS OFFERED "AS IS", AND BROADCOM GRANTS NO WARRANTIES OF ANY
# KIND, EXPRESS OR IMPLIED, BY STATUTE, COMMUNICATION OR OTHERWISE. BROADCOM
# SPECIFICALLY DISCLAIMS ANY IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS
# FOR A SPECIFIC PURPOSE OR NONINFRINGEMENT CONCERNING THIS SOFTWARE.
#
# $Id: makefile.26,v 1.1.144.1 2008/05/07 22:53:44 Exp $

obj-$(CONFIG_BCM4330) += wireless.o

obj-$(CONFIG_BRCM_USE_STATIC_BUF) += brcm_static_buf.o

wireless-objs = \
	src/dhd/sys/dhd_linux.o \
	src/dhd/sys/dhd_linux_sched.o \
	src/shared/linux_osl.o \
	src/shared/bcmutils.o \
	src/dhd/sys/dhd_common.o \
	src/dhd/sys/dhd_custom_gpio.o \
	src/shared/siutils.o \
	src/shared/sbutils.o \
	src/shared/aiutils.o \
	src/shared/hndpmu.o \
	src/wl/sys/wl_iw.o \
	src/shared/bcmwifi.o \
	src/shared/bcmevent.o \
	src/dhd/sys/dhd_cdc.o \
	src/dhd/sys/dhd_sdio.o \
	src/bcmsdio/sys/bcmsdh_sdmmc.o \
	src/bcmsdio/sys/bcmsdh.o \
	src/bcmsdio/sys/bcmsdh_linux.o \
	src/bcmsdio/sys/bcmsdh_sdmmc_linux.o \

SRCROOT = drivers/net/wireless/bcm4330/src
EXTRA_CFLAGS = \
	-DLINUX \
	-DBCMDRIVER \
	-DBCMDONGLEHOST \
	-DDHDTHREAD \
	-DBCMWPA2 \
	-DBCMWAPI_WPI \
	-DUNRELEASEDCHIP \
	-DBDC \
	-DTOE \
	-DDHD_BCMEVENTS \
	-DSHOW_EVENTS \
	-DBCMSDIO \
	-DDHD_GPL \
	-DBCMLXSDMMC \
	-DBCMPLATFORM_BUS \
	-Wall -Wstrict-prototypes -Werror \
	-I$(SRCROOT) \
	-I$(SRCROOT)/include \
	-I$(SRCROOT)/shared \
	-I$(SRCROOT)/dhd/sys \
	-I$(SRCROOT)/dongle \
	-I$(SRCROOT)/wl/sys \
	\
	-DIOCTL_RESP_TIMEOUT=1000 \
	-DSDIO_VENDOR_ID_BROADCOM=0x2d0 \
	-DSDIO_DEVICE_ID_BROADCOM_4325=0x4c6 \
	-DSDIO_DEVICE_ID_BROADCOM_4330=0x4330 \
	-DANDROID_SPECIFIC \
	-DOEM_ANDROID -DEMBEDDED_PLATFORM \
	-DDHD_SCHED \
	-DOOB_INTR_ONLY	\
	-DHW_OOB \
	-DMMC_SDIO_ABORT \
	-DCSCAN \
#	-DSDIO_ISR_THREAD		#by sjpark 10-11-18
#	\
	-fshort-wchar \
	-D__KERNEL__ \
	-Iinclude \
	-Iinclude/asm/mach-default \
	-DBCMEMBEDIMAGE="<dongle/rte/wl/builds/4325b0/sdio-g-cdc-reclaim-idsup-wme/rtecdc.h>" \

ifeq ($(CONFIG_ARCH_MSM),y)
EXTRA_CFLAGS += -DCUSTOM_OOB_GPIO_NUM=$(CONFIG_BCM4330_GPIO_WL_HOSTWAKEUP)
EXTRA_CFLAGS += -DCUSTOMER_HW3
else
ifeq ($(CONFIG_ARCH_OMAP),y)
EXTRA_CFLAGS += -DCONFIG_MACH_MAHIMAHI
endif # ($(CONFIG_ARCH_OMAP),y)
endif # ($(CONFIG_ARCH_MSM),y)

ifeq ($(CONFIG_BRCM_LGE_WL_PKTFILTER),y)
EXTRA_CFLAGS += -DPKT_FILTER_SUPPORT
endif
ifeq ($(CONFIG_BRCM_LGE_WL_ARPOFFLOAD),y)
EXTRA_CFLAGS += -DARP_OFFLOAD_SUPPORT
endif
ifeq ($(CONFIG_BRCM_USE_SOFTAP),y)
EXTRA_CFLAGS += -DSOFTAP
endif

ifeq ($(CONFIG_BCM43xx_CCX),y)
# For CCKM support
EXTRA_CFLAGS += -DBCMCCX
#EXTRA_CFLAGS += -DBCMDBG_EVENT
#EXTRA_CFLAGS += -DSHOW_EVENTS
endif

ifeq ($(CONFIG_BCM4330_DEBUG),y)
EXTRA_CFLAGS += -DDHD_DEBUG -DSDTEST -DSRCBASE="\"$(SRCROOT)\""
endif

ifeq ($(CONFIG_BRCM_USE_STATIC_BUF),y)
EXTRA_CFLAGS += -DDHD_USE_STATIC_BUF
endif

# WLP2P CONFIG by yhcha_20110329
ifeq ($(CONFIG_BRCM_USE_WLP2P),y)
EXTRA_CFLAGS += -DWLP2P
endif

# WLBTAMP CONIFG by yhcha_20110329
ifeq ($(CONFIG_BRCM_USE_WLBTAMP),y)
EXTRA_CFLAGS += -DWLBTAMP
wireless-objs += src/dhd/sys/dhd_bta.o
endif

ifeq ($(CONFIG_BRCM_USE_SOFTAP),y)
EXTRA_CFLAGS += -DSOFTAP
endif

EXTRA_CFLAGS += -Dlinux
EXTRA_CFLAGS += -DDHD_SDALIGN=32 -DMAX_HDR_READ=32 -DDHD_FIRSTREAD=32

# Strip Module
EXTRA_LDFLAGS += --strip-debug
