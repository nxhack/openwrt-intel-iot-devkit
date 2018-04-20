#
# Copyright (C) 2015-2018 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libmraa
PKG_VERSION:=1.9.0
PKG_RELEASE=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/intel-iot-devkit/mraa.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=fbb7d9232067eac3f4508a37a8f7ea0c4fcebacb
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=104420fc72b80bb6493ddc53014597abc0d455f965ebd6fc7f9be26aa5685ffd

PKG_BUILD_DEPENDS:=swig/host node/host
CMAKE_INSTALL:=1
PKG_USE_MIPS16:=0

PKG_MAINTAINER:=John Crispin <blogic@openwrt.org>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
include $(TOPDIR)/feeds/packages/lang/python/python-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

CMAKE_OPTIONS=-DBUILDARCH=$(CONFIG_ARCH) \
	-DENABLEEXAMPLES=0 \
	-DNODE_EXECUTABLE=$(STAGING_DIR_HOSTPKG)/bin/node \
	-DSWIG_DIR=$(STAGING_DIR_HOSTPKG)/bin

TARGET_CFLAGS+=-I$(STAGING_DIR)/usr/include/node

define Package/libmraa/Default
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Intel IoT lowlevel IO library
  URL:=https://github.com/intel-iot-devkit/mraa
endef

define Package/libmraa/Default/description
  Libmraa is a C/C++ library with bindings to Java, Python and JavaScript to interface with the IO on Galileo, Edison & other platforms, with a structured and sane API where port names/numbering matches the board that you are on. Use of libmraa does not tie you to specific hardware with board detection done at runtime you can create portable code that will work across the supported platforms.
endef

define Package/libmraa
  $(call Package/libmraa/Default)
  TITLE:=Intel IoT lowlevel IO C library
  DEPENDS:=+libstdcpp +libjson-c
endef

define Package/libmraa-node
  $(call Package/libmraa/Default)
  TITLE:=Intel IoT lowlevel IO Node.js library
  DEPENDS:=+libmraa +node
endef

define Package/libmraa-python
  $(call Package/libmraa/Default)
  TITLE:=Intel IoT lowlevel IO Python library
  DEPENDS:=+libmraa +python-light
endef

define Package/libmraa-python3
  $(call Package/libmraa/Default)
  TITLE:=Intel IoT lowlevel IO Python3 library
  DEPENDS:=+libmraa +python3-light
endef

define Package/libmraa/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/libmraa.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/mraa-* $(1)/usr/bin/
endef

define Package/libmraa-node/install
	$(INSTALL_DIR) $(1)/usr/lib/node/mraa
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/node_modules/mraa/* $(1)/usr/lib/node/mraa/
endef

define Package/libmraa-python/install
	$(INSTALL_DIR) $(1)/usr/lib/python$(PYTHON_VERSION)/site-packages
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/python$(PYTHON_VERSION)/site-packages/* \
		$(1)/usr/lib/python$(PYTHON_VERSION)/site-packages/
endef

define Package/libmraa-python3/install
	$(INSTALL_DIR) $(1)/usr/lib/python$(PYTHON3_VERSION)/site-packages
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/python$(PYTHON3_VERSION)/site-packages/* \
		$(1)/usr/lib/python$(PYTHON3_VERSION)/site-packages/
endef

$(eval $(call BuildPackage,libmraa))
$(eval $(call BuildPackage,libmraa-node))
$(eval $(call BuildPackage,libmraa-python))
$(eval $(call BuildPackage,libmraa-python3))
