# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-protobuf
PKG_VERSION:=5.29.1
PKG_RELEASE:=1

PYPI_NAME:=protobuf
PKG_HASH:=683be02ca21a6ffe80db6dd02c0b5b2892322c59ca57fd6c872d652cb80549cb

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE
PKG_CPE_ID:=cpe:/a:google:protobuf

PKG_BUILD_DEPENDS:=protobuf/host

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk

define Package/python3-protobuf
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=Protobuf support for Python
  URL:=https://pypi.org/project/protobuf
  DEPENDS:=+protobuf +python3-light +python3-ctypes
endef

define Package/python3-protobuf/description
Protocol Buffers - Google's data interchange format, for Python
endef

$(eval $(call Py3Package,python3-protobuf))
$(eval $(call BuildPackage,python3-protobuf))
