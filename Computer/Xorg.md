- On Unix-like OS, Xorg is the executable/implementation of [[The X Window System]].
- Install: 
	1. Arch: `pacman -S xorg-server`.
	2. Additional: `pacman - S xorg-apps` or `pacman -S xorg`.
	3. Install graphic design: 
		1. Check graphics card: `$ lspci -v | grep -A1 -e VGA -e 3D` -> Subsystem..
		2. [Install an appropriate driver]([Xorg - ArchWiki (archlinux.org)](https://wiki.archlinux.org/title/xorg#Installation)): `pacman -Ss xf86-video`.
- Configure:
	- Edit the file ~/.xinitrc.
- Usage:
	- `startx`
	- How to *startx* automatically after logging in:
	  `nano ~/.bash_profile`
	  add: 
	  `[[ $(fgconsole 2>/dev/null) == 1 ]] && exec startx -- vt1` (every space is required).