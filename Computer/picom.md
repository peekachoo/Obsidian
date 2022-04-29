- A [[compositor]] software.
- Installation: Arch: `pacman -S picom`
## Configuration
- Default: `/etc/xdg/picom.conf`
- Copy to home directory and edit:
  `cp /etc/xdg/picom/conf ~/.config/picom/picom.conf`
* Change conf file path: `picom --config path/to/picom.conf`
## Add to xinitrc
```
# Start compositor in the backgroun
picom & # or compton &...

# Execute window manager
exec dwm # every line after this exec line is ignored.
```
## Options
- Shadows
- Fading
- Transparency
- Corners
- Bg-blurring
- ...
- 