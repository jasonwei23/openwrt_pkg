include $(TOPDIR)/rules.mk

PKG_NAME:=coredns
PKG_VERSION:=1.11.3
PKG_RELEASE:=1

PKG_SOURCE:=coredns-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE_URL:=https://codeload.github.com/coredns/coredns/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=b64e0c5970000595a0682e9a87ebbad5ef0db790c1b6efbba6e341211bdf3299

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0
PKG_BUILD_FLAGS:=no-mips16

GO_PKG:=github.com/coredns/coredns
GO_PKG_LDFLAGS:=-s -w
#GO_PKG_GO_GENERATE:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/coredns
	SECTION:=net
	CATEGORY:=Network
	TITLE:=CoreDNS
	URL:=https://github.com/coredns/coredns
	DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle +libc +libpthread
endef

define Package/coredns/install
	$(call GoPackage/Package/Install/Bin,$(1))

	$(INSTALL_DIR) $(1)/etc/init.d $(1)/etc/coredns $(1)/etc/config
	$(INSTALL_BIN) $(CURDIR)/files/etc/init.d/coredns $(1)/etc/init.d/coredns
	$(INSTALL_CONF) $(CURDIR)/files/etc/coredns/Corefile $(1)/etc/coredns/Corefile
	$(INSTALL_CONF) $(CURDIR)/files/etc/config/coredns $(1)/etc/config/coredns
endef

define Build/Prepare
	( \
		$(call Build/Prepare/Default) ; \
		$(CP) $(CURDIR)/plugin.cfg $(PKG_BUILD_DIR)/plugin.cfg ; \
		cd $(PKG_BUILD_DIR) ; \
		go generate coredns.go ; \
		go get ; \
	)
endef

define Package/coredns/description
	CoreDNS is a DNS server that chains plugins.
endef

$(eval $(call GoBinPackage,coredns))
$(eval $(call BuildPackage,coredns))
