#
# Copyright (C) 2011-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# The newer revs installed as a python package and requires 'setuptools>=0.6.39

include $(TOPDIR)/rules.mk

PKG_NAME:=pyload
PKG_VERSION:=0.4.9-20161208
PKG_REV:=ea099613e81b08a693b1f601eb5b38b753bd575e
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/pyload/pyload
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/pyload
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+python-curl +python-sqlite3
  TITLE:=A fast, lightweight and full featured download manager
  URL:=http://pyload.org
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/pyload/postinst
#!/bin/sh
cat << EOF
Please install optional pyload dependencies first.

* for SSL connection with WebUI:
opkg install python-pyopenssl openssl-util

* for several hosters, ClickNLoad feature:
opkg install duktape

* for captcha recognition for a small amount of plugins:
opkg install pillow tesseract

* for RSDF/CCF/DLC support to decrypt container files:
opkg install python-crypto

* for using ExtractArchive plugin:
opkg install unrar unzip

And only then configure pyload by
pyload --configdir=/opt/var/pyload
EOF
endef

define Package/pyload/install
	$(INSTALL_DIR) $(1)/opt/share/pyload
	$(CP) $(PKG_BUILD_DIR)/{icons,locale,module,scripts,tests,*.py} \
	    $(1)/opt/share/pyload
	$(INSTALL_DIR) $(1)/opt/bin
	$(LN) ../share/pyload/pyLoadCore.py $(1)/opt/bin/pyload
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S51pyload $(1)/opt/etc/init.d
	$(SED) 's,/usr/bin/env python,/opt/bin/python,g' \
		$(1)/opt/share/pyload/pyLoad{Cli,Gui,Core}.py
endef

$(eval $(call BuildPackage,pyload))
