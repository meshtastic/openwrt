# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=meshtasticd-web
PKG_VERSION:=2.5.4
PKG_RELEASE:=1

PKG_SOURCE:=build.tar
PKG_SOURCE_URL:=https://github.com/meshtastic/web/releases/download/v$(PKG_VERSION)/
PKG_HASH:=9aded26483a8bee4e8811f33744da2016ad4bca4894f6d4cbdea79a53b0a7eaa
UNPACK_CMD=\
	mkdir -p $(1)/web; \
  $(TAR) -xf $(DL_DIR)/$(PKG_SOURCE) -C $(1)/web; \
	gzip -dr $(1)/web/

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>
PKG_LICENSE:=GPL-3.0

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/meshtasticd-web
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Meshtastic Daemon Web Interface
  URL:=http://github.com/meshtastic/firmware
  DEPENDS:=meshtasticd
endef

define Package/meshtasticd-web/description
  Meshtastic Daemon Web Interface
endef

define Build/Compile
endef

define Package/meshtasticd-web/install
	$(INSTALL_DIR) $(1)/usr/share/meshtasticd/web
	$(CP) $(PKG_BUILD_DIR)/web/* $(1)/usr/share/meshtasticd/web
endef

$(eval $(call BuildPackage,meshtasticd-web))
