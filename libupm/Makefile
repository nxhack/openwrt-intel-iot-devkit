#
# Copyright (C) 2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libupm
PKG_VERSION:=1.6.0
PKG_RELEASE:=2

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/intel-iot-devkit/upm.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=cc7fec9ae0228add9011bf1c2cd5e0ca2ba0d4f0
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_MIRROR_HASH:=26bc9c32eea0b8aa6218735e30a3d2317431518f0b2a055c0f21e78e6d92ca4f

PKG_MAINTAINER:=John Crispin <blogic@openwrt.org>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

CMAKE_INSTALL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

OW_VER:=$(shell git --git-dir=$(TOPDIR)/.git describe --abbrev=0 --always --tag)

UPM_MODULES:= \
	a110x abp ad8232 adafruitms1438 adafruitss adc121c021 adis16448 ads1x15 adxl335 adxl345 \
	adxrs610 am2315 apa102 apds9002 apds9930 at42qt1070 bh1750 biss0001 bma220 \
	bma250e bmg160 bmi160 bmm150 bmp280 bmpx8x bmx055 bno055 button buzzer cjq4435 collision \
	cwlsxxa dfrec dfrorp dfrph ds1307 ds1808lc ds18b20 ds2413 ecezo ecs1030 \
	ehr eldriver electromagnet emg enc03r flex gas gp2y0a gprs grove grovecollision groveehr \
	groveeldriver groveelectromagnet groveemg grovegprs grovegsr grovelinefinder grovemd \
	grovemoisture groveo2 grovescam grovespeaker groveultrasonic grovevdiv grovewater grovewfs \
	gsr guvas12d h3lis331dl hcsr04 hdc1000 hdxxvxta hka5 hlg150h hm11 hmc5883l hmtrp hp20x \
	ht9170 htu21d hx711 ili9341 ims ina132 interfaces isd1820 itg3200 jhd1313m1 joystick12 \
	kxcjk1013 l298 l3gd20 lcd lcdks lcm1602 ldt0028 led lidarlitev3 light linefinder lis2ds12 \
	lis3dh lm35 lol loudness lp8860 lpd8806 lsm303agr lsm303d lsm303dlh lsm6ds3h lsm6dsl lsm9ds0 \
	m24lr64e mag3110 max30100 max31723 max31855 max44000 max44009 max5487 maxds3231m maxsonarez \
	mb704x mcp2515 mcp9808 md mg811 mhz16 mic micsv89 mlx90614 mma7361 mma7455 mma7660 mma8x5x \
	mmc35240 moisture mpl3115a2 mpr121 mpu9150 mq303a ms5611 ms5803 my9221 nlgpio16 nmea_gps \
	nrf24l01 nrf8001 nunchuck o2 otp538u p9813 pca9685 pn532 ppd42ns pulsensor relay rf22 \
	rfr359f rgbringcoder rhusb rn2903 rotary rotaryencoder rpr220 rsc scam sensortemplate \
	servo sht1x si1132 si114x si7005 slide sm130 smartdrive speaker ssd1351 st7735 stepmotor \
	sx1276 sx6119 t6713 ta12200 tca9548a tcs3414cs tcs37727 teams temperature \
	tex00 th02 tm1637 tmp006 tsl2561 ttp223 uartat uln200xa ultrasonic urm37 utilities vdiv \
	veml6070 water waterlevel wfs wheelencoder wt5001 xbee yg1006 zfm20 \
	vcap t3311 hwxpxx h803x
# (require libbacnet) tb7300 t8100 e50hx bacnetmstp
# (require libmraa firmata) curieimu
ifneq ($(filter reboot v18.06%, $(OW_VER)),)
UPM_MODULES+=ozw
endif

CMAKE_OPTIONS=-DBUILDARCH=$(CONFIG_ARCH) \
	-DNODE_EXECUTABLE=$(STAGING_DIR_HOSTPKG)/bin/node \
	-DSWIG_DIR=$(STAGING_DIR_HOSTPKG)/bin

define Package/libupm/Default
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libmraa +librt
  SUBMENU:=IoT
endef

define Package/libupm
  $(call Package/libupm/Default)
  TITLE:=Intel IoT sensor library - Full
  DEPENDS+=+libjpeg +libmodbus
  ifneq ($(filter reboot v18.06%, $(OW_VER)),)
    DEPENDS+=+openzwave
  endif
  DEPENDS+= $(foreach module, $(UPM_MODULES), +libupm-$(module))
