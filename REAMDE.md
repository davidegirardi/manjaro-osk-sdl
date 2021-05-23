# Work in Progress Notes

## Installation
After installing the package, add the `osk-sdl` hook to `/etc/mkinitcpio.conf`.

## Manual Boot
At the moment, the Pinephone kernel on Manjaro does not load the mali module in the initrd.
The module gets loaded later, when Plymouth runs. I cannot figure out why and how to fix this.

To work around this, the hook provides a fallback to manually decrypting the filesystem.
On my test phone, the encrypted partition is number 3. Here's the code to make the phone boot (basically manually running the steps of the hook):

```shell
source /config
source /init_functions
# Replace mmcblk2p3 with your partition and type your passphrase:
cryptsetup open /dev/mmcblk2p3 cryptroot

fsck /dev/mapper/cryptroot
export root=/dev/mapper/cryptroot
mount $root /new_root/
run_hookfunctions 'run_latehook' 'late hook' $LATEHOOKS
run_hookfunctions 'run_cleanuphook' 'cleanup hook' $CLEANUPHOOKS
rdlogger_stop
exit
```

## Testing osk-sdl While The OS is Running
You can run:

```shell
systemctl stop phosh.service
export TSLIB_TSDEVICE=/dev/input/eventX
export DFBARGS="system=fbdev,no-cursor,disable-module=linux_input"
osk-sdl -d a -n a -c /etc/osk.conf -v
```

