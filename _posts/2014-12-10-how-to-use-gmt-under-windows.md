---
title: Windows 下使用 GMT 的正确姿势
date: 2014-12-10
updated: 2015-01-13
author: SeisMan
categories: GMT
tags: [Windows, GMT技巧]
---

我几乎是完全在 Linux 下工作的。有过几次在 Windows 下使用 GMT 的经历，个人觉得用户体验是非常糟糕的，Windows 自带的工具太简陋，用来画 GMT 图太繁琐，浪费好多时间。虽然未来我也几乎不会在 Windows 下写 bat 脚本，但还是想将自己的一些经验写下来，希望能够提高 Windows 下 GMT 的用户体验。

在正式开始本文之前，首先要认清几个基本的事实。如果你无法认同这几个事实，那么就没有再读下去的必要了：

1.  GMT 最初是在 Linux 下开发的 ** 纯命令行 ** 工具。在 Linux 下使用 GMT 要比在 Windows 下方便很多。所以，如果能在 Linux 下使用，就不要在 Windows 下使用；
2.  大多数图都不可能用一个 GMT 命令就完成，因而需要将一系列 GMT 命令写到 bat 脚本中；
3.  将 GMT 命令写入 bat 脚本的目的有两个：首先是记录 GMT 绘图的过程，其次才是批量绘图；
4.  写 bat 脚本的过程，大部分时间和精力都是花在命令的调试和图形的微调上；
5.  花半个小时时间折腾一下工具，就可以换取更好的用户体验以及更高的调试效率，这是一笔很划算的交易；

<!--more-->

## 不用 cmd

点击 “开始”-\>“附件”-\>“命令提示符”（或者点击 “开始”，然后搜索 “cmd”），会出来一个如下图所示的命令提示符窗口，简称为 cmd。

![](/images/2014121001.png)

Windows 下的 GMT 用户，尤其是 GMT 初学者，都会在 cmd 中敲一系列的 GMT 命令来画图。我想，用了几次就会体会到 cmd 的这些让人无法忍受的缺点：

1.  默认的界面又黑又丑，几乎无法自定义；
2.  默认字体完全不适合写脚本，难以区分 1 和 l 等，写脚本的时候容易被坑；
3.  复制粘贴比较麻烦，似乎没有简单的办法完成复制操作，这使得将命令复制到脚本中变得很麻烦；
4.  关闭 cmd 并重启后，前一次的命令历史都没了；

有一些与 cmd 类似的工具，比如 console、console
2、ColorConsole、ConEmu 等，可以完全替代 cmd，同时又有更好看的图形界面以及更丰富的自定义功能。

但是，不建议使用 cmd 以及这些类似的工具。

用 GMT 画图时，通常需要用多个命令绘制一张图，用 cmd 之类的工具写这些命令将会非常痛苦。因为一旦其中任意一个命令出现问题，或者想要微调其中某个命令的某个参数，则必须通过各种方式（一般是通过多次按上下方向键）将命令历史一一调出来并一一重新执行。这个过程非常繁琐、非常浪费时间，出错的概率也很高。

**不要使用 cmd！！！**

**不要使用 cmd！！！**

**不要使用 cmd！！！**

（因为 cmd 太坑，所以重复三遍。）

用 GMT 画图的正确姿势是将绘图所需的 GMT 命令都写到 bat 脚本中，即便某个命令出错或者某个命令需要微调也不用怕了，只是重新执行一下 bat 脚本即可。

## 不要用 notepad

既然是写脚本，就一定要使用文本编辑器。Windows 自带的文本编辑器是 notepad，也就是常说的记事本，也就是下面这货：

![](/images/2014121002.png)

因为实在无法忍受 notepad 那丑陋的默认字体，我把 notepad 的字体改成了等宽的 “Courier New”。

notepad 的缺点实在太多：

1.  没有语法高亮
2.  没有行号
3.  没有智能补全
4.  用 Ctrl+Z 只能撤销最近的一个操作历史

基本上你需要的功能它都没有。当然优点也是有的，比如 “它是系统自带编辑器” 以及“它是一款很简约（简陋？）的编辑器”。

**不要用 notepad 写 bat 脚本。** 它本来就不是一款用于写脚本或代码的编辑器。有很多功能强大的编辑器值得你去用。

## 使用 notepad++

-   不用 notepad，还可以用什么？

    优秀的文本编辑器实在太多。比如 notepad++、sublime text、EditPlus、vim、emacs 等等。除了 vim 和 emacs 学习曲线比较陡峭之外，其余的大多数文本编辑器都是很容易直接上手使用的。

-   为什么要使用 notepad++？

    这里并不是要推荐 notepad++，其他的文本编辑器也可以实现类似的功能，或许可以实现的更好更方便，但我没有时间也没有心思去寻找最好的那一款（其实没有最好只有最适合）。

    我只是想借着 notepad++ 来展示下一个合适的文本编辑器是如何提高写脚本 / 代码的效率的。针对本文的主题，也就是要解释一下，为什么一个好用的文本编辑器可以提高 GMT 绘图时的效率。

