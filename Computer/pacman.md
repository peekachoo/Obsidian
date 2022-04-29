## [Pacman](https://wiki.archlinux.org/title/pacman)
- The package manager of Arch:
- `pacman -S -needed pkg_name`
	- `-S` -> sync
	- `--needed` -> not re-install if the package is already installed.
- `pacman -F file_name` -> **find** out which package provides the file.
- `pacman -U name` -> **install** a 'local' package that is not from a remote repository ([[AUR]]).
- `pacman -R package_name` -> **remove** the package only.
  `pacman -Rs package_name` -> remove the package and all its dependencies that are not required by other packages.
  `pacman -Rsun package_name` -> remove everything including conf files.
- **Update** every packages: `pacman -Syu`