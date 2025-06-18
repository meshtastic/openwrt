#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libyder
PKG_VERSION:=1.4.12
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/babelouest/yder/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=59bed6df43c29bf1a0f85274369f7a8bc7dfe5e94be826139e8aa05eda3ba2e6

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>
PKG_LICENSE:=LGPL-2.1-or-later
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/yder-$(PKG_VERSION)
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libyder
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Logging library written in C.
  URL:=https://github.com/babelouest/yder
  DEPENDS:=+liborcania
endef

CMAKE_OPTIONS += \
	-DWITH_JOURNALD=off \
	-DCMAKE_BUILD_TYPE=Release

define Package/libyder/description
  Simple and easy to use logging library.
  You can log messages to the console, a file, Syslog, journald or a callback function.
endef

define Package/libyder/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libyder.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libyder))
