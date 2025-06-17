#
# Copyright (C) 2015-2019 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=python-idna
PKG_VERSION:=3.3
PKG_RELEASE:=2

PYPI_NAME:=idna
PKG_HASH:=9d643ff0a55b762d5cdb124b8eaa99c66322e2157b69160bc32796e824360e6d

PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE.rst
PKG_MAINTAINER:=Jeffery To <jeffery.to@gmail.com>

HOST_BUILD_DEPENDS:=python3/host python-build/host python-installer/host python-wheel/host python-setuptools/host
PKG_BUILD_DEPENDS:=python-setuptools/host

include $(TOPDIR)/feeds/packages/lang/python/pypi.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-package.mk
include $(TOPDIR)/feeds/packages/lang/python/python3-host-build.mk

define Package/python3-idna
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=IDNA library
  URL:=https://github.com/kjd/idna
  DEPENDS:= \
      +python3-light \
      +python3-codecs
endef

define Package/python3-idna/description
A library to support the Internationalised Domain Names in Applications
(IDNA) protocol as specified in RFC 5891. This version of the protocol
is often referred to as "IDNA2008" and can produce different results
from the earlier standard from 2003.
endef

$(eval $(call Py3Package,python3-idna))
$(eval $(call BuildPackage,python3-idna))
$(eval $(call BuildPackage,python3-idna-src))
$(eval $(call HostBuild))
