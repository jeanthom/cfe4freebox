# BCM6348 CFE Bootloader for Freebox (BCM6348)

This is a custom Broadcom CFE bootloader suited for Freebox SAS hardware (BCM6348 only). It probably breaks compatibility with the original firmware (**you won't be able to use your Freebox on Free's network anymore**), but *it does not matter* since the goal is to flash another OS (eg. OpenWRT) and use your Freebox as an generic embedded Linux platform.

It has mostly been tested on Freebox V4. It also works on Freebox V5 (but it is not fully supported).

You need to install this in order to compile : gcc, make, libstdc++5, unzip, libz-dev and libc headers. MIPS toolchain for i686 is provided, see [Building](#Building) if you want to replace it with your own toolchain.

## Building

Edit build.sh to set the board MAC address, and eventually edit board type. You can then build using the provided shell script :

```
./build.sh
```

A MIPS compiler for x86 GNU/Linux is provided, if you want to use your own you may want to edit the compiler path in `./cfe/build/broadcom/bcm63xx_rom/Makefile` et `./cfe/build/broadcom/bcm63xx_ram/Makefile`.

## Flashing CFE

JTAG is the recommended method, because in case of software brick you will (hopefully) be able to recover.

## Networking

EMACs are the network interfaces integrated into the BCM6348 chip.

The EMAC parameters are hardcoded in `/shared/opensource/boardparms/bcm963xx/boardparms.c`. Currently only Freebox V4 parameters are stored.

Only **ONE** is EMAC used by the bootloader. You can edit `/cfe/cfe/arch/mips/board/bcm63xx_ram/src/dev_bcm6348_eth.c` to replace constant `ENET_USE_EMAC1` to `ENET_USE_EMAC2`.

## Credits

Based on original work from Broadcom/@danitool/@Noltari.

