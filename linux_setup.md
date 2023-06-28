TIME
----

add cron task for every minute

```
pkill -RTMIN+9 dwmblocks
```

BRIGHTNESS
----------

1. add rule to udevs

in /etc/udev/rules.d/backlight.rules

```
SUBSYSTEM=="backlight", ACTION=="add", \
  RUN+="/bin/chgrp video /sys/class/backlight/intel_backlight/brightness", \
  RUN+="/bin/chmod g+w /sys/class/backlight/intel_backlight/brightness"
```

2. add user to video group

```
groups <username> //shows groups a user is part of
sudo usermod -a -G video <username>
```

3. reboot

BLUETOOTH
---------

required package: `bluez`, `bluez-utils`

1. add in /etc/bluetooth/main.conf

```
Expreimental=true
```

2. start service

```
systemctl enable bluetooth
systemctl start bluetooth
```

TOUCHPAD
--------
required package: `xf86-input-synaptics`

in /etc/X11/xorg.conf.d/70-synaptics.conf

```
Section "InputClass"
    Identifier "touchpad"
    Driver "synaptics"
    MatchIsTouchpad "on"
        Option "TapButton1" "1"
        Option "TapButton2" "3"
        Option "TapButton3" "2"
        Option "VertEdgeScroll" "on"
        Option "VertTwoFingerScroll" "on"
        Option "HorizEdgeScroll" "on"
        Option "HorizTwoFingerScroll" "on"
        Option "CircularScrolling" "on"
        Option "CircScrollTrigger" "2"
        Option "EmulateTwoFingerMinZ" "40"
        Option "EmulateTwoFingerMinW" "8"
        Option "CoastingSpeed" "0"
        Option "FingerLow" "30"
        Option "FingerHigh" "50"
        Option "MaxTapTime" "125"
EndSection
```

CRONJOBS
--------

using: cronie

```
systemctl enable cronie
systemctl start cronie
```
NOTIFICATION
------------
required packages: `libnotify`, `dunst`
