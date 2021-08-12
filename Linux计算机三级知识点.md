```
本文为作者计算机三级linux学习笔记
会在暑假陆陆续续更新完毕，欢迎关注！
欢迎交流讨论，喜欢的话点个赞吧
```

---

## 1.linux系统使用基础

### 1.1 常用linux命令

#### 1.1.1 linux命令的基本格式
1. /root是超级用户的目录，/home是普通用户的目录
2. cd 用于切换目录 `cd /nicholas/local`
3. ls 用于显示目录下的所有文件，`ls -l`可以显示详细信息，`ls -a`可以显示包括隐藏文件的所有文件

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

---

## 2.shell脚本编程基础
### 2.1 shell编程概述
#### 2.1.1 shell的种类
1. 输入`cat /etc/shells` 可以查看所有的shell种类
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210707133033267.png)

#### 2.1.2 shell脚本的运行
shell脚本主要有三种方式：
1. 利用chmod命令修改脚本文件的权限为可执行 
   - `chmod u+x sh01`
   - `./sh01`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021070713494029.png)

2. 以脚本名作为参数传递给shell程序
   - `bash sh01`
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

---

## 3.用户管理

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
`-u` | 手动指定UID
`-d` | 主目录**必须要写绝对目录**
`-c` | 手动指定/etc/passwd文件中各用户信息中字段5的描述性内容
`-g` |　手动制定用户的初始组
`-G` | 指定用户的附加组
`-s shell` | 手动指定用户的登录shell。**一般默认为/bin/bash**
`-r` | 创建系统用户

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
`-S` | 查询用户密码的状态
`-l` | 暂时锁定用户(仅root用户)
`-u` | 解锁用户(与-l相对应)
`-x` | 设置该用户密码的有效期
`-i` | 设置用户密码失效日期
`--stdin` | 可以将通过管道输出的数据作为用户的密码

#### 3.3.3 修改用户信息命令
使用 `usermod [选项] 用户名` 命令可以修改**已存在**的用户，也可以用vim编辑器修改(/etc/passwd /etc/shadow /etc/group /etc/gshadow)文件。
注意：需要分清useradd与usermod两个命令，前者用于添加新用户，后者针对已存在的用户。
选项 | 含义
--- | ---
`-c` | 修改用户的说明信息
`-d` | 修改用户的主目录
`-e` | 修改用户的失效时期
`-g` | 修改用户的初始组
`-u` | 修改用户的ID
`-G` | 修改用户的附加组
`-l` | 修改用户名称
`-s shell` | 修改用户的登录shell，默认的是/bin/bash

- 是不是感觉useradd与usermod的命令非常像呢？

#### 3.3.5 修改用户密码状态命令
使用 `chage [选项] 命令` 可以修改用户密码信息

选项 | 含义
--- | ---
`-l` | 列出用户的详细密码状态
`-m` | 修改密码最短保留天数
`-M` | 修改密码有效期
`-E` | 修改账号失效日期

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
`-l` | 完整切换工作环境
`-p` | 切换为指定用户的身份，但不改变工作环境
`-c` | 切换并只执行一次命令，执行完自动切回

- 注意：使用 `su` 命令的时候，有 `-` 和没有 `-` 是完全不同的，`-` 选项表示在切换用户身份的同时，连当前使用的环境变量也切换成指定用户的。

![在这里插入图片描述](https://img-blog.csdnimg.cn/2021071320485742.png)

#### 3.3.8 用户组管理命令
- 使用 `groupadd [选项] 组名` 来添加用户组
- 使用 `groupmod [选项] 组名` 来修改用户组的相关信息
- 使用 `groupdel 组名` 来删除用户组
  
使用 `gpasswd [选项] 组名` 来给组设置一个组管理员

选项 | 含义
--- | ---
`-A user1` | 将群组的控制权交给user1(仅root)
`-M user1` | 将user1等用户加入此组(仅root)
`-r` | 移除组的密码
`-R` | 让组的密码失效
`-a user` | 将user用户加入组
`-d user` | 将user用户从组中移除

---

## 4.文件管理

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
`-n` | 对输出的**所有行**进行编号
`-b` | 此选项表示只对**非空行**进行编号
`-s` | 当遇到多行空白行时，替换为一行的空白行

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210714140018911.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210714140406163.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)


2. more命令
- more命令的基本格式是 `more [选项] 文件名`，可以逐页阅读文件中的内容

选项 | 含义
--- | ---
`-c或-p` | 不滚屏，先清屏后再显示内容
`-s` | 当遇到多行空白行时，替换为一行的空白行
`+n` | 从第n行开始显示文件内容(n代表数字)
`-n` | 一次显示的行数(n代表数字)

