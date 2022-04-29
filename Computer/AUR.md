- Arch User Repository - a community-driven repository for Arch-based distro.
- The AUR doesn't contain prebuilt packages but PKGBUILD which are scripts that you can run with `makepkg` to build a package and then install with `pacman`.
- Users can contribute their own package builds (PKGBUILD) in the AUR and if the pkg is popular enough and there's a Trusted User willing to maintain it, it can enter the official community repository (!= AUR) and is accessible by [[Package Manager|pacman]]
## How to install without a helper:
* Make sure to have base-devel and git installed.
* Installation:
```
git clone https://aur.archlinux.org/package_name.git
cd PACKAGE_NAME
makepkg -si
```
* Update:
```
cd PACKAGE_NAME
git pull
makepkg -si
```
## How to install "yay" (AUR helper)
1. Ensure the `base-devel` and `git` is installed.
   `pacman -S --needed git base-devel`.
2. `git clone https://aur.archlinux.org/yay-git.git`
3. `cd yay-git` -> check to see if PKGBUILD is already created.
4. `makepkg -si` -> run in the same directory with PKGBUILD
	1. `-s/--syncdeps` -> install all needed dependencies and build.
	2. `-i/--install` -> install the built package (same as `pacman -U package_name`). 
## How to install form AUR with "yay"
1. Now download packages by: `yay -S pkg_name`.
2. **Update all installed packages**: `yay -Syu`.
3. **Clean unneeded dependencies**: `yay -Yc`.
## Install a package from AUR
* `yay -S package_name`
## Uninstall a package from AUR (with [[pacman]])
* Since we essentially install with pacman (`makepkg -i` = `pacman -U`), we'll uninstall with it as well:
  `pacman -R package_name` -> remove the package only.
  `pacman -Rs package_name` -> remove the package and all its dependencies that are not required by other packages.
