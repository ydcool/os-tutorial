系统编程指南
===========

如何从零开始创建一个操作系统！

一直以来我想学习如何从头开始构建一个操作系统。在大学里我学习了如何实现高级特性（如分页，信号量，内存管理等），
但是：

- 我还从来没有真正地搞过自己的引导扇区。
- 大学课程很难，学的东西基本上都还给老师了。
- 我受不了那些整天叫嚣着学习操作系统就应该从阅读一个现有的内核源码开始的人，不管那些内核有多么迷你。

受 [这个文档](http://www.cs.bham.ac.uk/~exr/lectures/opsys/10_11/lectures/os-dev.pdf) 和 [OSDev wiki](http://wiki.osdev.org/) 的启发，我在这里试着一步一步地整理出简要的指南和简明的示例代码。说实话，本教程实际上是第一个文档，但会分成多个小部分，没有长篇大论。

更新: 扩展阅读: [系统开发简明指南](https://littleosbook.github.io),
[JamesM 的内核开发教程](https://web.archive.org/web/20160412174753/http://www.jamesmolloy.co.uk/tutorial_html/index.html)


内容提要
--------

- 本教程是一本为那些有志于研究系统底层技术的人的编程指南。例如对操作系统的工作原理有强烈的好奇心但是没有充分的时间或精力去通读 Linux 内核源码的程序员。
- 这里面没有什么高深的理论。这是本教程的一大特色。谷歌才是你的理论导师，一旦离开校园，那些掉书袋的理论没有也罢。
- 这个教程短小精悍，可能你只需花 5 到 15 分钟就能搞定。相信我，你可以的！

如何使用本教程
------------------------

1. 请从第一个文件夹开始，依次往后看。每一节都是以之前的代码为基础，因此如果你直接跳到 05 节然而发现对 `mov ah, 0x0e` 一脸懵，那是因为你漏掉了 02 节的内容。
讲真，按顺序来吧，遇到你熟悉的内容尽管跳过。

2. 打开 README 并认真阅读第一行，其中详细列出了在你开始动手写代码前应当熟知的一些概念。不清楚的请自行谷歌。 第二行阐明了每节课的目标。仔细阅读这些内容，你会明白为何这样做以及如何做。 “为何” 和 “如何” 同样重要。
 
3. 阅读剩下的内容。**非常简洁**。

4. (可选) 读完 README 之后尝试自己动手编写那些代码。

5. 阅读那些代码示例。里面注释写的非常详尽。

6. (可选) 拿它们做实验，试着搞点突破。检查姿势是否真正理解某事的唯一途径就是尝试突破他，或者用另外的命令（方式）重构他。

太长不看版：首先阅读每个文件夹下面的 README 说明文档，然后是示例代码。只要你有足够信心，就自己把代码实现出来。


规划
--------

我们想让自己的操作系统实现很多功能：

- 从零引导系统，不用 GRUB - ✅已完成！ 
- 进入 32 位模式 - ✅已完成！
- 从汇编转到 C 语言 - ✅已完成！
- 中断处理 - ✅已完成！
- 屏幕输出和键盘输入 - ✅已完成！
- 实现一个极简的基础的并能根据我们的需求不断完善的 `libc` - ✅已完成！
- 内存管理 
- 实现一个文件系统来存储文件
- 实现一个极简的命令行
- 用户模式
- 可能会实现一个简单的文本编辑器
- 多进程以及调度

我们大概会按照这个流程走一遍，不过现在也很难说。

有信心的话，我们还可以做到：

- 一个基本的解释器，70 年代的那种！
- 图形界面！
- 网络！

参与贡献
------------

这是一个个人学习的项目，虽然很久没更新了，我还是希望有朝一日能重拾它。

非常感谢所以提出 BUG 以及提交 PR 的人。我需要点时间来回顾这一切，现在没法保证。

请随意 fork. 如果有不少人有兴趣继续这个项目，尽管告诉我，我会从这里链接一个 “主分支” 过去。