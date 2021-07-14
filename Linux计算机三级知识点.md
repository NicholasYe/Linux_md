
```
本文为作者计算机三级linux学习笔记
会在暑假陆陆续续更新完毕，欢迎关注！
欢迎交流讨论，喜欢的话点个赞吧
```
## 0 linux一些基础知识与命令
1. `su root` 进入超级用户模式
2. `yum search vim` 搜索软件, `yum install vim` 安装软件
3. 日期的格式为YYYY-MM-DD

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

1. who命令：只能显示当前登录的用户信息  `who [选项] [file]`
   1. who -a 全部显示 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706141401932.png)

3. echo命令 `echo [选项] [输出内容]`
   1. echo "Hello World" 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706141420378.png)

   2. echo "Hello World" 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210706141439689.png)

   3. **不知道为啥，在我眼中，科技最大的浪漫就是电脑回复你Hello World的那一刻**

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

符号 | 含义
--- | ---
* | 匹配任意字符的0次或多次出现
？ | 匹配任意单个字符
[ ] | 匹配该字符组所限定的任何一个字符
[^ ] 或 [! ] | 匹配不在该字符组的任何一个字符组
{string1, string2,……} | 匹配其中一个制定的字符串

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
如`echo 'It is warm(and sunny);come over & visit'` 计算机就不会误认为"（" 、 ";" 、 "&" 等符号。

2. 双引号
可是在程序中我们有时候需要保留部分有特殊含义的符号，如：

符号 | 意义
--- | ---
$ | 代表引用变量的值
\ | 转义字符
` | 引用命令

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

1. 输出重定向符 >>
命令的标准输出到指定文件的后面，原有文件不会被破坏
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707200900562.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

#### 2.2.4 命令执行操作符
1. 顺序执行 ;
如`ls ; date; cd/user; pwd` 会依次执行，命令之间没有任何逻辑关系，哪条命令错了也不会影响到下一条命令
2. 逻辑与 &&
如果使用“&&”连接多条命令，那么这些命令之间就有逻辑关系了。只有第一条命令正确执行了，第二条命令才会执行。`cp /root/test && rm /root/test`
3. 逻辑或 ||
只有第一条命令执行错误了，第二条命令才会执行。

- 注意：**&&与||具有相同的优先级，以从左往右的顺序执行**

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
1. 管道符 `|`
用于连接多条命令，**前一个命令的输出是下一个命令的输入**，命令2只能处理命令1的正确输出，如果输出内容过多，可以用 | more命令分屏显示
2. 后台命令符 `&`
可以使部分命令在后台进行，**与用户无交互，即不相应用户的输入和中断控制信号**
3. 注释符 `#`
注释注释注释，懂的都懂，不懂的话，emmm……

### 2.3 shell编程
>这章作者先暂时跳过，shell编程是独立且庞大的一章，作者会专门写一篇文章学习shell编程。


## 3 用户管理

### 3.1 用户与用户组管理
Linux系统支持多个用户在同一时间内登陆，不同用户可以执行不同的任务，并且互不影响

#### 3.1.1 用户与用户组
每一个用户都有一个**唯一**的用户名和密码。用户组是建立一个组，赋予这个组不同的权限，再将用户放置在组中，以达到赋予不同用户不同权限的功能。
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
- 其中1~499的ID是保留给系统使用的，这些用户被称为是系统用户或者伪用户，**无法用于登录系统**。500以后的ID是是给一般用户使用的。
- 每个字段含义如下：

>用户名：密码：UID：GID：描述性信息：主目录：默认shell
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210710123601940.png)

#### 3.2.2 shadow文件
shadow文件储存的是用户的密码信息，如果需要打开该文件，**需要通过 `su root` 进入管理员模式**，才能正常查看该文件。
通过 `cat /etc/shadow` 打开文件

#### 3.2.3 group文件
group文件储存的是用户组配置文件，可以通过 `cat /etc/group` 命令来打开
- 每个字段的含义如下：
>组名：密码：GID：该用户组的用户列表

#### 3.2.4 gshadow文件
同shadow文件，gshadow文件存储的是组用户信息。~~group+shadow嘛，简单！~~

### 3.3 用户和用户组管理的命令
**讲完如何查看用户的信息，那么下面自然而然讲的就是如何管理用户和用户组啦。**

#### 3.3.1 用户的添加
命令：`useradd [选项] 用户名`

选项 | 含义
--- | ---
-u | 手动指定UID
-d | 主目录**必须要写绝对目录**
-c | 手动指定/etc/passwd文件中各用户信息中字段5的描述性内容
-g |　手动制定用户的初始组
-G | 指定用户的附加组
-s shell | 手动指定用户的登录shell。**一般默认为/bin/bash**
-r | 创建系统用户

注意：**在创建用户的时候，系统已经帮用户设置了许多默认值**，如：
1. 在/etc/passwd中创建一行数据
2. 在/etc/shadow中创建一行数据，此时密码字段为“!!”，因为用户还未设置合理的密码
3. 在/etc/group中创建一行与用户名一模一样的群组
4. 在/etc/gshadow中创建一行与新增组相关的密码信息
5. 默认创建用户的主目录和邮箱
6. 将/etc/skel目录中的配置文件复制到新用户的主目录中

无敌版：
`useradd -u 550 -g student -G root -d /home/student -c "test user" -s /bin/bash student`
>所以这段代码是什么意思呢？请读者自行理解/doge

- 那我们新建用户的时候，能不能改一改默认的参考值呢？
  
用vim打开文件并修改： `vim /etc/default/useradd`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210710160219688.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

参数 | 含义
--- | ---
GROUP=100 | 用于建立用户的默认组
Home=/home | 用户主目录的默认位置
INACTIVE=-1 | 密码过期后的宽限天数(-1指不会过期)
EXPIRE= | 密码失效时间
SHELL=/bin/bash | 新建立用户的默认bash
SKEL=/etc/skel | 新建用户默认主目录的配置信息文件
CREATE_MAIL_SPOOL=yes | 指的是给新建用户建立邮箱

**这些值都可以通过vim编辑器进行修改**

- 除此以外，还有部分的默认信息可以在文件 `/etc/login.def` 中查看到

#### 3.3.2 密码配置命令
使用useradd命令创建新用户时，并没有给用户设置密码，所以无法正常登录，
通过命令 `passwd [选项] 用户名` 可以给账户设置密码

选项 | 含义
--- | ---
-S | 查询用户密码的状态
-l | 暂时锁定用户(仅root用户)
-u | 解锁用户(与-l相对应)
-x | 设置该用户密码的有效期
-i | 设置用户密码失效日期
--stdin | 可以将通过管道输出的数据作为用户的密码

#### 3.3.3 修改用户信息命令
使用 `usermod [选项] 用户名` 命令可以修改**已存在**的用户，也可以用vim编辑器修改(/etc/passwd /etc/shadow /etc/group /etc/gshadow)文件。
注意：需要分清useradd与usermod两个命令，前者用于添加新用户，后者针对已存在的用户。
选项 | 含义
--- | ---
-c | 修改用户的说明信息
-d | 修改用户的主目录
-e | 修改用户的失效时期
-g | 修改用户的初始组
-u | 修改用户的ID
-G | 修改用户的附加组
-l | 修改用户名称
-s shell | 修改用户的登录shell，默认的是/bin/bash

- 是不是感觉useradd与usermod的命令非常像呢？

#### 3.3.5 修改用户密码状态命令
使用 `chage [选项] 命令` 可以修改用户密码信息

选项 | 含义
--- | ---
-l | 列出用户的详细密码状态
-m | 修改密码最短保留天数
-M | 修改密码有效期
-E | 修改账号失效日期

> 既然可以用vim直接编辑，为何还要用chage命令呢？
> **因为chage命令可以让新建的用户在首次登录系统时立即修改密码**

代码如下：
```
# useradd student //创建用户student
# echo "student" | passwd --stdin student //设置用户的初始密码
# chage -d 0 student //将用户的创建日期改为1970年1月1日,这样用户登录后就必须修改密码
```

#### 3.3.5 删除用户命令
使用 `userdel -r 用户名` 可以删除用户的同时和用户的家目录

#### 3.3.6 查看用户的UID和GID命令
使用 `id 用户名` 可以查看用的UID、GID和附加组的信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210713204029219.png)


#### 3.3.7 用户间切换命令
使用 `su [选项] 用户名` 来切换用户

选项 | 含义
--- | ---
-l | 完整切换工作环境
-p | 切换为指定用户的身份，但不改变工作环境
-c | 切换并只执行一次命令，执行完自动切回

- 注意：使用 `su` 命令的时候，有 `-` 和没有 `-` 是完全不同的，`-` 选项表示在切换用户身份的同时，连当前使用的环境变量也切换成指定用户的。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021071320485742.png)

#### 3.3.8 用户组管理命令
- 使用 `groupadd [选项] 组名` 来添加用户组
- 使用 `groupmod [选项] 组名` 来修改用户组的相关信息
- 使用 `groupdel 组名` 来删除用户组
  
使用 `gpasswd [选项] 组名` 来给组设置一个组管理员

选项 | 含义
--- | ---
-A user1 | 将群组的控制权交给user1(仅root)
-M user1 | 将user1等用户加入此组(仅root)
-r | 移除组的密码
-R | 让组的密码失效
-a user | 将user用户加入组
-d user | 将user用户从组中移除
  
## 4 文件管理

### 4.1 文件系统
为了方便管理文件和目录，Linux系统将他们组织成一个分层的结构，有条不紊地管理着数据。

#### 4.1.1 文件系统的概念
文件系统的基本概念主要分三部分：
1. 文件：文件系统中存储数据的一个命名对象
2. 目录：包含许多文件控制块项目的一类特殊文件
3. 子目录：被包含在另一目录中的目录

说明目录或文件位置的方法有两种：
- 绝对路径：`/etc/login.defs`
- 相对路径：`etc/login.defs`

>注意：Linux系统**不以文件的扩展名来区分文件类型**
>例如：dog.exe只是一个文件，其扩展名.exe并不代表此文件就一定是可执行文件

### 4.2 文件与目录操作

#### 4.2.1 文件操作命令

1. cat命令
- cat命令的基本格式是 `car [选项] 文件名`，这个命令用于显示文件的内容。或者 `car 文件1 文件2 > 文件3`用于连接、合并文件。

选项 | 含义
--- | ---
-n | 对输出的**所有行**进行编号
-b | 此选项表示只对**非空行**进行编号
-s | 当遇到多行空白行时，替换为一行的空白行

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210714140018911.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210714140406163.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)


2. more命令
- more命令的基本格式是 `more [选项] 文件名`，可以逐页阅读文件中的内容

选项 | 含义
--- | ---
-c或-p | 不滚屏，先清屏后再显示内容
-s | 当遇到多行空白行时，替换为一行的空白行
+n | 从第n行开始显示文件内容(n代表数字)
-n | 一次显示的行数(n代表数字)

3. head命令与tail命令
- head命令的基本格式是 `head [选项] 文件名`，可以显示指定的文件前若干行的内容
- tail命令的基本格式是 `tail [选项] 文件名`，可以显示指定的文件末尾若干行的内容

选项 | 含义
--- | ---
-n k | 显示文件前k行的内容
-c k | 显示文件前k个字节的内容
-v | 显示文件名(head)
-f | 输出文件变化后增加的数据(tail)

4. touch命令
touch命令的重要功能是**修改文件的时间参数**

- 时间参数：
1. 访问时间(access time)：只要文件的内容被读取，访问时间就会被刷新
2. 数据修改时间(modify time)：只要文件的数据内容被修改，数据修改时间就会被刷新
3. 状态修改时间(change time)：只要文件的状态发生变化(权限和属性)，状态修改时间就会被刷新

- touch命令的基本格式是 `touch [选项] 文件名`

选项 | 含义
--- | ---
-a | 只修改文件的访问时间
-c | 修改文件的三个时间参数
-m | 只修改文件的数据修改时间
-t | 该选项可以跟欲修订的时间(格式为`YYYYMMDDhhmm`)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210714145335701.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

5. grep命令










---
`请在转载文章过程中明确标注文章出处！尊重原创，尊重知识产权，谢谢！`
