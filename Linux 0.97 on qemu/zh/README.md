# 在 qemu 上安裝 Linux kernel 0.97

我不太熟悉 qemu. 只是嘗試重複其他人在 qemu 上安裝、執行 Linux 0.11.<br>很顯然地, 許多網路上的中文說明都是同一個來源, 同一個錯誤. 所以, 就自己動手, 確定可以正確安裝、執行.

如果你已經完成 Linux kernel 0.97 on VirtualBox 這段的後, 可以直接跳到下一段 **"Preparation on host running qemu"** .

## 環境設定

- 同 "Linux kernel 0.97 on VirtualBox"

## 事前準備

- 同 "Linux kernel 0.97 on VirtualBox", 除了
- **linux-0.97.2-080516.zip** - Linux 0.97 source code from  [http://www.oldlinux.org/Linux.old/bochs/linux-0.97.2-080516.zip](http://www.oldlinux.org/Linux.old/bochs/linux-0.97.2-080516.zip)

## 在主機 (host) 上的準備工作 (基於 Ubuntu)

- 類似 "Linux kernel 0.97 on VirtualBox" 程序, 只是使用不同的檔案名稱
- 下載並解壓縮檔案 **linux-0.97.2-080516.zip** : 我們需要以下 3 個檔案: **bochsrc-hd.bxrc**; **bootimage-0.97.2.new**; **linux-0.97-hd.img**

## 步驟 1

- 跟 "Linux kernel 0.97 on VirtualBox" 同樣步驟

## 在主機 (host) 上執行 qemu

- 下載並執行 **qemu**

- 準備好以下 2 個檔案:

    - **boot-0.97.img** 從上一個步驟取得
    - **root-0.97.img** (or **linux-0.97-hd.img** from **linux-0.97.2-080516.zip**)

## 步驟 2

(參考文件 #1, 需注意以下修正)

### qemu

執行 qemu 來模擬 Linux 0.97 系統, 選擇 floppy disk 檔案: boot-0.97.img, 跟硬碟 HDD 檔案: root-0.97.img

`$ qemu-system-i386 -m 16M -boot a -fda boot-0.97.img -hda root-0.97.img`

### 執行 qemu + gdb

Qemu 模擬系統 (qemu emulation system) 結合 gdb (GNU Debugger) 後更強大, 所以, 我們執行 qemu 時會設定 gdb 為 enabled.

1. `$ qemu-system-i386 -m 16 -boot a -fda boot-0.97.img -hda root-0.97.img -S -s`

或者

1. `$ qemu-system-i386 -m 16 -boot a -fda boot-0.97.img -hda root-0.97.img -S -gdb tcp::1234`

參照參考文件  #2 對於 qemu gdb 有更多的說明

-s

-gdb tcp::1234 的縮寫, 也就是 打開 gdbserver TCP port 1234.

如果參考其它文章, 要你執行以下執行時, 都會在這裡出現錯誤訊息, 實際上,  -s 跟 -gdb  這 2 個選項其中一個是多餘的.

`$ qemu-system-i386 -m 16 -boot a -fda boot-0.97.img -hda root-0.97.img -S -s -gdb tcp::1234`

成功執行後, 系統會冒出一個新的螢幕, 一開始是全黑, 等著 gdb 接受鍵盤指令.

打開新的 terminal 執行 gdb

`$ gdb`<br> 3. `(gdb) target remote localhost:1234`<br> 4. `(gdb) c`

(gdb) 下的 'c' 指令意思是 - 繼續 'continue'

5. 可以執行了, 之後, 可以隨時下 gdb 的指令來中斷, 或持續執行.

## 參考文件

1. [https://wwssllabcd.github.io/blog/2012/08/03/compile-linux011/](https://wwssllabcd.github.io/blog/2012/08/03/compile-linux011/)

2. [qemu document - gdb usage](http://wiki.qemu.org/download/qemu-doc.html#gdb_005fusage)
