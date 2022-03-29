### Conda的安装与使用

在服务器上使用Linux命令行安装Conda（Conda可以理解类似于应用商店或是mac里的Aapp Store。可以在conda里面安装软件，或者在conda之外安装），使用conda管理小环境和使用conda管理软件，用conda来安装和管理生信软件以及环境比较方便。

>- conda的安装
>- conda创建小环境
>- conda创建的小环境里安装软件

**CONDA的官方链接与简介**

https://docs.conda.io/en/latest/

Conda is an open source **package management system** and **environment management system** that runs on Windows, macOS and Linux. Conda quickly installs, runs and updates packages and their dependencies. Conda easily creates, saves, loads and switches between environments on your local computer. It was created for Python programs, but it can package and distribute software for any language.

**几种conda之间的关系**

![几种conda之间的关系](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305152345561-6465028.png)

The **conda package and environment manager is included in all versions of [Anaconda]®, [Miniconda]**, and [Anaconda Repository]. Conda is also included in [Anaconda Enterprise], which provides on-site enterprise package and environment management for Python, R, Node.js, Java, and other application stacks. Conda is also available on [conda-forge], a community channel. You may also get conda on [PyPI], but that approach may not be as up to date.（https://docs.conda.io/projects/conda/en/latest/）

Conda包含miniconda和anaconda。miniconda比较简单，只能在命令行中使用，anaconda比较强大，有一个界面化的软件，但是占用系统空间比较大。现在使用Linux，用命令行操作的miniconda就可以了。

```

```



#### 1.下载conda

国内服务器需要选择conda镜像，**通常国内服务器选择清华源、中科大、北京外国语镜像，国外选择官网**，中科大的镜像之前挂了，国内可以搜索conda清华源镜像。

**以下网址最后有miniconda的使用帮助**

https://mirror.tuna.tsinghua.edu.cn/help/anaconda/

![找到miniconda的链接](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305154311320.png)

**miniconda版本的选择**

https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/

![找到最新的版本和复制链接](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305154819568.png)

网页上会显示Miniconda2...和Miniconda3等新旧以及不同系统（Windows、Mca，Linux）对应的版本。服务器用的Linux系统安装，下载Linux版本对应的miniconda，和自己的**电脑系统没有关系**。找到最新版本的 Miniconda3-latest-Linux-X86_64.sh，点击鼠标右键-复制链接地址。

![复制最新linux版本的链接](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305163804650.png)

复制链接地址到服务器，用服务器下载Miniconda。

```R
##wget 加网址，中间可以加-c参数，断点续传
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

![用服务器下载miniconda](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305163919675.png)

用的是服务器上的网络，速度很快。

![查看下载后的结果](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305164028629.png)

#### 2.安装conda

**安装过程：**注意路径，用**bash**命令去安装。

认真看安装过程提示信息，需要按**` Enter`** **(回车键)**或者输入**` yes`**，（如果输入yes时，不小心输多了，就按control和退格键删除）,

![用bash激活安装](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305164236885.png)

看到**more**就是按空格键翻页查看协议，按**`q`**退出

![在服务器安装软件同意协议](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305164403950.png)

接受协议，输入**`yes`**

![接受安装协议](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305164546012.png)

默认安装路径，按**`enter`**

![安装软件默认安装路径](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305164813502.png)

会询问是否需要初始化，输入**`yes`**

![安装需要初始化](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305165217130.png)

显示安装已完成的提示信息

![安装已经完成的提示](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305165421810.png)

**激活刚安装完成的软件**

一般安装软件完成后需要重启，在Linux叫激活，有两种方式，**第一种**是重新登录服务器，**第二种**是输入以下命令：

```shell
source ~/.bashrc
##比较常用
```

![激活环境](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305170006964.png)

![成功激活](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305170123683.png)

#### 3.检查conda是否安装成功

安装一个软件后，需要检查软件是否安装成功，调用软件的帮助文档

```R
conda --help
#调用出来说明安装成功
```

![能调用帮助文档说明安装成功](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305170345481.png)

#### 4.配置conda镜像

##### 选择镜像

使用conda是需要它去安装其它软件（如生信软件），conda是默认去自己的官网搜索，而我们使用的服务器是在国内，conda的网在国外，从国内的网络去访问国外的网络就是特别的慢，所以需要配置镜像，如配置清华的镜像。

主要看自己的服务器在哪里，无论人在国外还是国内，使用的服务器在国内，就配置国内镜像。

```R
# 下面这三行配置官网的channel地址
conda config --add channels r 
conda config --add channels conda-forge 
conda config --add channels bioconda
##以上三句命令一次性复制粘贴或是单独复制粘贴到服务器
```

![设置镜像前置](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305171028286.png)

配置国内访问镜像，国内用户推荐的镜像，以下选清华或是北外的镜像都可以，（1）和（2）任选一个，清华镜像的访问量很多，可以选北外镜像。

```R
#（1）下面这四行配置清华大学的conda的channel地址，国内用户推荐
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --set show_channel_urls yes
##配置清华镜像，四句代码一起复制粘贴到服务器

