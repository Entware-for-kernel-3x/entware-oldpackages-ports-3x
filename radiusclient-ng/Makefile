#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# Abandoned in 2009

include $(TOPDIR)/rules.mk

PKG_NAME:=radiusclient-ng
PKG_VERSION:=0.5.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION).orig.tar.gz
PKG_SOURCE_URL:=http://ftp.debian.org/debian/pool/main/r/$(PKG_NAME)
PKG_HASH:=282a9f1355f190efbb06c0d7c4e062eaa652caf342ed3ad361ac595f72f09f14

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/radiusclient-ng/Default
  URL:=http://developer.berlios.de/projects/radiusclient-ng/
endef

define Package/radiusclient-ng/Default/description
 Purpose of this project is to build a portable, easy-to-use and
 standard compliant library suitable for developing free and commercial
 software that need support for RADIUS protocol (RFCs 2128 and 2139).
endef

define Package/libradiusclient-ng
$(call Package/radiusclient-ng/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=RADIUS client library
endef

define Package/libradiusclient-ng/description
$(call Package/radiusclient-ng/Default/description)
 This package contains shared libraries, needed by other programs.
endef

define Package/libradiusclient-ng/conffiles
/opt/etc/radiusclient-ng/issue
/opt/etc/radiusclient-ng/port-id-map
/opt/etc/radiusclient-ng/radiusclient.conf
/opt/etc/radiusclient-ng/servers
endef

define Package/radiusclient-ng
  $(call Package/radiusclient-ng/Default)
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libradiusclient-ng
  TITLE:=RADIUS client
endef

define Package/radiusclient-ng/description
$(call Package/radiusclient-ng/Default/description)
 This package contains a RADIUS client.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

#define Build/InstallDev
#	$(INSTALL_DIR) $(1)/opt/include
#	$(CP) $(PKG_INSTALL_DIR)/opt/include/radiusclient-ng.h $(1)/opt/include/
#	$(INSTALL_DIR) $(1)/opt/lib/
#	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libradiusclient-ng.{a,so}* $(1)/opt/lib/
#endef

define Package/libradiusclient-ng/install
	$(INSTALL_DIR) $(1)/opt/etc
	$(CP) $(PKG_INSTALL_DIR)/opt/etc/radiusclient-ng $(1)/opt/etc/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libradiusclient-ng.so.* $(1)/opt/lib/
endef

define Package/radiusclient-ng/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/rad{acct,iusclient,login,status} $(1)/opt/sbin/
endef

$(eval $(call BuildPackage,libradiusclient-ng))
$(eval $(call BuildPackage,radiusclient-ng))
