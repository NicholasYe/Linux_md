本文所有笔记总结于：[简明 Vim 练级攻略](https://coolshell.cn/articles/5426.html)
前人栽树，后人乘凉，感谢！

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

