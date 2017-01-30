# JustBoom
## ALSA file for Surround Systems
JustBoomDigi.conf enables passthrough DTS for surround systems. Needs to be saved under /usr/share/alsa/cards

## Rotary encoder volume control
jb-rotary enables control of volume level via the rotary encoder and mute/unmute function via its push button.
###Installation
1. Login via SSH or via the console.
2. Run the following command and the JustBoom rotary and push button code will be configured and installed: 
```bash
curl -sSL https://pisupp.ly/jb-rotarycode | sudo bash
```
###Usage
The default settings for the script are:
* Start Volume = 0
* Volume increment/decrement steps = 1
* Rotary pins = 16,18 (Board notation)
* Button pin = 10 (Board notation)

Script usage:
```
Usage:  jb_rotary [-sirbv]
        jb_rotary {-h|--help}         Script usage information

        -s --startvol    start volume level
        -i --volinc      volume increments/decrements
        -r --rotary      rotary encoder pins
        -b --button      button pin
```
Example:

```
python jb-rotary -s 20 -5         Changes the starting volume and step increments
python jb-rotary -r 19,21 -b 15   Remaps the rotary and the button pins
```

Note that the default setting for the button requires to disable the onboard UART. This is mostly required when using the rotary encoder with the JustBoom Amp HAT via the P2 connector. [Check our main site JustBoom.co for the full pinout](https://www.justboom.co/technical-guides/boards-pinout/).

### Disable the UART on Raspberry Pi Zero, A+, B+ and 2B
on the command line execute these two commands:
``` bash
sudo systemctl stop serial-getty@ttyAMA0.service
sudo systemctl disable serial-getty@ttyAMA0.service
```
reboot the system.

### Disable the UART on Raspberry Pi 3B
on the command line execute these two commands:
``` bash
sudo systemctl stop serial-getty@ttyS0.service
sudo systemctl disable serial-getty@ttyS0.service
```
and remove the following line from /boot/cmdline.txt
```
console=serial0,115200
```
reboot the system

## LIRC lircd.conf
This is the configuration file for the JustBoom IR Remote to be used in conjunction with LIRC.
A tutorial that guides you through the whole installation of LIRC and the remote configuration can be found via [this link](https://www.justboom.co/tutorials/configure-justboom-ir-remote-lirc/).
