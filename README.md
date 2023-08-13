# PostmarketOS for Redmi-9A

This repository contains the basis of a PostmarketOS port for the Xiaomi
Redmi 9a smartphone. This phone can be bought for less than 70€ and is a good
candidate for a cheap Linux phone, that's why I'm **trying** to port
PostmarketOS to it.

**Please note this is a work in progress and may not be complete!**

This project may be abandoned at any time, I'm not sure I'll be able to
complete it.

## Technical research

See the [Technical Specifications](SPECS.md) for more details. These are the
results of my research on the phone hardware.

## Unlocking the bootloader

Use the offical [Mi Unlock Tool](https://en.miui.com/unlock/) to unlock the
bootloader (Xiaomi account required). You will have to wait one week before
being able to unlock the bootloader (?!).

If you can't wait one week to unlock the bootloader, you can use the mtkclient
software to unlock the bootloader:
```
# Plug the phone in preloader mode
$ python mtk e metadata,userdata,md_udc
$ python mtk da seccfg unlock
$ python mtk reset
```

## Kernel sources

The kernel sources are available on the Xiaomi Kernel OpenSource Github page,
but I've made a mirror of the sources on this repository for convenience
(here)[https://github.com/SheatNoisette/linux-xiaomi-dandelion]

## Flashing PostmarketOS

@TODO

## License
This work is licensed under the MIT License except otherwise specified.
Please see the [license file](LICENSE) for more information.
