# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libtinyb
PKG_VERSION:=0.5.1
PKG_RELEASE=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/intel-iot-devkit/tinyb/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=1d27b5f3b05c5b7a9f29f3d717164162607aa94b8e15ba2a9aaa3884908a2da1
PKG_BUILD_DIR:=$(BUILD_DIR)/tinyb-$(PKG_VERSION)

CMAKE_INSTALL:=1
CMAKE_BINARY_SUBDIR:=build
PKG_USE_MIPS16:=0

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libtinyb/description
  This project aims to create clean, modern and easy to use Bluetooth LE API. TinyB exposes the BLE GATT API for C++, Java and other languages, using BlueZ over DBus.
endef

define Package/libtinyb
  SECTION:=libs
  CATEGORY:=Libraries
  SUBMENU:=IoT
  TITLE:=Tiny Bluetooth LE Library
  URL:=https://github.com/intel-iot-devkit/tinyb
  DEPENDS:=@!arc @!armeb @!powerpc +libstdcpp +glib2
endef

define Package/libtinyb/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libtinyb.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libtinyb))
