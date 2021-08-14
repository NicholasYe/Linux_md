
```
本文为作者学习开源许可的笔记
欢迎交流讨论，喜欢的话点个赞吧
```

### 1.如何添加一个开源License

1. 在github自己的项目界面中点击`Add file`中的`Create new file`

![在这里插入图片描述](https://img-blog.csdnimg.cn/9cdba04e81ff44798d6ddf0fb9ea7f86.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

2. 再将自己的新文件命名为`LICENSE`，此时右侧会会出现一个`Choose a license template`选项

![在这里插入图片描述](https://img-blog.csdnimg.cn/10e442baa0a240fe9177b849f940675e.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

3. 点击该选项就会有看到一列表的开源License

![在这里插入图片描述](https://img-blog.csdnimg.cn/a3ec273bffa74dd68e159f914929ad25.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L05pY2hvbGFzWVRa,size_16,color_FFFFFF,t_70)

---

### 2.如何选择一个合适的开源License


#### 1.[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)

- 该License的特点：
  1. **任何情况下使用必须要带上License**
  2. 可以对源代码进行修改，但需要在被修改的文件中说明
  3. 该协议下的代码可以进行商用

- 使用说明：
  1. 在您的工作中包含一份 Apache 许可证的副本，通常在名为 LICENSE 的文件中，并考虑还包括一个引用该许可证的 NOTICE 文件。
  2. 要将 Apache 许可应用于您工作中的特定文件，请附上以下样板声明，**用您自己的识别信息替换括号“[]”中的字段**。（不要包括括号！）用文件格式的适当注释语法将文本括起来。


> APPENDIX: How to apply the Apache License to your work.
> 
> To apply the Apache License to your work, attach the following
  boilerplate notice, with the fields enclosed by brackets "[]"
  replaced with your own identifying information. (Don't include
  the brackets!)  The text should be enclosed in the appropriate
  comment syntax for the file format. We also recommend that a
  file or class name and description of purpose be included on the
  same "printed page" as the copyright notice for easier
  identification within third-party archives.

```
Copyright [yyyy] [name of copyright owner]

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License. 
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
- 样例([AliceMind](https://github.com/alibaba/AliceMind))：
```
License

AliceMind is released under the Apache 2.0 license.

Copyright 1999-2020 Alibaba Group Holding Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at the following link.

     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

#### 2. [MIT License](https://mit-license.org/)

- 该License的特点
  1. **可以对源代码进行修改，也不需要对自己的修改进行说明**
  2. 修改后的代码可以闭源进行商用，但必须附有MIT授权协议和版权声明

- 使用说明：直接添加在项目里就行了

```
MIT License

Copyright (c) 2021 NicholasYe

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

#### 3. [GNU General Public License v3.0](http://www.gnu.org/licenses/gpl-3.0.en.html)

- 该License的特点：
  1. **在修改源码后，不可以闭源用于产品的发布和销售**
  2. 对于该协议的产品，其衍生的软件产品也必须采用GPL协议

- 使用说明：
  1. 将下列文字附加到每个源文件的开头，以最有效地说明开源所有条件
  2. 每个文件至少应该添加“版权”行和关于完整“版权告示”在文件中的位置
  3. 还要添加有关如何通过电子邮件和纸质邮件与您联系的信息

> If you develop a new program, and you want it to be of the
greatest possible use to the public, the best way to achieve 
this is to make it free software which everyone can redistribute
and change under these terms.
> 
> To do so, attach the following notices to the program. It is 
safest to attach them to the start of each source file to most
effectively state the exclusion of warranty; and each file 
should have at least the "copyright" line and a pointer to 
where the full notice is found.
>
> Also add information on how to contact you by electronic and paper mail.

```
<one line to give the program's name and a brief idea of what it does.>
Copyright (C) <year>  <name of author>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
```

#### 4. 其他协议

对于其他的主流协议，可以看看[《如何选择开源许可证？》](http://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html)这篇博客中的这张图，作者就不再详细介绍了。

![](https://img-blog.csdnimg.cn/img_convert/3ce23af4e6b9533514e55e2bfe43ca90.png)


---
写在最后：开源必定是时代所趋，感谢开源给科技带来的进步，给社会带来的美好

`请在转载文章过程中明确标注文章出处！尊重原创，尊重知识产权，谢谢！`

