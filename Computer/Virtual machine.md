* A virtual machine is a virtual computer which uses softwares instead of physical computer components with the help of a [[hypervisor]].
* A virtual machine behaves like an actual machine, it thinks it's a real computer. It's in the matrix!
* How to install a virtual machine:
	1. Enable hardware virtualization support in the BIOS (for x64 only?).
	2. Download the OS (most of the time .iso file).
	3. Download a hypervisor.
	4. Download VirtualBox Extension pack if needed.
	5. Create a new virtual machine in the hypervisor - select the amount of RAM, hard disk (disk type - VDI, dynamically allocated/fixed, disk size). -> Create.
	   You can always go back and change these settings.
	6. After creating, you may want to give your VM a bit more CPU in the settings.
	7. Start the VM then boot from the ISO file just downloaded. 
* Always clone a VM when making critical changes.