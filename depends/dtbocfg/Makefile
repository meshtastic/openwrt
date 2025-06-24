# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (c) 2022 Tomasz Maciej Nowak <tmn505 at gmail.com>

include $(TOPDIR)/rules.mk

PKG_NAME:=dtbocfg
PKG_VERSION:=0.1.1
PKG_RELEASE:=1

PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ikwzm/dtbocfg.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=2d6a31ba01d05ab9bd15f127c06fab0e504dd6d7e41115be53e0021e6f8ba877

PKG_MAINTAINER:=Austin Lane <vidplace7@gmail.com>, Tomasz Maciej Nowak <tmn505@gmail.com>
PKG_BUILD_PARALLEL:=1
# PKG_FLAGS:=nonshared

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

# @!TARGET_bcm27xx @!OF_CONFIGFS
define KernelPackage/fs-dtbocfg
  SUBMENU:=Filesystems
  TITLE:=Device Tree Blob Overlay Configuration File System
  DEPENDS:=+kmod-fs-configfs
  FILES:=$(PKG_BUILD_DIR)/dtbocfg.$(LINUX_KMOD_SUFFIX)
  AUTOLOAD:=$(call AutoLoad,31,dtbocfg)
endef

define KernelPackage/fs-dtbocfg/description
  Device Tree Overlay is a mechanism that enables dynamic loading/unloading
  of a new device tree blob on top of the kernel device tree.
endef

define Build/Compile
	$(KERNEL_MAKE) M="$(PKG_BUILD_DIR)" modules
endef

$(eval $(call KernelPackage,fs-dtbocfg))
