
```
本文为作者计算机三级linux学习笔记
会在暑假陆陆续续更新完毕，欢迎关注！
欢迎交流讨论，喜欢的话点个赞吧
```


## 1 linux系统使用基础

### 1.1 常用linux命令

#### 1.1.1 linux命令的基本格式
1. /root是超级用户的目录，/home是普通用户的目录
2. cd 用于切换目录 `cd /nicholas/local`
3. ls 用于显示目录下的所有文件，`ls -l`可以显示详细信息，`ls--all`可以显示包括隐藏文件的所有文件

#### 1.1.2 linux的简单命令
1. w命令：可以显示所有用户的信息 `w [选项] [用户名]`
   1. w -h 不显示输出信息标题
   2. w -l 用详细格式输出
   3. w -s 用简洁格式输出
2. su root 进入超级用户模式

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706141336334.png)

1. who命令：只能显示当前登录的用户信息  `who [选项] [file]`
   1. who -a 全部显示 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706141401932.png)

3. echo命令 `echo [选项] [输出内容]`
   1. echo "Hello World" 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706141420378.png)

   3. echo "Hello World" 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706141439689.png)

   5. **不知道为啥，在我眼中，科技最大的浪漫就是电脑回复你Hello World的那一刻**

1. date命令 `date [选项]`
   1. date 
   2. data -s 设置时间

2. passwd命令 `passwd [选项] 用户名`
   1. root用户可通过 passwd xxx 修改普通用户的密码
   2. passwd 可以直接修改自己的密码 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706141458416.png)

### 1.2 RPM包安装、卸载和升级
1. 安装 `rpm -ivh xxx`
2. 升级 `rpm -Uvh xxx`
3. 卸载 `rpm -e xxx`
4. 查询 `rpm -q xxx`和`rpm -qa` 查询所有

## 2 shell脚本编程基础
### 2.1 shell编程概述
#### 2.1.1 shell的种类
1. 输入`cat /etc/shells` 可以查看所有的shell种类
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707133033267.png)

#### 2.1.2 shell脚本的运行
shell脚本主要有三种方式：
1. 利用chmod命令修改脚本文件的权限为可执行 
   1. `chmod u+x sh01`
   2. `./sh01`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021070713494029.png)
2. 以脚本名作为参数传递给shell程序
   1. `bash sh01`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707135215838.png)
3. 运行bash程序，以输出重定向的方式让bash从给定文件中读入命令行
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021070713542151.png)
- 注意：**这种方式脚本后面不可以带参数**

### 2.2 shell基础
#### 2.2.1 通配符
文件名的扩展称为通配（Globbing），通配定义了一整套使用特殊字符的规则。

符号|含义
---|---
*|匹配任意字符的0次或多次出现
？|匹配任意单个字符
[ ]|匹配该字符组所限定的任何一个字符
[^ ] 或 [! ]|匹配不在该字符组的任何一个字符组
{string1, string2,……}|匹配其中一个制定的字符串

**举几个例子吧：**
1. `ls -l ab*` 显示所有ab开头的文件信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707141554923.png)
2. `ls -l c?` 显示c开头的所有**两个字符**的文件信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707141931112.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
3. `ls -l [ch]` 显示所有含有c或者h的**单个字符**文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707142440337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
- 注意：**是单个字符！文件夹中的ch文件并未被进行操作**

1. 但是，`ls -l [!ch]*` 可以显示非c和h字符开头的所有文件，这里请细心琢磨琢磨

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707142736973.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

上课去啦———>上课回来啦

