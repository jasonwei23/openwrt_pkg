include $(TOPDIR)/rules.mk

PKG_NAME:=custom-settings
PKG_VERSION:=1
PKG_RELEASE:=1

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/custom-settings
  SECTION:=luci
  CATEGORY:=LuCI
  TITLE:=Custom Settings
  DEPENDS:=+TARGET_x86:ethtool
endef

define Package/custom-settings/description
	Custom Settings.
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/custom-settings/install
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) $(CURDIR)/files/zzz-default-settings $(1)/etc/uci-defaults/99-default-settings
	$(INSTALL_DIR) $(1)/etc/sysctl.d
	$(INSTALL_CONF) $(CURDIR)/files/20-net-core-mem.conf $(1)/etc/sysctl.d/20-net-core-mem.conf

ifneq ($(filter i386 i686 x86_64, $(ARCH)),)
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/autocore $(1)/etc/init.d/autocore
endif

endef

$(eval $(call BuildPackage,custom-settings))
