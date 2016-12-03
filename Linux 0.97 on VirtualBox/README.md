# Linux kernel 0.97 on VirtualBox

In this article, it is assumed that you have gone through the previous section of "Linux kernel 0.11 on VirtualBox". So it only states the differences of operations between these two versions.


## Environment
- same

## Prerequisite
- same except
- **linux-0.97.2-080516.zip** - Linux 0.97 source code from  [http://www.oldlinux.org/Linux.old/bochs/linux-0.97.2-080516.zip](http://www.oldlinux.org/Linux.old/bochs/linux-0.97.2-080516.zip)

## Preparation on host computer (Ubuntu)
- similar procedure, with different file names
- download & unzip **linux-0.97.2-080516.zip** : only 3 files are required: **bochsrc-hd.bxrc**; **bootimage-0.97.2.new**; **linux-0.97-hd.img**

## Steps
In this section, I use '$' as prompt when you are at host, and '#' as prompt when you are at linux 0.11 environment under Bochs.

1. Update **bochsrc-hd.bxrc** with the latest syntax requirements by **Bochs 2.6.8** (which changes quite a lot compared to the original file of bochsrc.bxrc)
2. Run **Bochs** and select the file **bochsrc-hd.bxrc** or   
`   $ bochs -f bochsrc-hd.bxrc
`
3. Go back to the root directory of the source code, and compile  
`    # cd /usr/src/linux-mcc  
`

    `# make clean
` 

    `# make
`

4. "Image" file is generated after compilation. Now write it back to floppy of Bochs so we will be able to read it from host computer

    `# dd bs=8192 if=Image of=/dev/fd0
`
5. Switch back to host computer. You will find the file **bootimag-0.97.2.new** has beed updated. Save it with a new name **boot-0.97.img**, with reasons  1. for clariy in naming; 2. VirtualBox requires .img as file name extension. 
6. Edit **boot-0.97.img** file with hexedit. In case you have to install hexedit on Ubuntu

    `    $ sudo apt-get update
`

    `    $ sudo apt-get install hexedit
`
    
7. change the contents of **boot-0.97.img** at locations 0x1FC/0x1FD from 0x00/0x00 to 0x01/0x03, as shown in below picture. (0xNN means the number NN in hexdecimal format)

    `$ hexedit boot-0.97.img
`

![image](https://dl.dropboxusercontent.com/u/26460417/VirtualBox_Ubuntu14.png)


## Preparation on host running VirtualBox
- download & install **VirtualBox**

- Get 2 files ready: 

    - **boot-0.97.img** from previous step
    - **root-0.97.img** (or **linux-0.97-hd.img** from **linux-0.97.2-080516.zip**)

- Convert the root.img to VirtualBox VDI format by issuing the following VirutalBox command

    `	$ VBoxManage convertfromraw --format VDI root-0.97.img root-0.97.vdi
`


## Steps
Follow exactly the same steps as in Linux kernel 0.11 on VirtualBox, by applying names from **boot.img** to **boot-0.97.img**, and **root.img** to **root-0.97.img**










   

 