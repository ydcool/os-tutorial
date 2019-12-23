*课前预习：linux, mac, terminal, compiler, emulator, nasm, qemu*

**本节目标：安装使用教程的必要软件**

我用 Mac，Linux 也很棒，因为上面已经有一些可以直接拿来用的标准工具。

在 Mac 上，安装 [Homebrew](http://brew.sh) 然后执行 `brew install qemu nasm`

不要用 xcode 的开发者工具 `nasm`，如果你已经安装了他们的话，大多数时候都不能正常使用。请使用 `/usr/local/bin/nasm`

在部分操作系统上，qemu 分成了多个二进制文件，你可以试试 `qemu-system-x84_64 binfile`
