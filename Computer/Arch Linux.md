# Arch Linux is the distro for beginners.
## Installation - Base
- Hlyselpful links: [1]([https://itsfoss.com/install-arch-linux/](https://itsfoss.com/install-arch-linux/), [2](https://www.freecodecamp.org/news/how-to-install-arch-linux), [3]([Arch Linux Installation Guide 2020 - YouTube](https://www.youtube.com/watch?v=PQgyW10xD8s))
1. [Arch Linux - Downloads](https://archlinux.org/download/)
2. Verify signature with GnuPG........ (I skipped this step :P).
3. Boot the live environment (via a [[Live USB]], disk,...).
	1. Disable Secure Boot and set up again after completing the installation.
	2. Access [[BIOS]] or [[UEFI]] during [[POST]].
	3. Choose "Arch Linux Install Medium".
	4. Logged in a virtual console as the [[root user]] + [[Zsh]] shell prompt -> you can switch to different console or use nano and vim,...
4. Verify the boot mode: list the efivars directory:
   `ls /sys/firmware/efi/efivars`
   -> If the directory is showed -> UEFI
   -> If not -> BIOS/CSM.
5. Connect to the internet:
	1. Check network interface: `ip link`.
	2. Connect to the network:
		1. Ethernet: plug in the cable.
		2. Wifi: authenticate using [[iwctl]].
	3. Configure your network connection:
		1. DHCP: ~~automatically configured.~~ -> haha no, read troubleshooting [below.
		2. Static IP: [[network manager]] or `dhcpcd`.
	4. Check connection with `ping`.
6. Set [[system time]]: `timedatectl list-timezones` -> `timedatetl set-timezone Europe/Paris`.
7. Partition the disks with `fdisk`.
	1. `fdisk -l` -> list all devices (disks).
	2. Results ending with `rom` `loop` or `airoot` can be ignored.
	3. `fdisk /dev/sda` -> partition the disk `dev/sda`.
	4. Required partitions:
		1. One partition for the root directory `/`.
		2. (UEFI only) One [[UEFI|EFI System Partition]].
			1. If the ESP already exists, do not create another one. It is recommended to delete all partitions and start fresh.
			2. Create a new partition -> `+512M` in size -> change its type to EFI System.
		3. (Optional): home and [[swap partition]] -> these can be created under the root later (others: stacked block devices?)
8. Format partitions (create a [[filesystem]]):
	1. `mkfs.ext4 /dev/root_partition` -> ext4 is a common [[filesystem]] for Linux data partition.
	2. `mkswap /dev/swap_partition` -> format [[swap partition]] if any.
	3. `mkfs.fat -F 32 /dev/efi_partition` -> format the newly created ESP (do not reformatting).
9. Mount the filesystems:
	1. `mount /dev/root_partition /mnt` -> mount the root volume to `/mnt`.
	2. Create mount points and mount the remaining partitions.
	   `mkdir /mnt/boot/efi`-> create mount points.
	   `mount /dev/efi_partition /mnt/boot/efi` -> mount.
	   or: `mount --mkdir /dev/efi_partition /mnt/boot/efi`.
	3. `swapon /dev/swap_partition` -> enable swap volume.
10. Arch Installation:
	1. Download packages from [[mirror]] servers defined in `/etc/pacman.d/mirrorlist` with reflector:
		1. Sync the pacman repo: `pacman -Syy`
		2. Install reflector: `pacman -S reflector`
		3. Backup mirrorlist: `cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak`.
		4. Use reflector to get a good mirror list: `reflector -c "FR" -f 12 -l 10 - n 12 --save /etc/pacman.d/mirrorlist`.
		5. Or edit the existing list: `nano /etc/pacman.d/mirrorlist`.
	2. Install with root mounted (previous step): `pacstrap /mnt base base-devel linux linux-firmware nano vim. 
	3. Additional important packages: `pacstrap /mnt networkmanager git dhclient dhcpcd`
11. Configure the Arch system:
	1. Generate a [[fstab]] file: `genfstab -U /mnt >> /mnt/etc/fstab` -> then check and edit in case of errors.
	2. [[chroot]] into the new system: `arch-chroot /mnt`.
	3. Set time zone: `ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime` (I skipped this).
	4. Localization (language, numbering, date, currency format,...):
		1. Generate the locales: `locale-gen`.
		2. Create `/etc/locale.conf` file and set the LANG variables: `echo LANG=en_US-UTF-8 > /etc/local.conf`
		3. Export environmental variable: `export LANG=en_US-UTF-8`.
		4. [Network Configuration](https://wiki.archlinux.org/title/Network_configuration#Check_the_connection):
			1. Create the hostname file which includes a single line with myHostName: `echo myHostName /etc/hostname`.
			2. Create and configure the hosts file: `touch /etc/hosts`.
			   -> edit the hosts file: `nano /etc/hosts` -> add these lines:
			   `127.0.0.1 localhost
			   `::1 localhost
			   `127.0.1.1 myHostName.localdomain myHostName`. (DHCP)
		5. Set up root password: `passwd`.
		6. Choose and install a [[bootloader]] (GRUB - UEFI systems):
			1. Install grub packages while still using arch-chroot: `pacman -S grub efibootmgr`
			2. Make sure ESP is already mounted (previous step).
			3. Install grub: `grub-install --target=x86_64-efi --bootloader-id=GRUB --efi-directory=/boot/efi`.
			4. Configure grub: `grub-mkconfig -o /boot/grub/grub.cfg`.
12. Install a [[Desktop Environment]] (optional).
13. Unmount the root partition to make sure there's no pending operations: `umount -l /mnt`. -> lazy unmount -> mount after the filesystem is not busy anymore.
14. Exit and reboot: `exit` -> `reboot`.
## Troubleshooting(!!!)
1. "Temporary failure in name resolution" -> network not configured -> can be easily obtained by downloading the package `pacstrap /mnt dhclient dhcpcd` during installation. If not, you can create your own configuration because `systemd-networkd` is already installed with Arch:
   [Fix Arch Linux Network after Rebooting](https://ae1020.github.io/arch-linux-network-after-boot/)
	1. `nano /etc/systemd/network/20-ethernet.network`.
	2. Add: [Source]([systemd-networkd - ArchWiki (archlinux.org)](https://wiki.archlinux.org/title/Systemd-networkd))
	   `[Match] 
	   `Name=enp* 
	   `Name=eth*`
	   `[Network]
	   `DHCP=ipv4`
	3. `systemctl restart systemd-networkd`
	4. `systemctl enable systemd-networkd`
	5. `systemctl enable NetworkManager.service`
2. Create new [[Root user|users]]:
	1. `useradd -m noah` -> `-m` is to create a home directory for this user.
	2. `passwd noah
	3. Add groups where this user belongs to:  `usermod -aG wheel,audio,video,optical,storage noah`
	   -> `-a` : append user...
	   -> `-G`: to group...
	4. Install and edit [[sudo]]: `pacman -S sudo`
	   `EDITOR=nano visudo` -> uncomment wheel group line since `noah` is the member of the [[wheel group]].
## Installation - GUI
- Here we're not gonna install a DE but only a stand-alone WM and some necessary apps.
1. Install X implementation ([[Xorg]]) and graphical drivers (intel, nvidia, amd) and [[xinit]]:
   `pacman -S xorg xorg-xinit xf86-video-fbdev `
2. Install wallpaper app and a [[compositor]] (picom):
   `pacman -S nitrogen picom`.
3. Three tools that must be installed before trying to log in to a new DE or WM: text editor, [[terminal emulator]], web browser.
   `pacman -S vim kitty firefox`
   Other: dmenu and file manager: `pacman -S ranger dmenu`
4. For [[Window Manager|WM]] and [[Terminal Emulator]], we'll install from the [[AUR]] (dwm, dmenu, st, nerd-fonts-mononoki).
5. Edit the xinitrc fiile and run -> see [[xinit]].
   `nitrogen --restore &`
   `picom &`
   `exec dwm/i3` (need to install first)
6. `reboot`
7. On booting, after login: run `startx`

## Update the system
- `pacman -Syu` -> That's all :D
## [[AUR]] - Arch User Repository
## The Arch Wiki Manual
- Always have the Arch and Gentoo Wiki bookmarked no matter which distro you're running.
## Easy way into Arch
- Manjaro (*)
- ArcoLinux
- Antergos
- SwagArch
- ArchLabs