#### 2.2.2 引号
1. 单引号
在输出字符的时候，计算机无法辨别字符是程序语言还是普通语言，所以用引号可以帮助计算机辨别语言种类
如`echo 'It is warm(and sunny);come over & visit` 计算机就不会误认为"（" 、 ";" 、 "&" 等符号。
2. 双引号
可是在程序中我们有时候需要保留部分有特殊含义的符号，如：
- $ : 代表引用变量的值
- \ : 转义字符
- ` : 引用命令
**在双引号中，这些符号会被正常识别为特殊符号**，看这个例子就懂啦
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707191841992.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
3. 倒引号
倒引号被括起来的字符串**被shell解释为命令行**，shell会直接执行这段命令并取代倒影号部分
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707192411804.png)

#### 2.2.3 输入/输出重定向符
其实输入/输出方向就是数据的流动方向
1. 输入重定向符 <
输入重定向符“<”的作用是把命令的标准输入重新定向到指定的文件,如`bash < sh01` 或者 `wc -l <abc` 可以统计abc文件中的行数。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707195509892.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
2. 输入重定向符 <<
输入重定向符可以使用特定的分界符作为命令的结束标志,如 `wc -l <<END` 只会在遇到END后才会结束。
3. 输出重定向符 >
输出重定向符“>”可以把命令的标准输出重新定向到制定文件中
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021070720043673.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
- 注意：若无此文件，将**生成一个新文件**；若已有该文件，此文件将被**重新覆盖！**
4. 输出重定向符 >>
命令的标准输出到指定文件的后面，原有文件不会被破坏
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707200900562.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

#### 2.2.4 命令执行操作符
1. 顺序执行 ;
如`ls ; date; cd/user; pwd` 会依次执行，命令之间没有任何逻辑关系，哪条命令错了也不会影响到下一条命令
2. 逻辑与 &&
如果使用“&&”连接多条命令，那么这些命令之间就有逻辑关系了。只有第一条命令正确执行了，第二条命令才会执行。`cp /root/test && rm /root/test`
3. 逻辑或 ||
只有第一条命令执行错误了，第二条命令才会执行。
- 注意：&&与||具有相同的优先级，以从左往右的顺序执行

#### 2.2.5 小括号与大括号
- 相同之处：大括号{ }和小括号( )都可以将若干命令括起来，在逻辑上成为同一条命令
- 不同之处：小括号会单独创建一个子shell，这个子shell可以在不需要输入的情况下一次性全部处理所有的命令，运行结束后子shell自动结束。

举个小例子吧：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707213827219.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
1. 第一个小括号的命令执行完后，主shell并未进入study的文件夹中，但是子shell进入study文件夹中并创建了文件test01；
2. 第二个大括号的命令执行完后，主shell进入study的文件夹中，并创建了test02文件；完成命令后主shell就在study文件夹中了。
- 注意：**大括号的第一条命令前多打一个空格，最后一条记得打分号！**
>懂了没懂了没懂了没/doge

#### 2.2.6 管道符、后台命令符和注释符
1. 管道符 |
用于连接多条命令，**前一个命令的输出是下一个命令的输入**，命令2只能处理命令1的正确输出，如果输出内容过多，可以用 | more命令分屏显示
2. 后台命令符 &
可以使部分命令在后台进行，**与用户无交互，即不相应用户的输入和中断控制信号**
3. 注释符 #
注释注释注释，懂的都懂，不懂的话，emmm……

### 2.3 shell编程
>这章作者先暂时跳过，shell编程是独立且庞大的一章，作者会专门写一篇文章学习shell编程。


## 3 用户管理

### 3.1 用户与用户组管理
Linux系统支持多个用户在同一时间内登陆，不同用户可以执行不同的任务，并且互不影响
#### 3.1.1 用户与用户组
每一个用户都有一个唯一的用户名和密码。用户组是建立一个组，赋予这个组不同的权限，再将用户放置在组中，以达到赋予不同用户不同权限的功能。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210708081943525.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
#### 3.1.2 用户与用户组管理
- 输入 `cat /etc/passwd` 后可以查看所有用户名与ID对应关系
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210708082802853.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
- 注意：其中第1字段是用户名，**第3字段是用户UID，第4字段是用户GID**（加粗部分下同）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210708083831248.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

- 输入 `cat /etc/group` 后可以查看ID与用户组对应关系
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210708083600803.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

### 3.2 用户和用户组管理的相关文件
#### 3.2.1 passwd文件
首先通过 `cat /etc/passwd` 打开文件
1. 其中1~499的ID是保留给系统使用的，这些用户被称为是系统用户或者伪用户，**无法用于登录系统**。500以后的ID是是给一般用户使用的。









---
`请在转载文章过程中明确标注文章出处！尊重原创，尊重知识产权，谢谢！`
