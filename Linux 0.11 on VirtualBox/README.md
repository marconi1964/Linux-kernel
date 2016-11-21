# Linux Kernel 0.11 on VirtualBox

There are many documents about Linux 0.11 running on Bochs, Qemu. But I see no one doing it on VirtualBox. It can be simple and straightforward, though still took me some time to get it right.

The purpose is to get Linux 0.11 run under VirtualBox. It contains 2 files: boot.img (on floppy) and root.img (on HDD).

I use Ubuntu as host computer to run Bochs, so I can update and compile the Linux 0.11 source code, to get boot.img. Togethe with root.img from original download, I run VirtualBox (on any machine, in my case, it is MacBook Pro.) with what-just-compiled boot.img on floppy drive, and root.img on HDD drive. So I can do whatever I want to do with Linux 0.11 on VirtualBox, not the Bochs I am not familar with. 

## Environment
- **Ubuntu 14.04** (running Bochs with Linux 0.11 source code compile)
- **MacOS El Captain** (running VirtualBox with Linux 0.11)

## Prerequisite
- **Bochs 2.6.8** - http://bochs.sourceforge.net
- **linux_devel_040329.zip** - Linux 0.11 source code from http://www.oldlinux.org
- **VirtualBox 5.0.16** - https://www.virtualbox.org

## Preparation on host computer (Ubuntu)
- download & install **Bochs**
- download & unzip **linux_devel_040329.zip** : only 3 files are required: **bochsrc-hd.bxrc**; **bootimage-0.11** > **boot.img**; **hdc-0.11.img** > **root.img**

## Steps
1. Update **bochsrc-hd.bxrc** with the latest syntax requirements by **Bochs 2.6.8** (which changes quite a lot compared to the original file of bochsrc.bxrc)
2. Run **Bochs** and select the file **bochsrc-hd.bxrc** or   
`   $ bochs -f bochsrc-hd.bxrc
`
3. 