endef

define Package/libupm/install/Default
	$(INSTALL_DIR) $(1)/usr/lib/{node/,python2.7/site-packages/upm}
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libupm*-$(2).so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/jsupm_$(2) $(1)/usr/lib/node/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/python2.7/site-packages/upm/{pyupm_$(2).py,_pyupm_$(2).so} \
		$(1)/usr/lib/python2.7/site-packages/upm/ ;
endef

define Package/libupm/install
	$(foreach module, $(UPM_MODULES), \
		$(call Package/libupm/install/Default,$(1),$(module)))
endef

define UpmPackage
define Package/libupm-$(1)
  $(call Package/libupm/Default)
  TITLE:=Intel IoT sensor library - $(1)
  ifeq ($(1),adafruitms1438)
    DEPENDS+=+libupm-pca9685
  endif
  ifeq ($(1),ads1x15)
    DEPENDS+=+libupm-interfaces
  endif
  ifeq ($(1),apa102)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),bh1750)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),bma250e)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),bmg160)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),bmi160)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),bmm150)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),bmp280)
    DEPENDS+=+libupm-interfaces +libupm-utilities
  endif
  ifeq ($(1),bmpx8x)
    DEPENDS+=+libupm-interfaces +libupm-utilities
  endif
  ifeq ($(1),bmx055)
    DEPENDS+=+libupm-utilities +libupm-bma250e +libupm-bmg160 +libupm-bmm150
  endif
  ifeq ($(1),bno055)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),buzzer)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),cjq4435)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),dfrec)
    DEPENDS+=+libupm-utilities +libupm-ds18b20
  endif
  ifeq ($(1),ds18b20)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),dfrorp)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),ds1808lc)
    DEPENDS+=+libupm-interfaces
  endif
  ifeq ($(1),ecezo)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),enc03r)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),guvas12d)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),hcsr04)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),hka5)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),hlg150h)
    DEPENDS+=+libupm-interfaces
  endif
  ifeq ($(1),ims)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),jhd1313m1)
    DEPENDS+=+libupm-utilities +libupm-lcm1602
  endif
  ifeq ($(1),lcm1602)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),lcdks)
    DEPENDS+=+libupm-utilities +libupm-lcm1602
  endif
  ifeq ($(1),lis2ds12)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),lis3dh)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),lp8860)
    DEPENDS+=+libupm-interfaces
  endif
  ifeq ($(1),lsm303agr)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),lsm303d)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),lsm6ds3h)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),lsm6dsl)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),m24lr64e)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),max30100)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),max44009)
    DEPENDS+=+libupm-interfaces
  endif
  ifeq ($(1),mb704x)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),mcp2515)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),md)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),mma7361)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),ms5611)
    DEPENDS+=+libupm-interfaces
  endif
  ifeq ($(1),ms5803)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),my9221)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),nmea_gps)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),nunchuck)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),otp538u)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),p9813)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),ppd42ns)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),rn2903)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),rsc)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),servo)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),sht1x)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),si1132)
    DEPENDS+=+libupm-interfaces
  endif
  ifeq ($(1),si7005)
    DEPENDS+=+libupm-interfaces
  endif
  ifeq ($(1),speaker)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),t6713)
    DEPENDS+=+libupm-interfaces
  endif
  ifeq ($(1),tsl2561)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),uartat)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),uln200xa)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),urm37)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),wfs)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),zfm20)
    DEPENDS+=+libupm-utilities
  endif
  ifeq ($(1),vcap)
    DEPENDS+=+libjpeg
  endif
  ifeq ($(1),t3311)
    DEPENDS+=+libmodbus
  endif
  ifneq ($(filter reboot v18.06%, $(OW_VER)),)
    ifeq ($(1),ozw)
      DEPENDS+=+openzwave
    endif
  endif
  ifeq ($(1),hwxpxx)
    DEPENDS+=+libmodbus
  endif
  ifeq ($(1),h803x)
    DEPENDS+=+libmodbus
  endif
endef

define Package/libupm-$(1)/install
	$(call Package/libupm/install/Default,$$(1),$(1))
endef
endef

$(eval $(call BuildPackage,libupm))
$(foreach module, $(UPM_MODULES), \
	$(eval $(call UpmPackage,$(module))) \
	$(eval $(call BuildPackage,libupm-$(module))))
