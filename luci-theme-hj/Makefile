#
# Copyright (C) 2019-2024
#
# Licensed under the Apache License, Version 2.0
#

include $(TOPDIR)/rules.mk

THEME_NAME:=hj
PKG_NAME:=luci-theme-hj
PKG_VERSION:=3.0.3
PKG_RELEASE:=1

LUCI_TITLE:=hj Theme by houjie
LUCI_DEPENDS:=+luci-base

define Package/luci-theme-hj
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=3. Themes
  TITLE:=$(LUCI_TITLE)
  DEPENDS:=$(LUCI_DEPENDS)
endef

define Package/luci-theme-hj/install
	$(INSTALL_DIR) $(1)/www/luci-static/$(THEME_NAME)
	$(CP) ./htdocs/* $(1)/www/luci-static/$(THEME_NAME)/

	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/view/themes/$(THEME_NAME)
	$(CP) ./luasrc/view/themes/$(THEME_NAME)/* $(1)/usr/lib/lua/luci/view/themes/$(THEME_NAME)/
endef

define Package/luci-theme-hj/postinst
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || {
	uci -q batch <<-EOF
		set luci.themes.$(THEME_NAME)=/luci-static/$(THEME_NAME)
		commit luci
	EOF
	rm -f /tmp/luci-indexcache.*
	rm -rf /tmp/luci-modulecache/
	killall -HUP rpcd 2>/dev/null
}
endef

define Package/luci-theme-hj/postrm
#!/bin/sh
[ -n "$${IPKG_INSTROOT}" ] || {
	uci -q delete luci.themes.$(THEME_NAME)
	uci commit luci
	rm -f /tmp/luci-indexcache.*
	rm -rf /tmp/luci-modulecache/
	killall -HUP rpcd 2>/dev/null
}
endef

CONFIG_LUCI_CSSTIDY:=

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
