# PostmarketOS for Redmi-9A

This repository contains the basis of a PostmarketOS port for the Xiaomi
Redmi 9a smartphone. This phone can be bought for less than 70€ and is a good
candidate for a cheap Linux phone, that's why I'm **trying** to port
PostmarketOS to it.

Please note this is a work in progress and may not be complete!
---

This project may be abandoned at any time, I'm not sure I'll be able to
complete it.

Status: Unable to boot the kernel, the bootloader is not loading the
kernel image correctly. Can't get the kernel log with BROM.

## Technical research

See the [Technical Specifications](SPECS.md) for more details. These are the
results of my research on the phone hardware.

## Unlocking the bootloader

Sadly, Xiaomi phones have a locked bootloader by default and can't be unlocked
with fastboot or using the developer settings.

There are two ways to unlock the bootloader for this phone:
- Mi Unlock Tool
- mtkclient (unofficial)

### Official method

Use the offical [Mi Unlock Tool](https://en.miui.com/unlock/) to unlock the
bootloader (Xiaomi account required). You will have to wait one week before
being able to unlock the bootloader (?!).

### mtkclient method

If you can't wait one week to unlock the bootloader, you can use the mtkclient
software to unlock the bootloader:
```
# Plug the phone in preloader mode (hold volume up + volume down + power)
# The screen should be black
$ python mtk e metadata,userdata,md_udc
$ python mtk da seccfg unlock
$ python mtk reset
```

Using this method, you get a dm-verity error on boot as follows:
```
dm-verity corruption

Your device is corrupt.
It can't be trusted and may not work properly.
Press power button to continue.
Or, device will power off in 5s
```
Press the power button to continue booting, you will get a unlocked lock logo on
the top of the screen, and the phone will boot normally.

## Kernel sources

The kernel sources are available on the Xiaomi Kernel OpenSource Github page,
but I've made a mirror of the sources on this repository for convenience
[here](https://github.com/SheatNoisette/linux-xiaomi-dandelion)

## Using an Alternative Recovery

Using a custom recovery isn't supported by PmOS. If you really want to use
one anyway, be sure to flash/be on Android 10.

**USING ANDROID 11 IS NOT SUPPORTED**
**I'M NOT RESPONSIBLE OF ANY DAMAGE TO YOUR PHONE**

Recovery:
- [OrangeFox](https://orangefox.download/release/62bb16c36a44bc738419d9bb)
- [Unofficial TWRP](https://mifirm.net/model/dandelion.ttt#twrp)

## Todo

This is a list of things that need to be done to get a bare minimum working
postmarketOS port:
- [x] Unlock bootloader
- [X] Dump partitions
- [X] Dump boot.img
- [X] Get offsets for boot.img
- [X] Build a kernel
- [ ] Get a kernel Booting with proof of booting (UART, led flashing, etc)
- [ ] Get the screen working (pmOS error rootfs not found)
- [ ] Load the rootfs
- [ ] Untethered booting (eMMC boot / SD card boot)

Additional things that need to be done to get a usable postmarketOS port:
- [ ] Touchscreen
- [ ] Sensors
- [ ] Sound
- [ ] Buttons
- [ ] Battery status

Some things that would be nice to have but would require a ton of work and may
not be possible (This depends on the state of the kernel sources):
- [ ] Sleep/Wake
- [ ] Get CPUfreq/cpu scaling working
- [ ] Get the modem (Bluetooth + WiFi + Cellular) working
- [ ] Get the GPS working
- [ ] Get the camera working
- [ ] GPU acceleration ([PowerVR Rogue DRM driver](https://lore.kernel.org/all/20220815165156.118212-2-sarah.walker@imgtec.com/) / Mesa)
- [ ] Mainline kernel port

## Flashing PostmarketOS

**THE DEVICE IS CURRENTLY NOT BOOTING, DO NOT FLASH POSTMARKETOS ON IT!**

See [PMBOOTSTRAP.md](PMBOOTSTRAP.md) for more details.

## License
This work is licensed under the MIT License except otherwise specified.
Please see the [license file](LICENSE) for more information.