-   notepad++ 和 notepad 是什么关系？

    这两个编辑器没有关系，只是恰好名字类似而已。

### 下载与安装

到官方网站下载： <http://notepad-plus-plus.org/>

安装过程没什么可说的。启动之后的界面如下图，代码高亮、行号显示、自动补全默认都实现了：

![](/images/2014121003.png)

对于 bat 脚本，右键，然后 “Edit with notepad++” 即可用 notepad++ 打开脚本。

### 基本的配置

“设置”-\>“首选项” 中提供了一些基本的配置，可以简单配置一下以符合自己的习惯。

“设置”-\>“语言格式设置” 中可以设置字体和字号，以及对各种不同语言做各种自定义。

### 安装插件 NppExec

“插件”-\>“Plugin Manager”-\>“Show Plugin Manager”会打开插件管理器，在 “Available” 标签页中可以找到 notepad++ 的各种插件。

用 notepad++ 写完 bat 脚本之后，就需要执行 bat 脚本以检查命令的正确性以及绘图效果。

最原始也是最常用的做法是鼠标双击 bat 脚本，然后一个黑框一闪而过。。。此时即便命令执行时有输出错误信息，用户也看不到，所以就开始抱怨自己的脚本画不出来图，但是又不懂得提供出错信息。当然这个问题可以解决，在 bat 脚本的最后加上一句 `pause`，则黑框在脚本执行完毕时不会自动关闭，就可以看到输出信息了，只是又要面对那又黑又丑的 cmd，又要面对无法把报错信息复制到 google 里搜索的尴尬。

NppExec 插件可以解决这个问题。安装该插件后（安装过程中需要从 sourceforge 下载数据，有时候该网站会被墙，自己想办法解决），并重启，notepad++ 的界面如下：

![](/images/2014121004.png)

直观地可以看到两个变化：

1.  整个界面被分为上下两个区：文本编辑区和 console 区
2.  工具栏上，在倒数第二的位置出现了一个终端的小图标

写完 GMT 脚本后，Ctrl+S 保存，然后键入 F6，就会出现 “Execute” 对话框如下图：

![](/images/2014121005.png)

在其中输入 `$(FULL_CURRENT_PATH)` ，然后点击 OK，即可执行该 bat 脚本。

**注意**：

在执行 bat 脚本的过程中，可能会出现生成的 PS 文件被放到 notepad++ 的安装文件夹下，或者因为权限问题 “拒绝访问” 的错误，解决办法是在 “插件”-\>“NppExec” 中勾选“Follow
\$(CURRENT\_DIRECTORY)” 选项，并重启 notepad++ 使其生效。该选项的作用是使得在执行 bat 之前，先 cd 到 bat 所在的路径，再执行 bat 脚本中的命令。

执行后的效果如下：

![](/images/2014121006.png)

在 console 中可以看到 bat 脚本中的每个命令的执行，当然，如果命令有错误，也会显示报错信息。这样，在编辑器里就既可以编辑 bat 脚本，也可以执行 bat 脚本，并可以根据终端的输出来判断命令是否有错误以及警告。

如果脚本有问题就需要修改，修改完成后保存，再次键入 F6，又会出现 “Execute” 对话框，`$(FULL_CURRENT_PATH)` 已经输入好了，再点击一次 “OK” 即可再次运行修改后的脚本。不过，按 F6 再点击 OK 还是有些麻烦：当脚本执行过一次之后，可以用快捷键 Ctrl+F6 重新运行脚本。

每次修改代码之后都要先保存再执行也挺麻烦的，最好能够在运行之前自动保存。在 “插件”-\>“NppExec” 中选中 “Save all files on execute” 即可实现每次运行之前自动保存代码。

对于终端，还可以做一些额外的设置，可以在 “插件”-\>“NppExec” 中进一步调整：

1.  “Change Console font” 来挑选一个合适的等宽字体和字号；
2.  一些系统级别的信息对于我来说没有用，所以勾选 “No internal messages”
3.  Ctrl 键和 F6 键离得有些远，按起来还是不太方便：在 “Advanced options” 中，把 “ToolbarBtn” 改成“ExecPre”，则点击工具栏里倒数第二个终端小图标，就相对于执行了 Ctrl+F6，好方便；
4.  “Advanced options” 中还可以改 console 中文本的颜色，这个用默认值就好啦。

console 的输出信息，对于我们测试 bat 脚本是非常重要的，所以会要求输出信息尽量完整且精简。默认的输出不太满意，在 “Console Output Filters” 中做一些修改：

1.  终端的输出信息中有太多空白行，浪费了宝贵的空间，想要把这些空白行都 ** 过滤 ** 掉，在 Filter 标签中修改如下图：

    ![](/images/2014121007.png)

2.  输出信息中每行都有很长的当前路径信息，影响了输出的阅读，而且该路径信息与具体的命令之间没有空格，就更容易混淆了。在 Replace 标签页中，将当前路径都 ** 替换 ** 成 `GMT5>` ，具体如下图：

    ![](/images/2014121008.png)

    需要注意一下， `GMT5>` 的大于号后面有个空格，使得提示符与命令之间更容易区分。

3.  输出信息中包含了命令、错误信息、警告信息以及输出，通常希望将错误、警告以及输出跟命令区分一下。这里的处理方式是，先在 “Advanced Options” 中将设置 console 的输出文本颜色为蓝色：

    ![](/images/2014121009.png)

    然后在 “Highlight” 选项卡中，将以 GMT5 开头的行设置为黑色：

    ![](/images/2014121010.png)

    这样设置之后，所有的命令都是黑色显示，所有的输出、错误、警告都用蓝色显示，当然也可以将错误、警告、输出定义不同的颜色，稍稍麻烦一些，这里就不做了。

经过这么一番配置之后，再次 Ctrl+F6 执行，效果如下：

![](/images/2014121011.png)

这里在命令里加了个输出，并且故意把命令写错了，所以出现了蓝色的输出和报错信息，一眼就可以看到错误信息，看上去更直观。

**注意**: 似乎该插件不会输出 GMT 命令中 `-V` 显示的信息，原因未知。

## PS 查看器

上面已经把编辑器配置得可以方便地编辑、执行脚本，并可以根据输出信息来判断脚本的正误。有些时候脚本是对的，只是绘图的效果不够理想，此时需要不断微调脚本并实时预览 PS 文件。

gsview 是 GMT 官方推荐的 PS 查看器，它可以基本实现 PS 文件的实时预览。这里说 “基本实现”，因为在每次生成 PS 文件后，总是需要将焦点切换到 gsview 软件上，gsview 才会重新载入 PS 文件。不喜欢 gsview 的另一个原因是，gsview 是商业软件，需要注册才可以使用，未注册的软件在每次打开 PS 文件时都会弹出要求注册的对话框，很是烦人。

推荐使用 [SumatraPDF](http://www.sumatrapdfreader.org/free-pdf-reader.html)，一个非常精致小巧的阅读器，支持 PDF、PS、epub 等多种格式。

在我眼中，SumatraPDF 相对于 gsview 的优势在于：

1.  免费软件，不会弹出讨厌的注册对话框
2.  完全自动重载 PS 文件，实时预览 PS 文件，而不是像 gsview 一样需要将焦点切换到软件上才可重载

如果觉得 SumatraPDF 不错，可以将 PS 文件的默认打开方式设置为 SumatraPDF。

默认情况下，SumatraPDF 是不能打开含中文的 PS 文件的，这就需要设置环境变量 `GS_FONTPATH` 为 gs 指定字体的搜索路径。具体步骤是：“我的电脑”上右键点击 “属性”-\>“高级系统设置”-\> 在“高级”选项卡中点击 “环境变量(N)...”-\>“新建” 系统变量 -\>变量名为 `GS_FONTPATH` ，变量值为 `C:\Windows\Fonts`。如果设置后依然无法打开含中文的 PS 文件，可以考虑升级 gs 的版本，gs9.05 和 9.18 经测试都是可以的。

## 效果图

基于以上的一些配置，定制出来一套 Windows 下我觉得很友好也很高效的 GMT 绘图系统（右键查看大图）：

![](/images/2014121012.png)

屏幕左边是编辑器，右边是 PS 阅读器（预览区）。编辑器上边为编辑区，下边为终端区。

试想一下，在编辑区写脚本，写完了 Ctrl+S 保存，然后 Ctrl+F6 执行，眼睛移到终端区看看有没有错误和警告，有的话就修改脚本，重复以上动作，没有的话眼睛瞟一眼预览区，看看最终的绘图效果。整个过程都不需要动一下鼠标，比 cmd、notepad、gsview 之类可高效多了。

## Tips Or Bugs

1.  要使用 SumatraPDF 查看 PS 文件，必须先安装较新版本的 ghostscript；
2.  Notepad++ 默认将文件以 UTF-8 编码保存，因而若需要在 PS 文件中添加中文，则可能会导致乱码；
3.  编辑 bat 文件时应注意 dos 里是没有续行符的，一条命令必须在一行写完。不像 Linux 下的
    `\` 、Fortran90 下的 `&` 和 matlab 下的 `...` 续行；

## 修订历史

-   2014-12-10：初稿；
-   2015-01-13：加入了与 GMT 中文相关的几个注意事项；
-   2015-01-17：NppExec 插件应勾选 “Follow \$(CURRENT\_DIRECTORY)” 选项；Thanks to Joe Wang；
-   2015-01-21：SumatraPDF 查看 PS 文件时依赖于 ghostscript；Thanks to Michael Song；
-   2015-10-13：SumatraPDF 可以查看含中文的 PS 文件；
