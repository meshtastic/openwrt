# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=meshtasticd-web
# TODO renovate
PKG_VERSION:=2.6.0
PKG_RELEASE:=1

PKG_SOURCE:=build.tar
PKG_SOURCE_URL:=https://github.com/meshtastic/web/releases/download/v$(PKG_VERSION)/
# TODO renovate?
PKG_HASH:=d01e7bdb687b6689b2e3e1f6d2ca71839ccce9301b3e2b519039ea23a1d66456
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
	$(INSTALL_DIR) $(1)/etc/meshtasticd/ssl
endef

$(eval $(call BuildPackage,meshtasticd-web))
