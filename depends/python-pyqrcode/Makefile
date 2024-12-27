# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-pyqrcode
PKG_VERSION:=1.2.1
PKG_RELEASE:=1

PYPI_NAME:=PyQRCode
PKG_HASH:=fdbf7634733e56b72e27f9bce46e4550b75a3a2c420414035cae9d9d26b234d5

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>
PKG_LICENSE:=BSD-3-Clause

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-pyqrcode
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=QR code generator for Python
  URL:=https://pypi.org/project/pyqrcode
  DEPENDS:=+python3-light +python3-urllib +python3-xml
endef

define Package/python3-pyqrcode/description
A QR code generator written purely in Python with SVG, EPS, PNG and terminal output
endef

$(eval $(call Py3Package,python3-pyqrcode))
$(eval $(call BuildPackage,python3-pyqrcode))