3. head命令与tail命令
- head命令的基本格式是 `head [选项] 文件名`，可以显示指定的文件前若干行的内容
- tail命令的基本格式是 `tail [选项] 文件名`，可以显示指定的文件末尾若干行的内容

选项 | 含义
--- | ---
`-n k` | 显示文件前k行的内容
`-c k` | 显示文件前k个字节的内容
`-v` | 显示文件名(head)
`-f` | 输出文件变化后增加的数据(tail)

4. touch命令
touch命令的重要功能是**修改文件的时间参数**

- 时间参数：
  1. 访问时间(access time)：只要文件的内容被读取，访问时间就会被刷新
  2. 数据修改时间(modify time)：只要文件的数据内容被修改，数据修改时间就会被刷新
  3. 状态修改时间(change time)：只要文件的状态发生变化(权限和属性)，状态修改时间就会被刷新

- touch命令的基本格式是 `touch [选项] 文件名`

选项 | 含义
--- | ---
`-a` | 只修改文件的访问时间
`-c` | 修改文件的三个时间参数
`-m` | 只修改文件的数据修改时间
`-t` | 该选项可以跟欲修订的时间(格式为`YYYYMMDDhhmm`)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210714145335701.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

5. grep命令
- grep命令的基本格式是 `grep [选项] 模式 文件名`，可以从文件中找到包含指定信息的那些行，**这里的模式，要么是字符(串)，要么是正则表达式。**

选项 | 含义
--- | ---
`-F` | 将查找模式解释成单纯的字符串
`-E` | 将查找模式解释成正则表达式
`-c` | 仅列出文件中包含模式的行数
`-i` | 忽略模式中字母的大小写
`-n` | 在每一行的最前面列出行号
`-v` | 列出没有匹配模式的行

> 正则表达式是描述一组字符串的一个模式，**通过使用操作符，将较小的表达式组合成一个新的表达式**

模式 | 含义
--- | ---
`c*` | 将匹配0个或多个字符c
`.` | 将匹配任何一个字符，而且只能是一个字符
`[xyz]` | 匹配方括号中的任意一个字符
`[^xyz]` | 匹配除方括号中字符外的所有字符
`^` | 行首定位符
`$` | 行尾定位符

6. sed命令
- sed命令的基本格式是 `sed [选项] sed 编辑命令 文件名`，sed主要用来自动编辑一个或多个文件，简化对文件的反复操作，编写转换程序，**文件的内容并没有改变，除非使用重定向存储输出。**

选项 | 含义
--- | ---
`-n` | 只显示匹配处理的行
`-e` | 执行多个编辑命令时使用
`-i` | 直接在文件中进行修改，而不是输出到显示器
`-r` | 支持扩展正则表达式 
`-f` | 从脚本文件中读取内容并执行

编辑命令 | 含义
--- | ---
`p` | 打印匹配行(print)
`d` | 删除指定行(delete)
`a` | 在匹配行后面追加(append)
`i` | 在匹配行前面插入(insert)
`c` | 整行替换
`r` | 读取文件的内容(read)
`w` | 将文本写入文件(write)
`s` | 字符串替换(匹配正则表达式)

- 是不是感觉晕了？我来举几个例子吧

1. `sed -n '3,5p' test03` 显示test03文件中第三、五行在显示屏上

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715000033694.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

2. `sed '2a drink tea' test03` 在test03文件第二行最后加上drink tea

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715001340234.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

- 注意：**这只是显示的时候有改动，实际的文件并没有改动**

7. awk命令
- awk命令的基本格式是 `awk [选项] '匹配规则{执行命令}' 文件名`，该命令也是逐行扫描文件，寻找含有目标文本的行，如果匹配成功，则会在该行上执行用户想要的操作。

8. cp命令
- cp命令的基本格式是 `cp [选项] 源文件 目标文件`，该命令主要用来复制文件和目录，同时借助某些选项可以复制整个目录。

选项 | 含义
--- | ---
`-a` | 相当于-d,-p,-r选项的合集
`-i` | 如果目标文件已存在，则会询问是否覆盖
`-l` | 把目标文件建立为源文件的硬链接文件(不复制)
`-s` | 把目标文件建立为源文件的软链接文件(不复制)
`-p` | 复制后目标文件保留源文件的属性
`-r` | 递归复制，用于复制目录
`-u` | 若目标文件与源文件有差异，可以更新目标文件

9. rm命令

- rm命令的基本格式是 `rm [选项] 文件或目录`，该命令可以永久性的删除文件系统中制定的文件或目录

选项 | 含义
--- | ---
`-f` | 强制删除，无提示
`-i` | 询问删除，有提示
`-r` | 递归删除，用于删除目录

> 出现啦，`rm -f` 删库跑路啦/doge


10. mv命令

- mv命令的基本格式是 `mv [选项] 源文件 目标文件`，该命令既可以在不同的目录之间移动文件或目录，也可以对文件和目录进行重命名

选项 | 含义
--- | ---
`-f` | 强制覆盖
`-i` | 交互移动
`-n` | 如果目标文件存在则不会覆盖移动
`-v` | 显示文件或目录的移动过程
`-u` | 若目标文件已经存在， 则对目标文件进行升级

- 除此以外，如果源文件和目标文件在同一目录中，那就是改名

比如：`mv test03 test 3` 就是直接修改文件名称

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715160845789.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

11.  sort命令

- sort命令的基本格式是 `sort [选项] 文件名`，该命令可以依据不同的数据类型来进行排序

选项 | 含义
--- | ---
`-f` | 忽略大小写
`-b` | 忽略每行前面的空白部分
`-n` | 以数值型进行排序
`-r` | 反向排序
`-u` | 删除重复行
`-t` | 指定分隔符
`-k [n,m]` | 从第n到第m个字段排序

12. wc命令

- wc命令的基本格式是 `wc [选项] 文件名`

选项 | 含义
--- | ---
`-l` | 只统计行数
`-w` | 只统计单词数
`-m` | 只统计字符数

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210715172121824.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)


#### 4.2.2 目录操作命令
1. mkdir命令

- mkdir命令的基本格式是 `mkdir [选项] 目录名`，该命令可用于创建新目录

选项 | 含义
--- | ---
`-m` | 用于手动配置所创建目录的权限
`-p` | 递归创建所有的目录

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210718085951636.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)


2. rmdir命令

- rmdir命令的基本格式是 `rmdir [-p] 目录名`，该命令用于删除**空目录**

与上一个命令相同，`-p` 指的是递归删除所有的目录，因此若只需要删除一个目录，可以不添加 `-p`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210718090417549.png)

3. cd命令

- cd命令的基本格式是 `cd [相对路径或绝对路径]`，是change directory对的缩写，用来切换工作目录

特殊符号 | 作用
--- | ---
`~` | 当前登录用户的主目录
`-` | 代表上次所在目录
`.` | 代表当前目录
`..` | 代表上级目录

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210718140018544.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

4. pwd命令

- pwd命令用于显示当前所在的绝对目录，是print working directory的缩写

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210718140324866.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)


5. ls命令

- ls命令的基本格式是 `ls [选项] 目录名称`，主要功能是显示当下目录的内容。

选项 | 含义
--- | ---
`-a` | 显示所有文件，包括隐藏文件
`-d` | 仅列出目录本身，而不列出目录内的文件数据
`-F` | 在文件或目录名后加上文件类型的指示符号
`-h` | 以易读的方式显示文件或目录大小
`-l` | 用长格式列出文件和目录信息
`-n` | 以UID和GID分别代替文件用户名和群组名显示出来
`-r` | 排序结果反向输出
`-R` | 连同子目录一同输出
`-S` | 以文件容量大小排序
`-t` | 以时间先后排序

- 如果想使用ls命令显示更多的内容，就需要使用表中相应的选项。**其中 `ls -ail` 命令最为常用**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210718153749904.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

> 细心的大家一定发现了，输入命令 `ls -l` 后的第一列会有一些字符，这些字符其实指的是**文件类型和不同的用户对文件所拥有的权限**，具体的字符含义如下

第一列字符 | 含义 | 其他列字符 | 含义
--- | --- | --- | ---
`-` | 普通文件 | `r` | 读
`d` | 目录 | `w` | 写
`l` | 链接文件 | `x` | 可执行
`b` | 块设备文件 | 
`c` | 字符设备文件 | 

6. ln命令

> 想要了解清楚ln命令，首先要了解ext4文件系统

- ext4文件系统主要分为两大部分：
  1. 小部分保存文件的索引(inode)信息(即`ls -l`显示的信息)
  2. 大部分保存数据块(block)信息

inode默认128字节，用来记录文件的权限(r,w,x)、文件的所有者和属组、文件的大小、文件的状态修改时间(ctime)、访问时间(atime)、数据修改时间(mtime)、文件数据真正保存的block编号。**每一个文件需要占用一个inode。**

block默认4KB，用于实际的数据存储。一个文件的内容可以存在多个block中，**但block只能存放同一个文件的内容，不能放入其他文件的数据。**

> 每一个文件独自占用一个inode，文件内容由inode来指向；如果想要读取文件内容，就必须借助目录中记录的文件名找到该文件的inode，才能找到文件内容所在的block。
> **整体流程：文件——>inode——>block——>文件数据**

而根据Linux系统储存文件的特点，链接的方式分为以下两种：
1. 软链接
   类似于windows的快捷方式，即产生一个特殊的文件，该文件用于指向另一个文件

2. 硬链接
   给文件的inode分配多个文件名，通过任何一个文件名，都可以找到此文件的inode

- ln命令的基本格式是 `ln [选项] 源文件 目标文件`
- 选项 `-s` 创建软链接文件，不加则创建硬链接文件

**硬链接特点：**
  1. **不管修改源文件还是硬链接文件，另一个文件的数据都会改变**
  2. 不管删除源文件还是删除硬链接文件，只要还有一个文件存在，这个文件（指inode号指代的文件）都可以被访问
  3. 硬链接不会建立新的inode信息，也不会更改inode的总数
  4. 硬链接不能跨文件（分区）建立
  5. 硬链接不能连接目录

![在这里插入图片描述](https://img-blog.csdnimg.cn/9254f455ea274acc89019bbc10ab6ebd.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

**软链接特点：（与windows的快捷方式一模一样）**
  1. 修改源文件，软链接文件的数据会随之发生改变
  2. **删除软链接文件，源文件不受影响；删除源文件，软链接文件将找不到实际的数据，从而显示文件不存在**
  3. 软链接会新建自己的inode信息和block，只是在block中不存储实际的文件数据，而存贮的是源文件的文件名和inode号
  4. 软链接可以链接目录
  5. 软链接可以跨分区

![在这里插入图片描述](https://img-blog.csdnimg.cn/9eb461641c9340d8acf26c99d74be493.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

### 4.3 访问权限管理

所谓权限管理，其实就指对不同的用户，设置不同的文件访问权限，包括对文件的读、写、删除等。

#### 4.3.1 权限位

Linux系统最常见的文件权限有3种，即对文件的**读（r）、写（w）和执行（x）权限**。在linux系统中，每个文件都明确规定了不同身份用户的访问权限，通过ls命令可以看到。

![在这里插入图片描述](https://img-blog.csdnimg.cn/dcffb51395c2455bb1358f2dd03d27ba.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

- 注意：
  - 第一位表示的是文件的具体类型
  - 后九位分为三组
     1. 文件所有者的权限
     2. 文件所有组的权限
     3. 其他人的权限

> 那么，`r w x` 三个权限的具体含义是什么呢？
> 注意：同一权限对文件和目录的作用是不同的

权限 | 对文件的作用 | 对目录的作用
--- | --- | ---
读权限 r | 可以读取此文件中的实际内容 | 可以读取目录结构列表
写权限 w | 可以编辑、新增或者修改文件中的内容 | 可以在目录中建立、删除或者更名文件与目录
执行权限 x | 表示该文件具有被系统执行的权限 | 表示用户可以进入目录

![在这里插入图片描述](https://img-blog.csdnimg.cn/98e1880a9c8b499c8020374a6260aea5.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

#### 4.3.2 修改权限位的命令

1. chmod命令

文件的基本权限由9个字符组成，如 `rwxrw-r-x` 就是由九位字母组成。可以使用数字来代表各个权限。其中：**r代表4，w代表2，x代表1**。那么，上式中的 `rwxrw-r-x` 就可以完美的转换为 `765`。由此，通过一串数字，我们就可以更改文件的权限，如 `chmod 777 study.exe`

- chmod命令的基本格式是 `chmod 权限值 文件名 `，**如果加选项 `-R` 表示连同子目录中的所有文件，也都修改为设定的权限。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/54f064945d7f4598a466e0b2e5b29869.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)


2. umask命令

Linux系统通过使用**umask默认权限**来给新建的文件和目录赋予初始权限的。
那么怎么查看umask默认权限的值呢？

![在这里插入图片描述](https://img-blog.csdnimg.cn/5c8ce84fff8149a19b7c7826016f54e9.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

- 唉？为什么是四个数字呢？这是因为第一个数字是指文件所具有的特殊权限，而后三位数字才是umask权限值，这里的0002代表的便是 `-------w-`

那么，就有：`文件（或目录）的初始权限=文件（或目录）的最大默认权限-umask权限`，而文件与目录的最大初始权限又是不同的。

种类 | 字母符号 | 数字
--- | --- | ---
文件 | `rw-rw-rw-` | `666`
目录 | `rwxrwxrwx` | `777`

- 想要修改也非常简单，使用 `umask xxx` 就可以修改，但这样的修改是临时性的，一旦重启或者重新登录就会失效。

3. chown命令(change owner)

- chown命令的基本格式是 `chown 所有者：所属组 文件或目录`，主要用于修改文件（或目录）的所有者，也可以用来修改文件（或目录）的所属组。
- 添加 `-R` 选项表示连同子目录的所有文件，都更改所有者

4. chgrp命令(change group)

- chgrp命令的基本格式是 `chgrp 所属组 文件名（目录名）`，用于修改文件（或目录）的所属组。
- 添加 `-R` 选项表示连同子目录的所有文件，都更改所属组。


> 这章终于结束了5555555555

---

## 5.进程管理

### 5.1 进程监视

1. ps命令

- ps命令的基本格式是 `ps [选项]`，此命令可以查看系统中所有运行进程的详细信息。

推荐的选项 | 作用
--- | ---
`-aux` | 查看系统中所有的进程
`-le` | 查看系统中所有的进程及其父进程的PID与进程优先级
`-l` | 只能查看当前shell产生的进程

- 输入 `ps -aux`

![在这里插入图片描述](https://img-blog.csdnimg.cn/25345e0a2d734a46a6e4622f213a47da.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

各个字段的含义如下：
字段 | 含义
--- | ---
`USER` | 进程是由哪个用户产生的
`PID` | 进程的ID
`%CPU` | 进程的CPU使用率
`%MEM` | 进程的物理内存使用率
`VSZ` | 进程占用虚拟内存的大小
`RSS` | 进程占用实际物理内存的大小
`TTY` | 进程是在哪个终端运行的
`STAT` | 进程的状态：   `S`睡眠，`R`正在运行，`T`停止，`<`高优先级，`N`低优先级，`L`锁入内存，`l`具有多线程，`+`位于后台
`START` | 进程启用的时间
`TIME` | 进程占用CPU的运算时间
`COMMAND` | 产生进程的命令名

- 输入 `ps -le`

![在这里插入图片描述](https://img-blog.csdnimg.cn/3a462d97bf6740f3a70402f46728d02d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

字段 | 含义
--- | ---
`F` | 进程标志，说明进程的权限（1是可复制不可执行，4是使用超级用户权限）
`S` | 进程的状态
`UID` | 运行进程的用户的ID
`PID` | 进程的ID
`PPID` | 父进程的ID
`C` | 进程的CPU占用率
`PRI` | 进程的优先级，数值越小，进程的优先级越高，越早被CPU执行
`NI` | 进程的优先级，数值越小，进程越早被执行
`ADDR` | 进程所在的位置
`SZ` | 进程占用的内存大小
`WCHAN` | 进程是否运行，`-`代表正在运行

- 如果你不想看到所有的进程，只想看到当前登录中断产生了哪些进程，只需要使用 `ps -l` 就足够了。

2. pstree命令

- pstree命令的基本格式是 `pstree [选项] [PID或用户名]`，用于以树形结构显示程序和进程之间的关系。

选项 | 含义
--- | ---
`-a` | 显示启动每个进程对应的完整指令
`-c` | 显示的进程中包含子进程和父进程
`-n` | 根据进程PID号来排序输出
`-p` | 显示进程的PID号
`-u` | 显示进程对应的用户名称

用pstree显示用户的所有进程并显示UID号：

![在这里插入图片描述](https://img-blog.csdnimg.cn/233398b538e44b7eaeb9d1b91a28f858.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

3. top命令

- top命令的基本格式是 `top [选项]`，主要用来动态地持续监听进程的运行状态。该命令还提供一个交互界面，用户可以根据需要，人性化地定制自己的输出。

选项 | 含义
--- | ---
`-d 秒` | 指定top命令每隔几秒更新
`-b` | 使用批处理模式输出
`-n 次数` | 指定top命令执行的次数
`-p 进程PID` | 仅查看指定ID的进程
`-s` | 使top命令在安全模式中运行
`-u 用户名` | 只监听某个用户的进程

![在这里插入图片描述](https://img-blog.csdnimg.cn/0b23ca3b54c84a32a6bad9e4e5eacc3a.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

> 是不是很像windows管理器的呢 /doge

在这个界面下，还可以使用如下按键进行交互操作：

按键 | 作用
--- | ---
`P` | 按照CPU的占用率排序
`M` | 按照内存的占用率排序
`N` | 安装PID排序
`T` | 按照CPU的累计运算时间排序
`q` | 退出top命令

- 如果想要看到所有的进程，则可以把执行结果重定向到文件中。不过top命令也是持续运行的，这是就需要使用`-b`和`-n`选项了，具体如下：`top -b -n 1 > top.log`，就可以把结果保存到`top.log`这个文件中，就可以看到所有的进程了。

![在这里插入图片描述](https://img-blog.csdnimg.cn/df35aca553ab493a842124dc01be2728.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

4. lsof命令(list opened files)

- lsof命令的基本格式是 `lsof [选项]`，就是列举系统中已经被打开的文件，通过该命令可以根据文件找到对应的进程信息，也可因此找到进程打开的文件。

选项 | 含义
--- | ---
`-c 字符串` | 只列出字符串开头的进程打开的文件 
`+d 目录名` | 列出某个目录中所有被进程调用的文件
`-u 用户名` | 只列出某个用户的进程打开的文件
`-p PID` | 列出某个用户的进程打开的文件

### 5.2 结束进程

进程的管理主要是指进程的关闭与重启。进程的关闭要依赖进程的信号(Signal)。可以用命令 `kill -l` 来查询。

![在这里插入图片描述](https://img-blog.csdnimg.cn/27efa32d01a84532b381238bb7eceb4b.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

信号代码 | 信号名称 | 说明
--- | --- | ---
1 | SIGHUP | 使进程立即关闭，重新读取配置文件之后重启
2 | SIGINT | 程序终止信号，用于终止前台进程
8 | SIGFPE | 在发生致命的算数错误时发出
9 | SIGKILL | 立即结束程序的运行（一般用于强制终止进程）
14 | SIGALRM | 时钟定时信号，计算的是实际的时钟或时钟时间
15 | SIGTERM | 正常结束进程的信号，kill命令的默认信号
18 | SIGCONT | 该信号可以让暂停的进程恢复执行，该信号不能被阻断
19 | SIGSTOP | 该信号可以暂停前台进程，该信号不能被阻断

1. kill命令

- 该命令的基本格式是 `kill [-信号] PID`，用来向进程发送一个用户指定的信号。
- 注意：kill命令只是“发送”一个信号，因此**只有信号被程序成功“捕获”，系统才会执行kill命令；反之，如果信号被“封锁”或“忽略”，则kill命令会失效**

2. killall命令

- 该命令的基本格式是 `killall [选项] [-信号] 进程名`，与`kill`命令不同的是，`killall`命令不再依靠PID来杀死单个进程，而是通过程序的进程名来杀死一类进程。

选项 | 含义
--- | ---
-i | 交互式询问是否杀死进程
-I | 忽略进程名的大小写

3. pkill命令

- 该命令的基本格式是 `pkill [-信号] 进程名`，但与`killall`命令不同的是，**`pkill`可以按章终端号来踢出登录用户**，命令的基本格式是 `pkill [-信号] [-t 终端号] 进程名`。

通过命令 `w` 查看本机已登录的用户，并用命令 `pkill -9 -t pts/0` 结束另外一个用户的进程：

![在这里插入图片描述](https://img-blog.csdnimg.cn/70d0089d49be48da9c905ad7885a3568.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)


### 5.3 进程优先级

Linux系统中通常运行着非常多的进程，但是CPU在一个时钟周期内只能运算几条指令，那么，谁应该先运算谁应该后运算呢？**这就需要由进程的优先级来决定了**

- 在Linux系统中，有两个参数表示进程的优先级：`PRI`(Priority) 和 `NI`(Nice)。
- 输入指令 `ps -le` 可以查看进程的优先级

![在这里插入图片描述](https://img-blog.csdnimg.cn/c674570cdd114d98b82e94dd25779f55.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

- 这两个值都代表着优先级，数值越小代表该进程越优先被CPU处理。**不过，PRI值是由内核动态调整，用户不能直接修改，只能修改NI的值。**
- PRI与NI两者之间的关系：`PRI（最终值）=PRI（原始值）+NI`

**修改NI值时有几个注意事项：**
  1. NI的范围是-20~19
  2. 普通用户调整NI值是0~19，而且只能调整自己的进程
  3. 普通用只能调高NI值，不能调低
  4. root用户可以在限制范围内随意更改

- 修改NI的值命令的基本格式是 `nice [-n NI值] 命令`，**该命令可以给要启动的进程赋予NI值，但是不能修改已运行进程的NI值。**

---

## 6.存储管理

### 6.1 存储设备的查看

硬盘可分为机械硬盘(Hard Disk Drive)和固态硬盘(Solid State Disk)。

#### 6.1.1 硬盘结构

- 机械硬盘
   - IDE硬盘
   - SATA硬盘
   - SCSI硬盘

#### 6.1.2 硬盘识别

分区号 | 分区类型
--- | ---
0x5或(0xf) | 可扩展分区
0x82 | Linux交换区
0x83 | 普通Linux分区
0x8e | Linux逻辑卷管理分区
0xfd | Linux的RAID分区

硬盘分区的作用：
1. 方便管理和控制
2. 提高系统的效率
3. 使用磁盘配额的功能限制用户使用的磁盘量
4. 便于备份和恢复

#### 6.1.3 存储设备的挂载

1. mount命令

该命令的常见格式有以下两种：
   1. `mount -l` 用于显示系统中已挂载的设备信息，`-l` 会额外显示出卷标名字
   2. `mount -a` 自动检查`/etc/fstab`文件中有无银疏漏而未被挂载的设备文件，如果有，则进行自动挂载操作。

### 6.2 磁盘管理

#### 6.2.1 df命令

- 该命令的基本格式是 `df [选项] [目录或文件名]`，用于显示Linux系统中个文件系统的硬盘使用情况，包括文件系统所在硬盘分区的总容量、已使用的容量、剩余容量等。

选项 | 含义
--- | ---
`-a` | 显示所有文件系统信息
`-m` | 以MB为单位显示容量
`-k` | 以KB为单位显示容量
`-h` | 使用KB、MB或GB等单位自行显示容量
`-T` | 显示该分区的文件系统名称
`-i` | 不显示硬盘容量而显示inode的数量

![在这里插入图片描述](https://img-blog.csdnimg.cn/6508c2294c8e4d2b88700f78f5a2a36c.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

> `Monuted on`: 文件的挂载点，也就是硬盘挂载的目录位置

#### 6.2.2 du命令

- 该命令的基本格式是 `du [选项] [目录或文件名]`，是用来统计目录或文件所占磁盘空间容量的。

选项 | 含义
--- | ---
`-a` | 显示所有子目录和子文件的磁盘占用量
`-h` | 使用习惯单位显示磁盘占用量
`-s` | 统计总磁盘的占用量

![在这里插入图片描述](https://img-blog.csdnimg.cn/52452f49037e4e61bc609779b77c5618.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

> 注意：**使用`du`命令和`df`命令去统计分区的使用情况时，得到的数据是不一样的。**`du`命令是通过搜索文件来计算每个文件的磁盘占用量，然后累加的；`df`命令记录的是通过文件系统获取文件的磁盘占用量，可以看得到已经删除的文件，而且计算大小的时候，把这一部分的空间也加上了。

#### 6.2.3 fsck命令

- 该命令的基本格式是 `fsck [选项] 分区设备文件名`，主要用来检查文件系统并尝试修复出现的错误。

选项 | 含义
--- | ---
`-a` | 自动修复文件系统，无提示信息
`-r` | 采取交互式的修复模式
`-A` | 按照`/etc/fstab`配置文件的内容检查文件内罗列的文件系统
`-t 文件系统类型` | 指定要检查的文件系统类型
`-C` | 显示检查分区的进度条
`-f` | 强制检测所有磁盘
`-y` | 自动修复（部分文件系统仅支持`-y`指令）

### 6.3 磁盘阵列

1. **RAID 0**

由两块及以上硬盘组成，每一组数据差分储存到不同硬盘之中

- 优点：
  1. 通过把多块硬盘合并成一块大的逻辑硬盘，实现数据跨硬盘存储
  2. 通过把数据分割成相等大小的区块，分别存入不同的硬盘，加快了数据的读写速度
  3. 几块硬盘组成了更大的硬盘，而且没有容量损失
- 缺点：
  1. 任何一块硬盘损坏，所有硬盘中的数据都会丢失 

> 我先来：R0一时爽，一直R0一直爽

2. **RAID 1**

由两块硬盘组成，一个硬盘作为另外一个硬盘的复制盘

- 优点：
  1. 具备数据冗余功能
  2. 读取性能会比单一硬盘更快
- 缺点：
  1. 容量只有两块硬盘的50%
  2. 硬盘的写入速度变慢了，因为要同时写入两个硬盘

3. **RAID 10或RAID 01**

- RAID 10：先组R1再组R0
- RAID 01：先组R0再组R1

> ~~好浪费啊~~

4. **RAID 5**

由三块及以上的相同硬盘组成，一块硬盘作为奇偶校验值，其他盘用于存储数据，当任何一块盘损坏时，都可以用奇偶校验值进行恢复。

- 优点：
  1. 具备数据冗余的功能
  2. 硬盘容量损失少，而且组成R5的硬盘数量越多，容量损失占比就越小 
  3. 读写性能比R1好
- 缺点：
  1. 只支持一块硬盘损坏后的数据修复
  2. 损失一块硬盘的存储空间 

> 我个人认为性价比最高的存储方式

---

## 7.网络管理

1. 网络接口卡(Network Interface Card,NIC)

通常，联网操作是通过机器上的PCI设备，即网络接口卡来实现的。通过命令`lspci`可以验证给出的PCI设备是否能被内核检测到。

> VM上的显示的接口很杂乱，为此，博主用树莓派上的Linux系统来展示

![在这里插入图片描述](https://img-blog.csdnimg.cn/8e2f6082a09e4a5e8cc2d327b3313937.png)

2. 网络接口

**常用的Linux接口名称和类型：**

名称 | 类型
--- | ---
eth0 | 以太网
lo | （虚拟）回环设备
ppp0 | 使用PPP协议的串口设备
tr0 | 令牌环
fddi0 | 光纤

3. 检测接口

输入命令 `ifcondig -a` 可以检测所有目前已被识别的网络接口信息

![在这里插入图片描述](https://img-blog.csdnimg.cn/838bf80431c040ee9970356fccf8edce.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

~~*啊 这章好难 书上写的好乱 我跳过了*~~

## 8.OpenSSH

### 8.1 安装OpenSSH

1. OpenSSH是Linux系统中最为常用的SSH服务器，在CentOS系统中通过命令 `sudo yum install openssh*` 安装OpenSSH。
2. 通过命令开启防火墙的22号端口
```
# sudo firewall -cmd --zone=public -add-port=22 /tcp --permanent
# sudo service firewall restart 
```

### 8.2 配置OpenSSH

OpenSSH的主配置文件为 `/etc/ssh/sshd_config`，可以通过Vim编辑器进行编辑，下面列出一些常见的配置选项：

配置选项 | 配置方法
--- | ---
设置SSH的端口号为22 | `Port=22`
启用SHH版本2协议 | `Protocol 2`
设置服务器监听的地址 | `ListenAddress 192.168.0.222`
设置IPV6地址 | `ListenAddress`
拒绝访问的用户（用空格隔开） | `DenyUsers Kobe James`
允许访问的用户（用空格隔开） | `AllowUsers root Nicholas`
禁止root用户登录 | `PermitRootLogin no`
用户登录需要密码认证 | `PermitEmptyPasswords no`
启用口令认证方式 | `PasswordAuthentication yes`
是否显示登录提示信息 | `PrintMotd yes`
是否使用DNS解析 | `UseDNS yes`

![在这里插入图片描述](https://img-blog.csdnimg.cn/f68331481b1c450c86a82e54eeb6770c.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)



- 通过命令 `service sshd status` 可以查看SSH服务是否正在运行，如果没有正常运行，可以通过指令 `service sshd start` 开启或者 `service sshd restart` 重启。

![在这里插入图片描述](https://img-blog.csdnimg.cn/5b0df1dbcfe74659a738d3d66b451379.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

### 8.3 OpenSSH的使用

OpenSSH采用密钥的方式对数据进行加密，在正式开始传输数据之前，双方先要交换密钥，当收到对方的数据时，再利用密钥和相应的程序对数据进行解密。

#### 8.3.1 远程登录

使用`ssh`命令登录的时候一般格式是 `ssh [user@] host [选项]`，使用ssh以root身份登录远程主机，执行ssh远程登录命令后，需要输入登录密码。在终端输入`exit`或`logout`退出登录，返回本机，退出成功后，终端会提示与远程主机断开连接。

选项 | 含义
--- | ---
`-p port` | 远程服务器监听的端口
`-b` | 指定连接的源IP地址
`-v` | 调试模式
`-C` | 压缩方式
`-X` | 支持x11转发
`-t` | 强制伪tty分配

#### 8.3.2 文件传输

- scp是OpenSSH中的一个重要客户端软件。该命令的一般格式是：**`scp [user@host1:]file1 [user@host2]file2`**，第一个参数是源文件，第二个参数是目标文件。

1. 从服务器上下载文件的命令一般格式是：`scp username@servername:/path/test.txt`
2. 从服务器上下载目录的命令一般格式是：`scp -r username@sername:/etc/github/(远程目录) /etc/download/(本地目录)`
3. 上传本地文件到服务器的命令一般格式是：`scp /path/test.txt username@servername:/path`
4. 上传本地目录到服务器的命令一般格式是：`scp -r /etc/upload/(本地目录) username@servername:/etc/github/(远程目录)`

---
> 好的，就到这里结束啦，开心~
> 一路上还是挺累的，又是上课又是做项目的，断断续续学完的
> 但是还有vim编辑和bash编程还没学，我会单独写两篇Blog的
> 希望能早点回学校吧，图书馆借的书没有带回来，bash是学不了555
> 继续加油吧╰(￣▽￣)╭

- 挖坑：
- [ ] Vim编辑器学习笔记
- [ ] Bash编程学习笔记
- [ ] Arduino扩展板——从AD设计再到投板焊接

---

`请在转载文章过程中明确标注文章出处！尊重原创，尊重知识产权，谢谢！`
