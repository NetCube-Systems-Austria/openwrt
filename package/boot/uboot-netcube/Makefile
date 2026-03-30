include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://gitlab.com/netcube-systems-austria/u-boot.git
PKG_SOURCE_DATE:=2026-03-25
PKG_SOURCE_VERSION:=96dc047f9153862346ec48ec7ed44865dc1f4e4d
PKG_MIRROR_HASH:=skip

PKG_MAINTAINER:=NetCube Systems Austria

UBOOT_USE_INTREE_DTC:=1

include $(INCLUDE_DIR)/u-boot.mk
include $(INCLUDE_DIR)/package.mk

define U-Boot/Default
  BUILD_TARGET:=sunxi
  UBOOT_IMAGE:=u-boot-sunxi-with-spl.bin
  UENV:=default
  HIDDEN:=1
endef

define U-Boot/netcube_nagami_basic_carrier
  BUILD_SUBTARGET:=cortexa7
  NAME:=NetCube Systems Nagami Basic Carrier Board
  BUILD_DEVICES:=netcube_nagami-basic-carrier
  UENV:=netcube_nagami
endef

UBOOT_TARGETS := \
	netcube_nagami_basic_carrier

UBOOT_CONFIGURE_VARS += USE_PRIVATE_LIBGCC=yes

UBOOT_CUSTOMIZE_CONFIG := \
	--disable TOOLS_KWBIMAGE \
	--disable TOOLS_LIBCRYPTO \
	--disable TOOLS_MKEFICAPSULE

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR_IMAGE)
	$(CP) $(PKG_BUILD_DIR)/$(UBOOT_IMAGE) $(STAGING_DIR_IMAGE)/$(BUILD_DEVICES)-u-boot-with-spl.bin
	mkimage -C none -A arm -T script -d uEnv-$(UENV).txt \
		$(STAGING_DIR_IMAGE)/$(BUILD_DEVICES)-boot.scr
endef

define Package/u-boot/install/default
endef

$(eval $(call BuildPackage/U-Boot))
