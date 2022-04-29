- In order to access data in devices in Linux, we have to mount that device on a location on the [[filesystem]] (in the directory tree).
-> Mounting makes data from that a device accessible.
- For ex: when system boots, the root participation (can be any storage device - drive/usb...) is associated with the root of the directory tree -> is mounted on `/`.
- The root directory of the filesystem: mount point.
- For ex: you want to access files on a CD-ROM
	- CD-ROM device: `/dev/cdrom`
	- Chosen mount point: `/media/cdrom`
	- -> `mount /dev/cdrom /media/cdrom`
	- Now the file whose location on the CD-ROM is `/dir/file` is now accessible on your system as `/media/cdrom/dir/file`.
- Command: `mount device dir`
  -> Tells the [[kernel]] to attach the filesystem found on *device* at the directory *dir*.
  -> The mountpoint (`dir`) becomes the root directory of the mounted filesystem.
  -> The previous contents (if any) of *dir* become invisible until this filesystem is [[unmounted]].