# （2）下面四行配置北京外国语大学的conda的channel地址
conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/pkgs/main/ 
conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/cloud/conda-forge/ 
conda config --add channels https://mirrors.bfsu.edu.cn/anaconda/cloud/bioconda/ 
conda config --set show_channel_urls yes
```

![设置国内镜像](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305171429538.png)

##### 查看配置镜像结果

 配置镜像完成后会出现一个.condarc 文件，会在 ~/.condarc 文件中 写入以下内容

![镜像设置成功生成文件](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305171617238.png)

```
cat ~/.condarc
```

![conda设置](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220309154601485.png)

```R
##关掉左上角的（base），运行以下两行代码
conda config --set auto_activate_base false
source ~/.bashrc
##不想关掉也没有关系
```

每一行是一个频道，含有free的频道已经没有

检查一个目录下有多少人是安装成功conda的命令：

```
ls -lh /trainee*/Jan*|grep miniconda
```

如果安装conda失败需要做些什么

```R
##先删除后安装
##删除：
rm -r miniconda/
ls -lha
rm -r .conda
##.condarc不要删掉，是配置镜像的，不管镜像

#重新安装
ls 
bash  Miniconda3-latest-Linux-x86_64.sh 
##跟着之前的步骤安装
```

#### 5.安装conda之后，创建小环境

##### 创建小环境

**`-n `**指定小环境的名字 rna，并安装 **python=3** 版本

安装conda的目的是，通过安装conda来安装其它软件，安装其它软件之前要构建一个小环境，可以创建多个小环境。有时候，A软件需要python=3和B软件需要python=2，python=2和python=3不兼容，就冲突了，创建小环境可以解决这个问题，A有自己的小环境，B有自己的小环境。

```R
# 创建名为rna的软件环境来安装转录组学分析的生物信息学软件
conda create -y -n  rna  python=3
#如果不加-y，中间会问需要继续进程吗？
#linux一般会默认安装python最新版本，除非所处的环境不能安装最新版本的。

# 创建小环境成功，并成功安装python3版本
# 每建立一个小环境，安装一个python=3的软件作为依赖

# 查看当前conda环境
conda info -e

# 每次运行前，激活创建的小环境rna
conda activate rna
##激活成功会出现一个小括号（小环境名字，rna）
# 退出小环境
conda deactivate
```

**创建成功最后会出现 3 个 done**

![激活和退出小环境](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220309154853456.png)

##### 激活与退出小环境、查看已经创建过的小环境

```shell
conda activate rna
##激活小环境
conda deactivate 
##退出，后面不需要加小环境的名字
```

![进入和退出小环境的标志](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220309155028691.png)

#### 6.在小环境中安装生信软件

**Conda下载安装软件**指定版本，-y 参数的作用是忽略提示。

注：**软件都要安装在小环境中，*不要安装在 base*里**， **首先要用conda激活小环境。**

```sh
##在小环境里安装软件
# 激活环境
conda activate rna
##安装samtools
##conda install -y samtools
##安装成功一般会出现三个done，
##有时候因为一些问题安装不成功，去channel的搜索，有时候因为网络的问题，下载的库不完整，网络问题很少出现，如果没有安装完，过一段时间，重新运行安装代码

# 安装 fastqc 软件
conda  install -y fastqc

# 调出帮助文档
fastqc --help

# 可以指定软件版本
conda install -y sra-tools
##可以指定安装版本
##conda install -y sra-tools=2.10.7
##安装完成返回3个done，如果有一个文件比较大，终止了，可以重新运行安装命令

# aspera 
conda install -y aspera-cli -c  hcc 
ascp --help

# 可以一次安装多个软件
conda install -y trim-galore  hisat2  subread  multiqc  samtools  salmon  fastp
##作为新手，建议一个个软件安装，有时候软件之间会出现冲突，conda不能解决软件之间的冲突问题。
```

建议**初学者**安装软件，单个软件安装，如果批量安装软件，出现报错，解决就比较麻烦。

下载安装软件：下载过程可能受网络影响没下载成功，如果出现 **3 个 done**，即表示下载完成。

![安装软件完成的标志-3个done](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305210154009.png)

检查：通过调用软件的帮助文档来经常是否下载成功。如果失败， 重新下载即可。通过**调用软件的帮助文档**来检查软件是否可以使用。

![fastqc --help调出来，说明安装成功](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220305210521605-20220305210728454.png)

并不是每个软件都是用”软件名--help“来调用的。**samtools 是生信分析中最强大的一个软件，后面的分析可能就会用到几个常用的参数**

#### 7.特殊情况

不在channel里的软件，如何确定频道，后面讲怎么搜索频道

```R
conda install -y aspera-cli -c  hcc 
##-c hcc，-c是指定它在hcc频道，就是指定安装的频道
##调用帮助文档，不是软件的名字，如下
ascp --help
#有时候一个软件是一个工具集，它下面有很多工具，每个工具都有不同的名字，就调某个具体工具的名字，而不是调用软件的名字。

