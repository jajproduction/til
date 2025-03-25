# Natural Scrolling X11

This could help you activate your touchpad on tap and scrolling with two fingers.

`/etc/X11/xorg.conf.d/30-touchpad.conf`

```bash
Section "InputClass"
    Identifier "touchpad"
    Driver "libinput"
    MatchIsTouchpad "on"
    Option "Tapping" "on"
    Option "NaturalScrolling" "on"
EndSection
```
