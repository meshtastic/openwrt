# Inspired by OnionIOT's `onion-dt-overlay` package
# https://github.com/OnionIoT/OpenWRT-Packages/tree/openwrt-23.05/onion-dt-overlay

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=openwrt-one-mikrobus-spidev
PKG_URL:=https://github.com/openwrt/openwrt/pull/17399
PKG_VERSION:=1.0
PKG_RELEASE:=1

DTC=$(LINUX_DIR)/scripts/dtc/dtc

include $(INCLUDE_DIR)/package.mk

# @TARGET_mediatek_filogic
define Package/openwrt-one-mikrobus-spidev
	TITLE:=openwrt-one-mikrobus-spidev
	DEPENDS:=+kmod-spi-dev +kmod-fs-configfs @aarch64
endef

define Package/openwrt-one-mikrobus-spidev/description
	!!! ONLY INSTALL ON OpenWRT One !!!
	DT Overlay for OpenWRT One MikroBus spidev support
endef

define Build/Compile
	$(DTC) -b 0 -@ -O dtb ./files/mt7981b-openwrt-one-mikrobus-spidev.dtso -o $(PKG_BUILD_DIR)/mt7981b-openwrt-one-mikrobus-spidev.dtbo
endef

define Package/openwrt-one-mikrobus-spidev/install
	$(INSTALL_DIR) $(1)/lib/firmware/device-tree/overlays
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/mt7981b-openwrt-one-mikrobus-spidev.dtbo $(1)/lib/firmware/device-tree/overlays/mt7981b-openwrt-one-mikrobus-spidev.dtbo
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/dtbo-mikrobus-spidev.init $(1)/etc/init.d/dtbo-mikrobus-spidev
endef

define Package/openwrt-one-mikrobus-spidev/postinst
#!/bin/sh
if [ -z "$$$${IPKG_INSTROOT}" ]; then
	/etc/init.d/dtbo-mikrobus-spidev enable
	/etc/init.d/dtbo-mikrobus-spidev start
fi
endef

define Package/openwrt-one-mikrobus-spidev/prerm
#!/bin/sh
if [ -z "$$$${IPKG_INSTROOT}" ]; then
	/etc/init.d/dtbo-mikrobus-spidev stop
	/etc/init.d/dtbo-mikrobus-spidev disable
fi
endef

$(eval $(call BuildPackage,openwrt-one-mikrobus-spidev))
