- A program allowing to manually start [[Xorg]], WM or DE.
- Installation: `pacman -S xorg-xinit`.
- Configuration:
	- startx and xinit take argument -> if not provided it will look for ~/.xinitrc to run as a startup shell script.
	- Set up ~/.xinitrc to run programs and set environment variables on X server startup:
		- If it is not present in the home dir startx will run the default (twm, xorg-xclock, xterm): /etc/X11/xinit/xinitrc.
		- -> To run WM or DE of choice: `cp /etc/X11/xinit/xinitrc ~/.xinitrc` or `/home/noah/.xinitrc`.
		  -> Edit the file.
  * Run: `startx`.
	