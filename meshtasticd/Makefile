# SPDX-License-Identifier: GPL-2.0-only

include $(TOPDIR)/rules.mk

PKG_NAME:=meshtasticd
PKG_VERSION:=2.8.2
PKG_SOURCE_VERSION:=f7f66b4731d182bc18ce11e542c6e7632e853310
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/meshtastic/firmware.git
PKG_MIRROR_HASH:=6353fc4d633bdec38b1cd416dede419f1fa080771ca38724b5b6dd91d0121f67

FRONTEND_VERSION:=2.7.2
FRONTEND_DEST:=$(PKG_NAME)-frontend-$(FRONTEND_VERSION).tar
FRONTEND_URL:=https://github.com/meshtastic/web/releases/download/v$(FRONTEND_VERSION)/
FRONTEND_HASH:=62657b85b4c24af4d44da2932b64143abdbf6e65a79fcb51fd0801d9540616e2

PKG_BUILD_DEPENDS:= \
	python3/host \
	python-platformio/host \
	python-pyelftools/host \
	!USE_GLIBC:argp-standalone

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>, George Sapkin <george@sapk.in>
PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-host.mk
include $(INCLUDE_DIR)/nls.mk

define Package/meshtasticd/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Meshtastic
  TITLE:=Meshtastic daemon
  URL:=https://github.com/meshtastic/firmware
endef

# Leaving a possibility for adding a light variant without the web UI / avahi
# support if it's made configurable upstream. Currently headers are autodetected
# so it's not possible to add it.
define Package/meshtasticd-full
  $(call Package/meshtasticd/Default)
  TITLE+= (with web UI + avahi support)
  DEPENDS:= \
    +bluez-libs \
    +kmod-spi-dev \
    +libgpiod \
    +libi2c \
    +libopenssl \
    +liborcania \
    +libulfius-gnutls \
    +libusb-1.0 \
    +libuv \
    +libyaml-cpp \
    +libyder \
    +zlib \
    +jsoncpp \
    +libavahi-client \
    $(INTL_DEPENDS)
  PROVIDES:=meshtasticd
endef

# Transitional. meshtasticd announces itself over mDNS directly as of 2.8.x
# (NativeDiscovery.cpp, via libavahi-client), so the static service file is
# now a duplicate announcement. This package ships nothing and exists only to
# retire that file on systems that installed the old one. Drop it after the
# next release branch.
define Package/meshtasticd-avahi-service
  $(call Package/meshtasticd/Default)
  TITLE+= (avahi service, transitional)
  DEPENDS:=+meshtasticd
endef

define Package/meshtasticd-web
  $(call Package/meshtasticd/Default)
  TITLE:=Meshtastic daemon web interface
  URL:=https://github.com/meshtastic/web
  DEPENDS:=+meshtasticd-full
  VERSION:=$(FRONTEND_VERSION)-r$(PKG_RELEASE)
endef

define Package/meshtasticd-full/description
  Meshtastic daemon with web interface support
endef

define Package/meshtasticd-avahi-service/description
  Transitional empty package. meshtasticd now announces itself via mDNS
  directly; this package is safe to remove.
endef

define Package/meshtasticd-web/description
  The official Meshtastic web interface
endef

define Download/meshtasticd-web
  URL:=$(FRONTEND_URL)
  URL_FILE:=build.tar
  FILE:=$(FRONTEND_DEST)
  HASH:=$(FRONTEND_HASH)
endef

PLATFORMIO_BUILD_FLAGS := \
	-fdata-sections \
	-ffunction-sections \
	-Os \
	-Wl,--gc-sections \
	-lcrypto \
	-lorcania \
	-lssl \
	-lulfius \
	-lyder \
	$(if $(CONFIG_USE_GLIBC),,-largp) \
	$(if $(INTL_FULL),-lintl)

BUILD_FLAGS := \
	TARGET_AR="$(TARGET_AR)" \
	TARGET_AS="$(TARGET_CC) -c $(TARGET_ASFLAGS)" \
	TARGET_CC="$(TARGET_CC)" \
	TARGET_CFLAGS="$(TARGET_CFLAGS)" \
	TARGET_CXX="$(TARGET_CXX)" \
	TARGET_CXXFLAGS="$(TARGET_CXXFLAGS)" \
	TARGET_LD="$(TARGET_LD)" \
	TARGET_LDFLAGS="$(TARGET_LDFLAGS)" \
	TARGET_OBJCOPY="$(TARGET_CROSS)objcopy" \
	TARGET_RANLIB="$(TARGET_RANLIB)" \
	PLATFORMIO_BUILD_CACHE_DIR="$(PKG_BUILD_DIR)/.pio-build-cache" \
	PLATFORMIO_CACHE_DIR="$(DL_DIR)/platformio-cache"

define Build/Prepare/meshtasticd-web
	mkdir -p $(PKG_BUILD_DIR)/web
	$(HOST_TAR) -xf $(DL_DIR)/$(FRONTEND_DEST) -C $(PKG_BUILD_DIR)/web
	gzip -dr $(PKG_BUILD_DIR)/web/
endef

define Build/Prepare
	$(call Build/Prepare/Default)
	$(call Build/Prepare/meshtasticd-web)
endef

define Build/Compile/meshtasticd-full
	mkdir -p $(PKG_BUILD_DIR)/full

	$(BUILD_FLAGS) \
	PLATFORMIO_BUILD_DIR="$(PKG_BUILD_DIR)/full" \
	PLATFORMIO_BUILD_FLAGS="$(PLATFORMIO_BUILD_FLAGS)" \
	$(HOST_PYTHON3_BIN) -m platformio run \
		--environment buildroot \
		--project-dir $(PKG_BUILD_DIR)
endef

define Build/Compile
	$(call Build/Compile/meshtasticd-full)
endef

define Package/meshtasticd-full/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/meshtasticd.conf $(1)/etc/config/meshtasticd

	$(INSTALL_DIR) $(1)/etc/meshtasticd
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/bin/config-dist.yaml $(1)/etc/meshtasticd/config.yaml

	$(INSTALL_DIR) $(1)/etc/meshtasticd/available.d
	$(CP) -R $(PKG_BUILD_DIR)/bin/config.d/* $(1)/etc/meshtasticd/available.d

	$(INSTALL_DIR) $(1)/etc/meshtasticd/config.d

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/meshtasticd.init $(1)/etc/init.d/meshtasticd

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/full/buildroot/meshtasticd $(1)/usr/bin/meshtasticd
endef

define Package/meshtasticd-avahi-service/install
	:
endef

# Remove the static Avahi service file
define Package/meshtasticd-avahi-service/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
	rm -f /etc/avahi/services/meshtasticd.service
fi
exit 0
endef

define Package/meshtasticd-web/install
	$(INSTALL_DIR) $(1)/usr/share/meshtasticd/web
	$(CP) $(PKG_BUILD_DIR)/web/* $(1)/usr/share/meshtasticd/web

	$(INSTALL_DIR) $(1)/etc/meshtasticd/ssl
endef

define Package/meshtasticd-full/conffiles
/etc/config/meshtasticd
/etc/meshtasticd/config.d/
/etc/meshtasticd/config.yaml
/etc/meshtasticd/ssl
endef

$(eval $(call Download,meshtasticd-web))
$(eval $(call BuildPackage,meshtasticd-full))
$(eval $(call BuildPackage,meshtasticd-avahi-service))
$(eval $(call BuildPackage,meshtasticd-web))
