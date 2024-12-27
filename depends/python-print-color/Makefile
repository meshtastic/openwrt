# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-print-color
PKG_VERSION:=0.4.6
PKG_RELEASE:=1

PYPI_NAME:=print_color
PKG_HASH:=d3aafc1666c8d31a85fffa6ee8e4f269f5d5e338d685b4e6179915c71867c585

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=python-poetry-core/host

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-print-color
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Print in color to the terminal
  URL:=https://pypi.org/project/print-color
  DEPENDS:=+python3-light
endef

define Package/python3-print-color/description
A simple package to print in color to the terminal
endef

$(eval $(call Py3Package,python3-print-color))
$(eval $(call BuildPackage,python3-print-color))
