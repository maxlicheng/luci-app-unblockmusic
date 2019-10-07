# Copyright (C) 2016 Openwrt.org
#
# This is free software, licensed under the Apache License, Version 2.0 .
#
# licheng
# www.maxlicheng.com
# 2019-06-08
#

include $(TOPDIR)/rules.mk

_VER_MAJ := $(shell cat "./version/.VER_MAJ")
_VER_MIN := $(shell cat "./version/.VER_MIN")
_VER_REV := $(shell cat "./version/.VER_REV")
_VER_PTH := $(shell cat "./version/.VER_PTH")

PKG_NAME:=luci-app-unblockmusic
PKG_VERSION:=v$(_VER_MAJ).$(_VER_MIN).$(_VER_REV)
PKG_RELEASE:=$(_VER_PTH)

PKG_LICENSE:=Apache-2.0

LUCI_TITLE:=LuCI support for Unblock NeteaseCloudMusic
LUCI_DEPENDS:=+UnblockNeteaseMusic +bash +dnsmasq-full +ipset +curl +wget +libopenssl
LUCI_PKGARCH:=all

PKG_MAINTAINER:=<https://github.com/maxlicheng/luci-app-unblockmusic>

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature

