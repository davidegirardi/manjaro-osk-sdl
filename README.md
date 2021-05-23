# Work in Progress Notes

## Installation
After installing the package, modify `/etc/mkinitcpio.conf` as follows.

Force adding the panel module to the initramfs:
```
MODULES=(panel_sitronix_st7703)
```

Add the `osk-sdl` hook:
```
HOOKS=(base udev autodetect modconf block filesystems keyboard osk-sdl fsck bootsplash-manjaro)
```
