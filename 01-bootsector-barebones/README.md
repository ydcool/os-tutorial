<!-- 
*Concepts you may want to Google beforehand: assembler, BIOS*
-->
*课前预习： assembler, BIOS*

<!--
**Goal: Create a file which the BIOS interprets as a bootable disk**
-->
**本节目标：创建一个可被 BIOS 识别为可引导磁盘的文件**

<!--
This is very exciting, we're going to create our own boot sector!
-->
真是令人激动，我们要创建一个自己的引导扇区了！

<!--
Theory
-->
理论知识
------

<!-- 
When the computer boots, the BIOS doesn't know how to load the OS, so it
delegates that task to the boot sector. Thus, the boot sector must be
placed in a known, standard location. That location is the first sector
of the disk (cylinder 0, head 0, sector 0) and it takes 512 bytes.
-->
当计算机启动时，BIOS 不知道如何加载操作系统，所以它将该任务委托给启动扇区。因此，引导扇区必须是放置在已知的标准位置。那个位置是第一段的磁盘(柱面0，磁头0，扇区0)，它需要 512 字节。

<!--
To make sure that the "disk is bootable", the BIOS checks that bytes
511 and 512 of the alleged boot sector are bytes `0xAA55`.
-->
为确保该磁盘是可引导的，BIOS 会检查引导扇区 511 和 512 字节数据为 `0xAA55`。

<!--
This is the simplest boot sector ever:
-->
这是一个最简单的引导扇区：

```
e9 fd ff 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
[ 29 more lines with sixteen zero-bytes each ]
00 00 00 00 00 00 00 00 00 00 00 00 00 00 55 aa
```

<!--
It is basically all zeros, ending with the 16-bit value
`0xAA55` (beware of endianness, x86 is little-endian). 
The first three bytes perform an infinite jump
-->
可以看到这个例子里面基本上都是零值，以 16 bit 的 `0xAA55` 结尾（注意字节序，x86 是小端）。前三字节执行一个无限跳转。

<!--
Simplest boot sector ever
-->
最简单的引导扇区
-------------------------

<!--
You can either write the above 512 bytes
with a binary editor, or just write a very
simple assembler code:
-->
您可以使用一个二进制编辑器编写上面的 512 字节，或者只需写一个非常简单的汇编代码:

```nasm
; Infinite loop (e9 fd ff)
loop:
    jmp loop 

; Fill with 510 zeros minus the size of the previous code
times 510-($-$$) db 0
; Magic number
dw 0xaa55 
```

<!--
To compile:
-->
编译：
`nasm -f bin boot_sect_simple.asm -o boot_sect_simple.bin`

<!--
> OSX warning: if this drops an error, read chapter 00 again
-->
> OSX 用户注意：如果编译报错，再复习一下第 00 节。 

<!--
I know you're anxious to try it out (I am!), so let's do it:
-->
我知道你现在已经迫不及待想亲自试一把了（和我一样！），那么我们就开始吧：

`qemu boot_sect_simple.bin`

<!--
> On some systems, you may have to run `qemu-system-x86_64 boot_sect_simple.bin` If this gives an SDL error, try passing the --nographic and/or --curses flag(s).
-->
> 在某些操作系统上，可能需要运行 `qemu-system-x86_64 boot_sect_simple.bin`。如果行命令报出了一个 SDL 错误，尝试传递 ——nographic 和/或 ——curses 参数标志。

<!--
You will see a window open which says "Booting from Hard Disk..." and
nothing else. When was the last time you were so excited to see an infinite
loop? ;-)
-->
你会看到一个窗口打开，上面写着 “Booting from Hard Disk...“ 然后就没有然后了。你上一次见识到死循环是什么时候? :-)