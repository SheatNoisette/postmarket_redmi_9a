# PostmarketOS for Redmi 9a

This repository contains the basis of a PostmarketOS port for the Xiaomi
Redmi 9a smartphone.

Please note this is a work in progress and may not be complete
---

## Technical research

See the [Technical Specifications](SPECS.md) for more details.

## Unlocking the bootloader

Use the offical [Mi Unlock Tool](https://en.miui.com/unlock/) to unlock the 
bootloader.

If you can't wait one week to unlock the bootloader, you can use the mtkclient
software to unlock the bootloader:
```
# Plug the phone in preloader mode
$ python mtk e metadata,userdata,md_udc
$ python mtk da seccfg unlock
$ python mtk reset
```

## Flashing PostmarketOS

@TODO

## License
This work is licensed under the MIT License except otherwise specifified.
Please see the [license file](LICENSE) for more information.
