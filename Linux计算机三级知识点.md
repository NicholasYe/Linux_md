
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

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706141336334.png)

2. who命令：只能显示当前登录的用户信息  `who [选项] [file]`
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
注意：**这种方式脚本后面不可以带参数**

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
2. `ls -l c?` 显示从开头的所有两个字符的文件信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707141931112.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
3. `ls -l [ch]` 显示所有含有c或者h的**单个字符**文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707142440337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
**注意是单个字符！文件夹中的ch文件并未被进行操作**

4. 但是，`ls -l [!ch]*` 可以显示非c和h字符开头的所有文件，这里请细心琢磨琢磨

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707142736973.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)
#### 2.2.2 引号
上课去啦






---
`请在转载文章过程中明确标注文章出处！尊重原创，尊重知识产权，谢谢！`