#samtools，fastqc刚好有一个软件名和它的命令是一样的。

####第二个特殊情况
#  trim-galore
trim_galore --help
##注意中间连线的不同，这是某个作者开发的，可能作者觉得好玩，就这么弄不一致。
```

我们用的工具都是先人开发好的，知道怎么用就行，感兴趣自行探索。

```R
## 不是通过软件名来调用帮助文档，而是软件的命令
# sra-tools
prefetch --help
fastq-dump --help
which prefetch

#  trim-galore
trim_galore --help

# hisat2
hisat2 -h

# subread
featureCounts

# multiqc
multiqc --help

# samtools
samtools
which samtools

# salmon
salmon

# fastp
fastp --help
```

#### 8.conda其他用法

>- 更新软件：conda  update  软件名
>- 卸载软件：conda  remove  软件名
>- 删除环境：conda  remove  -n   环境名
>- 克隆环境：conda  create –n 新环境名 –clone  旧环境名
>
>（克隆就是备用的，如果发现新的好用的环境）
>
>- 查找软件：conda  search  软件名
>
>（查找用得最多）
>
>注意：以上的操作要在小环境里

- **查找软件常用的链接**：

[https://bioconda.github.io](https://bioconda.github.io/)[/](https://bioconda.github.io/)

https://anaconda.org/search

```R
##我们认知的软件名（通过文献或是公众号）和conda给的名字不一样，先搜索，如下的软件
trim_galore -> trim-galore
       vep  -> ensembl-vep
sratoolkit  -> sra-tools
```

bioconda是一个频道，里面是有与生信相关的软件。看看bioconductor与生信相关的R包。

- **查看已安装的软件:**

>• conda list
>• conda list fast*
>(比如很早就安装某个软件，如果只想起四个字母，用通配符的去查找)
>• conda list –n rna

- **清空缓存:**

清除掉下载了但是没有用到的包，清除掉index，清空缓存结合报错一起使用

>• conda clean -i 
>• conda clean -a 
>• conda clean –p 
>• conda clean –t

-  **常见报错及解决方法1:**

**CondaHTTPerror**

![网络问题导致的报错](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220306095438201.png)

因为网络问题导致的，重新下载一份，或是重新运行命令，或是过一段时间之后安装就可以。但是有时候试了都不行，可能之前下载到一半，重新下载识别之前的一般，这时考虑清除缓存。

**conda clean 清空环境中的缓存等**

有时候遇到一些奇怪的报错，可以尝试下面的办法（没有理由的尝试，小郭老师多次探索）：

**把 ~/.condarc 中的 https 改成 http**

修改网络传输协议，比如，你使用的那台服务器在某个时间段不允许访问清华镜像。很奇怪，是经过探索出来的（小郭老师）。

- **常见报错及解决方法2：**

**一直在 Solving environment?**

![安装时出现的报错](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220309155255600.png)

**网络较差，换个时间试试**
可以**conda clean 清空环境中的缓存等**

或是**把** **~/.condarc** **中的** **https** **改成** **http**

多尝试多探索。

#### 9.mamba

mamba是非常强大的一个工具，是conda的升级版

mamba作用：

提高 conda 安装软件的速度，需要在 base 环境中安装 mamba ，激活小环境后 conda activate rna，使用 mamba 代替 conda 进行搜索、安装软件等。

```bash
conda deactivate
##不要在小换环境下安装mamba，mamba是唯一一个特殊的软件，不需要安装在小环境里，其它的要安装在小环境里。
conda install -y mamba
##记得加-y参数，
mamba install -y bowtie2
##安装成功
which bowtie2
##查找软件所在的位置
```

**注意：**很少用到mamba，一般用conda安装不行，再用mamba试一下

![mamba的安装](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220309155426258.png)

**安装完成的标志：3个done**

![用mamba安装bowtie2](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220309155553317.png)

#### 10.查看conda里环境

```
conda info -e
##查看环境
```

![查看环境以及当前所处的环境](/Users/jschen/Desktop/conda%E5%AE%89%E8%A3%85.assets/image-20220309155734474.png)



### 说明

以上内容是听**生信技能树小郭老师**授课内容以及参考课件。

