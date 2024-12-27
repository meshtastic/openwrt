# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-dotmap
PKG_VERSION:=1.3.30
PKG_RELEASE:=1

PYPI_NAME:=dotmap
PKG_HASH:=5821a7933f075fb47563417c0e92e0b7c031158b4c9a6a7e56163479b658b368

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE.txt

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-dotmap
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=dot-access dictionaries for Python
  URL:=https://pypi.org/project/dotmap
  DEPENDS:=+python3-light
endef

define Package/python3-dotmap/description
ordered, dynamically-expandable dot-access dictionary
endef

$(eval $(call Py3Package,python3-dotmap))
$(eval $(call BuildPackage,python3-dotmap))
