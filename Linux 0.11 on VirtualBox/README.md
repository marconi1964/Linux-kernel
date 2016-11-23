# Linux Kernel 0.11 on VirtualBox

There are many documents about Linux 0.11 running on Bochs, Qemu. I saw no one doing it on VirtualBox. It can be simple and straightforward, though still took me some time to get it right.

The purpose is to get Linux 0.11 run under VirtualBox. It contains 2 files: boot.img (on floppy) and root.vdi (on HDD).

I use Ubuntu as host computer to run Bochs, so I can modify and compile the Linux 0.11 source code, to get boot.img. Togethe with root.img from original download, I run VirtualBox with what-just-compiled boot.img on floppy drive, and root.img on HDD drive. So I can do whatever I want to do with Linux 0.11 on VirtualBox, not the Bochs I am not familar with. 

## Environment
- **Ubuntu 14.04** (running Bochs with Linux 0.11 & source code)
- **MacOS El Captain** (running VirtualBox with Linux 0.11 & source code)

## Prerequisite
- **Bochs 2.6.8** - [http://bochs.sourceforge.net](http://bochs.sourceforge.net)
- **linux-0.11-devel-040329.zip** - Linux 0.11 source code from  [http://www.oldlinux.org/Linux.old/bochs/linux-0.11-devel-040329.zip](http://www.oldlinux.org/Linux.old/bochs/linux-0.11-devel-040329.zip    )
- **VirtualBox 5.0.16** - [https://www.virtualbox.org](https://www.virtualbox.org)

## Preparation on host computer (Ubuntu)
- download & install **Bochs**
- download & unzip **linux_devel_040329.zip** : only 3 files are required: **bochsrc-hd.bxrc**; **bootimage-0.11**; **hdc-0.11.img**

## Steps
1. Update **bochsrc-hd.bxrc** with the latest syntax requirements by **Bochs 2.6.8** (which changes quite a lot compared to the original file of bochsrc.bxrc)
2. Run **Bochs** and select the file **bochsrc-hd.bxrc** or   
`   $ bochs -f bochsrc-hd.bxrc
`
3. You will be at the directory of /usr/root after boot from Linux 0.11. change directory to /usr/src/linux/kernel/blk_drv and modify hd.c
 (reference: [https://virtuallyfun.superglobalmegacorp.com/2010/08/13/great-resource-for-ancient-linux/](https://virtuallyfun.superglobalmegacorp.com/2010/08/13/great-resource-for-ancient-linux/)) 
4. Go back to the root directory of the source code, and compile  
`    $ cd /usr/src/linux  
`

    `$ make clean
` 

    `$ make
`

    (Several Makefiles need to be updated if you not using the root.img here, but using the original hdc-0.11.img. [http://11210601.blog.51cto.com/11200601/1744524](http://11210601.blog.51cto.com/11200601/1744524)
)
5. "Image" file is generated after compilation. Now write it back to floppy of Bochs so we will be able to read it from host computer

    `$ dd bs=8192 if=Image of=/dev/fd0
`
6. Switch back to host computer. You will find the file **booting-0.11** has beed updated. Save it with a new name **boot.img**, with reasons  1. for clariy in naming; 2. VirtualBox requires .img as file name extension. 

## Preparation on host running VirtualBox
- download & install **VirtualBox**

- Get 2 files ready: 

    - **boot.img** from previous step
    - **root.img** (or **hdc-0.11.img** from **linux_devel_040329.zip**)

- Convert the root.img to VirtualBox VDI format by issuing the following VirutalBox command

    `	$ VBoxManage convertfromraw --format VDI root.img root.vdi
`


## Steps
1. Launch VirtualBox
2. Select - New
![image](https://dl.dropboxusercontent.com/u/26460417/VB_linux_0_11_01.jpg)

3. 











   

 