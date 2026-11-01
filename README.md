# postmarketOS port for Samsung Galaxy J7 Neo (SM-J701M, j7velte)

Work in progress. Exynos 7870, based on the close-to-mainline kernel
(exynos7870-mainline) and U-Boot's generic Exynos mobile board.
Boots from a microSD card.

## Status (tested on SM-J701M)
Working: U-Boot via Odin (BOOT partition), boot from microSD, framebuffer
(simpledrm), touchscreen (melfas_mip4, patch 0025), battery gauge, Wi-Fi,
Phosh session. USB gadget works only after `rootfs/usb-muic.start` closes
the S2MU005 MUIC D+/D- switches (register 0xB5 = 0x24).
Untested: touch keys (patch 0026 + DT node), see git log.
Known issues: Panfrost reports INSTR_INVALID_ENC with the GPU compositor
(WLR_RENDERER=pixman as workaround), no MUIC/charger driver, no panel
driver (EA8061S), no audio/Bluetooth/sensors/camera checked yet.

## Layout
- kernel/devicetrees/: exynos7870-j7velte.dts (goes in mainline-patches/devicetrees)
- kernel/patches/: patches 0025, 0026 (go in mainline-patches/patches)
- u-boot/: exynos7870-j7velte-u-boot.dtsi (arch/arm/dts) and the DTS in dts/upstream/src/arm64/exynos
- pmaports/: diff of linux-postmarketos-exynos7870 (local patches tarball + config)
- rootfs/usb-muic.start: copy to /etc/local.d/ on the device

Hardware data comes from Samsung's open source release for SM-J701M.
Files derived from other projects keep their original licenses (GPL-2.0).
