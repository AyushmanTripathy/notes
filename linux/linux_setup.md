## PACMAN

in /etc/pacman.conf uncomment the line

```
#ParallelDownloads = 5
```

## Yay

```
git clone https://github.com/Jguer/yay --depth 1
cd yay
makepkg -si
```

## TIME

add cron task for every minute

```
pkill -RTMIN+9 dwmblocks
```

## Docker

re login after, adding user to docker group

```
sudo usermod -aG docker ayush
```

## BRIGHTNESS

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

## BLUETOOTH

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

## TOUCHPAD

required package: `libinput`

note: `xf86-input-synaptics` is something
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
        Option "FingerLow" "10"
        Option "FingerHigh" "30"
        Option "MaxTapTime" "125"
EndSection
```

## EMOJIS

required packages: `noto-fonts-emoji`
required packages: `noto-fonts` (other languages)

## NOTIFICATION

required packages: `libnotify`, `dunst`

## CRONJOBS

required packages: `cronie`

```
systemctl enable cronie
systemctl start cronie
```

## Fonts

-   put your fonts in `/usr/share/fonts`
-   to install

```
sudo fc-cache -fv
```

-   to preview use `display`

## FileSystem Tools

change permission for /media `chown -R ayush:ayush /media`

1. gparted
1. exfatprogs
1. dosfstools
1. ntfsprogs

1. jmtpfs (aur)

## Discord

-   in `.config/discord/settings.json`

```
"SKIP_HOST_UPDATE": true,
```

## Other Packages I use

#### wm

1. dwm [window manager]
1. dmenu [input?]
1. dwmblocks [status bar]

#### gui programs

1. chromium [web browser]
1. mpv [media player]
1. sxiv [image viewer]
1. alacrity [terminal emulator]
1. pinta [image editor]

#### tui programs

1. neovim [text editor]
1. moc [music player]
1. htop [task manager]
1. man [docs]

#### tools

1. slock [lock screen]
1. tree [listing directories]
1. pandoc [opening .docx, .pptx]
1. openssh [ssh client and daemon]
1. sshfs [mounting remote directories]
1. yay [AUR package manager]
1. scrot [screen shot]
1. slop [mouse selection]
1. udisks2 [usb ejection]
1. zip and unzip [working with .zips]
1. fzf [fuzzy finder]
1. qrencode [qrcodes]

1. xdotool [automations]
1. xclip [clipboard]
1. xwallpaper [wallpaper]

#### daemons

1. picom [compositor]
1. pipewire [audio]
1. networkmanager [networking]
1. dunst & libnotify [notifications]
1. bluez & bluez-utils [bluetooth]
1. cronie [cronjobs]

#### fun

1. sl
1. cmatrix

#### programming

1. nodejs [from nvm]
1. pip [package manager for python]
1. nodemon, live-server & editmd [from npm]
