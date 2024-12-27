# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-meshtastic
PKG_VERSION:=2.5.7
PKG_RELEASE:=1

PYPI_NAME:=meshtastic
PKG_HASH:=45e43e192e3a5467dd31f86a378efe4160efde1fdec29af91dc61ed369e33c5d

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSES/GPL-3.0-only.txt

PKG_BUILD_DEPENDS:=python-poetry-core/host

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-meshtastic
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Meshtastic Python
  URL:=https://pypi.org/project/meshtastic
  DEPENDS:= \
	+python3-light +python3-asyncio +python3-decimal +python3-logging \
	+python3-pyserial +python3-requests +python3-yaml +python3-bleak \
	+python3-tabulate +python3-protobuf +python3-pypubsub \
	+python3-dotmap +python3-pyqrcode +python3-print-color
endef

define Package/python3-meshtastic/description
Meshtastic Python CLI / API
endef

$(eval $(call Py3Package,python3-meshtastic))
$(eval $(call BuildPackage,python3-meshtastic))
