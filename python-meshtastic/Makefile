# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-meshtastic
# TODO renovate
PKG_VERSION:=2.7.4
PKG_RELEASE:=1

PYPI_NAME:=meshtastic
# TODO renovate?
PKG_HASH:=9bcd1f386eac1aff2e07d3b1626925c2e9515d39c09153849fb493094c1bed30

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSE.md

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
	+python3-tabulate +python3-protobuf +python3-pypubsub
endef

define Package/python3-meshtastic/description
Meshtastic Python CLI / API
endef

$(eval $(call Py3Package,python3-meshtastic))
$(eval $(call BuildPackage,python3-meshtastic))
