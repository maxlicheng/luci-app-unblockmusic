# Copyright (C) 2020 Openwrt.org
#
# This is free software, licensed under the Apache License, Version 2.0 .
#
# licheng
# www.maxlicheng.com
# 2019-06-08
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-unblockmusic
PKG_VERSION:=2.3.1
PKG_RELEASE:=41

PKG_CONFIG_DEPENDS := \
	CONFIG_UnblockNeteaseMusic_Go \
	CONFIG_UnblockNeteaseMusic_NodeJS

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)/config
  source "$(SOURCE)/Config.in"
endef

PKG_LICENSE:=Apache-2.0

LUCI_TITLE:=LuCI support for Unblock NeteaseCloudMusic
LUCI_DEPENDS:=+dnsmasq-full +ipset +wget +UnblockNeteaseMusic_NodeJS:UnblockNeteaseMusic +UnblockNeteaseMusic_Go:UnblockNeteaseMusicGo
LUCI_PKGARCH:=all

PKG_MAINTAINER:=<https://github.com/maxlicheng/luci-app-unblockmusic>

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature

