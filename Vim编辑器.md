>本文所有笔记总结于：[简明 Vim 练级攻略](https://coolshell.cn/articles/5426.html)
>前人栽树，后人乘凉，感谢！

---

### 1、安装及初步使用vim
首先，通过命令 `sudo apt-get install vim` (ubuntu系统)安装vim，如果你是图形界面，安装完之后，你会在应用栏里找到vim程序，单击打开，你会看到一个弹窗。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210710203554473.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

**此时的vim处于normal模式下**
- 注意：**此处的normal模式相当于键盘上的ctrl模式**。按住ctrl是一种键盘，放开ctrl就是普通的键盘。

在**normal模式下**，有以下基本的操作：
按键 | 操作
--- | ---
`i` | Insert模式，按ESC回到Normal模式
`x` | 删除当前光标所在的字符
`:w xxx` | 以xxx存盘
`dd` | 删除当前行，并把删除的行存在剪贴板中
`p` | 粘贴剪贴板
`hjkl` | 左下上右移动光标
`:help <command>` | 显示相关命令的帮助

- 注意：以`:`开始的命令需要输入`<enter>`回车结束

### 2、vim中级使用教程
- 注意：**所以的命令都必须是在normal模式下才能使用**

#### 1、各种插入模式

按键 | 操作
--- | ---
`a` | 在光标后插入
`o` | 在当前行后插入一个新行
`O` | 在当前行前插入一个新行
`cw` | 替换从光标所在位置后到一个单词结尾的字符

#### 2、简单的移动光标

按键 | 操作
--- | ---
`0` | 移动光标到行头
`^` | 到本行第一个不是空格的位置
`$` | 到本行行尾
`g_` | 到本行最后一个不是空格的位置。
`/pattern` | 搜索`pattern`的字符串（按n切换下一个）



