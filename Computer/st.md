1. git clone https://git.suckless.org/st
2. cd st
3. sudo make clean install
4. Configuration with `config.h`
5. Defaults are stored in `config.def.h` -> patches apply their config changes here.
6. Patching:
	1. Download [patches](https://st.suckless.org/patches/) into the st folder (consider creating a subfolder: patches).
	2. `patch --merge -i /path/to/patch.diff` -> merge conflict if there's any.
	3. `rm -rf config.h && sudo make clean install` -> generate a new up-to-date config file and rebuilt.
 