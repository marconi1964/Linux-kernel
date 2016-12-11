# Linux kernel 0.97 on qemu

I am not familiar with qemu. Try to replicate what people have done of running Linux 0.11 on qemu. However, it seems that many of searched Chinese documents coming from the same source, containing the same mistake. So document it with correction to make sure it works properly.

If you follow the previous section of Linux kernel 0.97 on VirtualBox, you can go straight to **"Preparation on host running qemu"** section. 


## Environment
- same as in "Linux kernel 0.97 on VirtualBox"

## Prerequisite
- same as in "Linux kernel 0.97 on VirtualBox", except
- **linux-0.97.2-080516.zip** - Linux 0.97 source code from  [http://www.oldlinux.org/Linux.old/bochs/linux-0.97.2-080516.zip](http://www.oldlinux.org/Linux.old/bochs/linux-0.97.2-080516.zip)

## Preparation on host computer (Ubuntu)
- similar procedure, with different file names
- download & unzip **linux-0.97.2-080516.zip** : only 3 files are required: **bochsrc-hd.bxrc**; **bootimage-0.97.2.new**; **linux-0.97-hd.img**

## Steps

- same steps as in "Linux kernel 0.97 on VirtualBox"


## Preparation on host running qemu
- download & install **qemu**

- Get 2 files ready: 

    - **boot-0.97.img** from previous step
    - **root-0.97.img** (or **linux-0.97-hd.img** from **linux-0.97.2-080516.zip**)



## Steps
(Check reference #1 in Chinese, with correction)

### qemu

Run qemu to emulate the Linux 0.97 system with floppy disk from file: boot-0.97.img, and HDD from file: root-0.97.img 

`$ qemu-system-i386 -m 16M -boot a -fda boot-0.97.img -hda root-0.97.img
`

### qemu + gdb

Qemu emulation system is much more powerful with gdb (GNU Debugger). We run qemu with gdb enabled.

1. `$ qemu-system-i386 -m 16 -boot a -fda boot-0.97.img -hda root-0.97.img -S -s`

OR

1. `$ qemu-system-i386 -m 16 -boot a -fda boot-0.97.img -hda root-0.97.img -S -gdb tcp::1234`


See reference qemu document (reference #2) for more detail explanation  

-s  

Shorthand for -gdb tcp::1234, i.e. open a gdbserver on TCP port 1234 (see gdb_usage).  

You will get error message if you input as follows, as it is duplicated to have both -s and -gdb options:  

`$ qemu-system-i386 -m 16 -boot a -fda boot-0.97.img -hda root-0.97.img -S -s -gdb tcp::1234`  

Once successfully launched, it will launch a new screen. The screen is black as it is STOPPED, and waiting for gdb to input the command to proceed.  

![image](https://dl.dropboxusercontent.com/u/26460417/qemu_gdb_stopped.png)
2. Open a new terminal windows, and run gdb    

`$ gdb`  
3. `(gdb) target remote localhost:1234`  
4. `(gdb) c`  

![image](https://dl.dropboxusercontent.com/u/26460417/qemu_gdb_running.png)
5. It works, and you may still interrupt with gdb command as you wish



## Reference
1. [https://wwssllabcd.github.io/blog/2012/08/03/compile-linux011/](https://wwssllabcd.github.io/blog/2012/08/03/compile-linux011/)

2. [qemu document - gdb usage](http://wiki.qemu.org/download/qemu-doc.html#gdb_005fusage)










   

 