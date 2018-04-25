#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openc2x
PKG_VERSION:=v1.2
PKG_RELEASE:=1


PKG_SOURCE_PROTO:=git
PKG_SOURCE:=$(PKG_NAME)-v$(PKG_VERSION).tar.xz
#PKG_MIRROR_HASH:=b2d96c36682391f45c63b21a91fbe77a969a7b362417c851dd0091a06fcc74d9
PKG_SOURCE_URL:=https://github.com/sitaramc/gitolite.git
PKG_SOURCE_VERSION:=11b14199f9cc39b51f9e1c76a5998263fbf0e82f
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_BUILD_DEPENDS:=asn1c/host autoconf-archive


PKG_MAINTAINER:=Hal Martin 
PKG_LICENSE:=GPL-2
PKG_CONFIG_DEPENDS:=
PKG_USE_MIPS16:=0 
#PKG_SOURCE_URL:=http://www.ccs-labs.org/software/openc2x/
#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_HASH:=a5bf011250d4decc276f46c59facd6845a9657aa0283d0beb777a9d52127af0c
#MAKE_PATH:=Open
include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk





#TARGET_LDFLAGS+= \
#  -Wl,-rpath-link=$(STAGING_DIR)/usr/lib \
#  -Wl,-rpath-link=$(STAGING_DIR)/usr/lib/libconfig/lib \
#  -Wl,-rpath-link=$(STAGING_DIR)/usr/lib/sqlite/lib

define Package/openc2x
  SECTION:=utils
  CATEGORY:=Utilities
  PKG_BUILD_DEPENDS := cppzmq asn1c
  DEPENDS:=+boost +boost-system +boost-thread +protobuf +libstdzmq +libnl-tiny +gpsd +libgps +libsqlite3 +libuci
  TITLE:=openc2x
  URL:=http://www.ccs-labs.org/software/openc2x/
  MENU:=1
endef
#TARGET_CFLAGS += -ggdb3 \
#	-g 
	
TARGET_CXXFLAGS += \
	-I$(STAGING_DIR)/usr/include/libnl-tiny \
	-I$(STAGING_DIR)/usr/include \
#	-ggdb3 \
#	-g

CMAKE_OPTIONS += \
	-DLIBNL_LIBS=-lnl-tiny \
#	-DDEBUG=1

define Package/openc2x/description
Vehicular networking is at the corner from early research to final deployment. This phase requires more field testing and real-world experimentation. Most Field Operational Tests (FOTs) are based on proprietary commercial hardware that only allows for marginal modifications of the protocol stack. Furthermore, the roll-out of updated implementations for new or changing protocol standards often takes a prohibitively long time.

We developed one of the first complete Open Source experimental and prototyping platform for vehicular networking solutions. Our system supports most of the ETSI ITS-G5 features and runs on standard Linux. New protocol features and updates could now easily be done by and shared with the vehicular networking R&D community. 
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	#mkdir -p $(PKG_BUILD_DIR)
	#$(CP) $(PKG_BUILD_DIR)/../OpenC2X/* $(PKG_BUILD_DIR)/
endef

#define Build/Configure
#endef

#define Build/Compile
#	$(MAKE) -C $(PKG_BUILD_DIR) $(TARGET_CONFIGURE_OPTS)
#endef
	#$(INSTALL_DIR) $(1)/etc/config
	#$(INSTALL_CONF) $(PKG_BUILD_DIR)/l $(1)/etc/config/l

define Package/openc2x/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/usr/share/openc2x/gpsdata
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	#$(INSTALL_BIN) $(PKG_BUILD_DIR)/cam/src/cam $(1)/usr/bin/
	#$(INSTALL_BIN) $(PKG_BUILD_DIR)/dcc/src/dcc $(1)/usr/bin/
	#$(INSTALL_BIN) $(PKG_BUILD_DIR)/denm/src/denm $(1)/usr/bin/
	#$(INSTALL_BIN) $(PKG_BUILD_DIR)/denmApp/src/denmApp $(1)/usr/bin/
	#$(INSTALL_BIN) $(PKG_BUILD_DIR)/gps/src/gpsService $(1)/usr/bin/
	#$(INSTALL_BIN) $(PKG_BUILD_DIR)/httpServer/src/httpServer $(1)/usr/bin/
	#$(INSTALL_BIN) $(PKG_BUILD_DIR)/ldm/src/ldm $(1)/usr/bin/
	#$(INSTALL_BIN) $(PKG_BUILD_DIR)/obd2/src/obd2 $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/etc/config/* $(1)/etc/config/
	$(CP) files/etc/init.d/openc2x $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/etc/uci-defaults/uci-defaults-openc2x $(1)/etc/uci-defaults/openc2x
endef

$(eval $(call BuildPackage,openc2x))
