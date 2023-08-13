# pmBootstrap

You need to ln the pmbootstrap layers:
```
# We need to symlink the device and kernel repos to the pmaports tree:
$ ln -s $PWD/linux-xiaomi-dandelion/ /home/$USER/.local/var/pmbootstrap/cache_git/pmaports/device/testing/
$ ln -s $PWD/device-xiaomi-dandelion/ /home/$USER/.local/var/pmbootstrap/cache_git/pmaports/device/testing/
```

Export the image:
```
$ pmbootstrap export
```
