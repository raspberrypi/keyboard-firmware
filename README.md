# keyboard-firmware
This repository contains the [QMK](https://github.com/raspberrypi/qmk) firmware binaries for the (RP2040-powered) keyboards in the Raspberry Pi 500
and 500+, and a script for updating the firmware.

## rpi-keyboard-fw-update

### Installation
If `rpi-keyboard-fw-update` isn't already installed, install it with:
```
sudo apt update && sudo apt install rpi-keyboard-fw-update
```

### Usage
Running `rpi-keyboard-fw-update -h` will display:
```
rpi-keyboard-fw-update [options]

Update the firmware in a Pi 500 or Pi 500+ keyboard.

Options:
   -f <FILE> Use the specified UF2 file (skips model auto-detection).
   -h Display this usage message.
   -i Ignore version checks and always update firmware.
   -s Silent mode.
   -v Detect keyboard type and firmware version.
   -w Wipe entire flash before updating firmware.
```
The `-h` and `-v` options don't require `sudo`, all other usages of the script do. The simplest way to invoke the script is to run just:
```
sudo rpi-keyboard-fw-update
```
and this will automatically detect which version of Raspberry Pi 500/500+ you're using, which layout is required, and which firmware-version
is currently installed. If your keyboard firmware is already up-to-date it'll tell you "Your keyboard firmware is already up to date", but
if your keyboard firmware is out of date, it'll automatically be updated to the latest version.

To ignore the version-checks and _always_ upgrade your keyboard-firmware to the latest version, run:
```
sudo rpi-keyboard-fw-update -i
```

To see more details about which version of Raspberry Pi 500/500+ you're using, which layout is required, and which firmware-version is currently
installed, run:
```
rpi-keyboard-fw-update -v
```
which might print out something like:
```
DT_MODEL: Raspberry Pi 500 Rev 1.0
MODEL_VARIANT: pi500plus
DT_COUNTRY_CODE: 1
CC_LAYOUT: ISO
DETECTED_PI500_KEYBOARD: 0
DETECTED_PI500PLUS_KEYBOARD: 1
DETECTED_PI500PLUS_KEYBOARD_VARIANT: ISO
DETECTED_KEYBOARD_FIRMWARE_VERSION: 1.00
```

The current "illumination mode" and "colour" of the Raspberry Pi 500+ LEDs are stored in Flash, but in an area outside of that used by the firmware
(which means these settings will be retained when you upgrade to a newer firmware version). Use the `-w` option to clear these settings (you may
need to combine this with the `-i` option if your firmware is already up to date) whilst updating your firmware.

If you want to flash your own custom firmware instead of the pre-supplied firmware, then this can be done wih the `-f` option, which automatically
skips the model, layout and version-detection steps. Be warned that if your custom keyboard firmware is faulty or non-functional, the keys in your
keyboard might not work, and so you'd need to use an external USB keyboard (plugged into one of the USB ports on the Raspberry Pi 500/500+) in
order to run `rpi-keyboard-fw-update` again and flash a working firmware version.
