# pmBootstrap

The version of pmbootstrap used for this project is `1.53.0`.

## Install pmbootstrap

You need to install pmbootstrap first, please check the postmarketOS wiki for
more details: https://wiki.postmarketos.org/wiki/Installation_guide

## Dump partitions

Before messing with the phone, you need to dump the partitions using the
`mtkclient` tool:
```bash
# Set your phone in preloader mode (hold volume up + volume down + power)
$ ./mtk r emmc.bin
```
This will dump the whole eMMC to the `emmc.bin` file. Wait until the process is
finished, it can take a while (around ~20 minutes). Keep the phone plugged in
during the whole process.

**Do not forget to archive the `emmc.bin` file somewhere safe!**

## Copy the pmbootstrap layers

Because the device is not supported by pmbootstrap yet, you need to copy the
layers from the pmbootstrap repository to your local pmbootstrap cache:
```bash
# We need to symlink the device and kernel repos to the pmaports tree:
$ ln -s $PWD/linux-xiaomi-dandelion/ /home/$USER/.local/var/pmbootstrap/cache_git/pmaports/device/testing/
$ ln -s $PWD/device-xiaomi-dandelion/ /home/$USER/.local/var/pmbootstrap/cache_git/pmaports/device/testing/
```

## Building the image

Export the image:
```bash
$ pmbootstrap install
$ pmbootstrap export
```
