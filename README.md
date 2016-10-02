## DOL开发环境的配置 
#### **1. 关于DOL的简介和配置基础**
* ##### DOL的简介
DOL是一个并行应用的软件开发环境。支持多种并行运行的模型引擎，同时还支持基于xml规范格式描述的并行应用程序。

![dol](http://i1.piimg.com/567571/2816b7851abd9647.png)

* ##### 配置基础
	**Make工具**
	
	在linux和Ubuntu环境中编译工程和链接程序
	
	**Ant工具**
	
	java的扩展，用于build的一个脚本
	
	**java&javac**

	诸多插件脚本的运行基础

#### **2. 配置过程**

* ##### 下载文件 	
在linux下用sudo wget 从网络上下载systemC与dol的安装包
>$ sudo wget http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz 	
>$ sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip 

* ##### 解压文件

	新建dol的文件夹
	>$ mkdir dol

	将dolethz.zip解压到 dol文件夹中 	
	>$ unzip dol_ethz.zip -d dol

	解压systemc	
	>$ tar -zxvf systemc-2.3.1.tgz 	

* ##### 编译systemC

	解压后进入systemc-2.3.1的目录下
	>$ cd systemc-2.3.1

	新建一个临时文件夹objdir
	>$ mkdir objdir

	进入该文件夹objdir
	>$ cd objdir

	运行configure (能根据系统的环境设置一下参数，用于编译)
	>$ ../configure CXX=g++ --disable-async-updates

	![configure](http://i1.piimg.com/567571/0ad78ee72da124fd.jpg)

	编译
	>$ sudo make install

	编译完后文件目录如下
	>$ cd ..        
	>$ ls

	![ls](http://p1.bqimg.com/567571/00b6ccd2a9f5f17d.jpg)


	记录当前的工作路径(会输出当前所在路径，记下来，待会有用)
	>$	pwd

	*此时我当前的工作路径为 **/home/sunhan/systemc-2.3.1***

* ##### 编译Dol
	
	进入刚刚dol的文件夹
	>$ cd ../dol

	修改build_zip.xml文件

	**找到下面这段话，就是说上面编译的systemc位置在哪里**

		<property name="systemc.inc" value="YYY/include"/>
		<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>

	把YYY改成上页pwd的结果（注意，对于64位系统的机器，lib-linux要改成lib-linux64）

	然后是编译
	>$ ant -f build_zip.xml all

	若成功会显示build successful

	![build succsess](http://p1.bqimg.com/567571/d0e1d57b1d66d722.jpg)

	接着可以试试运行第一个例子
	进入build/bin/mian路径下
	>$ cd build/bin/main

	然后运行第一个例子
	>$ ant -f runexample.xml -Dnumber=1

	运行成功时控制台的输出

	![run success](http://p1.bpimg.com/567571/162452b8a03d309c.jpg)


	运行产生的文件
	>$ xdot example1.dot

	![run res](http://i1.piimg.com/567571/bca59e5edf281503.jpg)


#### **3. 实验感想&心得**

学习了Dol的基础原理应用等，并且在这个过程中深入了解许多linux指令，例如make，Makefile，而不是盲目的输入于命令行中。

还学习了一下安装插件xdot，再利用命令行运行应用程序，简单好用逼格高！

同时还打开了xml的大门，简单了解了他的语法规则。

此外，在这个过程中熟悉了md，熟悉了git的应用和linux上git的许多指令，总而言之，再接再厉！
