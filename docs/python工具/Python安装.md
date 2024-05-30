# Python安装

**一、什么是Python环境**

参考文档：https://cloud.tencent.com/developer/article/2124483

1. Python环境主要由运行python解释器的位置所决定**，**python环境查找当我们在执行`main.py`的时候，python哪里来，这个主要归功于配置的系统环境变量PATH；当我们在命令行中运行程序时，系统会根据PATH配置的路径列表依次查寻是否有可执行文件python.exe；当查寻到该文件时执行该文件， 如果在所有路径列表中都查找不到，就会报报错python不是内部或外部命令，也不是可运行的程序或批处理文件

2. `main.py`代码中import的模块在哪里找? import的模块包含两类，一类称为标准库，随着python的安装而安装；另一类称为第三方库，使用pip工具或者自己手动安装的包，模块的搜索路径可通过sys.path查看，主要由可执行文件python所在的位置所决定

3. Python环境主要包括以下内容，①解释器 python.exe，②Lib目录下保护标准库和site-pakages目录(默认安装第三方库所在的目录)，③Scripts目录，包含一些执行文件，包安装管理工具pip.exe和打包工具pyinstaller.exe（需要自己安装）

**二、什么是Python虚拟环境**

1. 有两个项目A和B，如果A和B都要用到某一模块，但版本不相同怎么办

2. 为了解决上面的问题，python使用了虚拟环境这个概念，你可以认为是python环境的多个副本，只是在不同的副本中安装了不同的包；既然叫虚拟环境，总得有点不一样，虚拟环境中一般不包含标准库，不包含python解释器运行时所需的依赖文件，可执行文件全部放于Scripts目录等

3. 后面介绍到pycharm的时候，选择虚拟环境，此处先忽略这个

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFk5eEtuXM57lI1yz7VhMP744akIE-d89d53.png)

**三、安装步骤**

1. 先下载，如下windows选择这个就可以

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFoy85jqpJMm2SfgHph4bwW0q0Fnp-ea3663.png)

2. 如下为下载好的exe软件

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFv_stgrRHVucVqdebWaKq7JVxL1s-4aa356.png)

3. 勾选add to path , 选择自定义安装

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnVM7C-koXWTOnWw2AZW1-bJx8GN-dc6b96.png)

4. 直接next

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFjOggvtg0jXkUf96ZT86NS2nWyM3-ce37c7.png)

5. 自定义安装路径

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFizV2k59foYXVAd5rREz4kZ2JiLo-7e0f89.png)

6. 大概1分钟左右就安装好了，然后close掉就行

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFi3S9TB4TIzEhreXeo5mjxK4GuUV-913d44.png)

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFirhc6E8T5rMGXBNr2YCi3An6-iM-fe9e26.png)

7. win+R快捷键，输入cmd，打开cmd窗口

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFr0NgrG8L3dKyqnUtsm2bm8SNQwb-e69e60.png)

8. 在cmd窗口输入where python可以看到当前python环境在哪个文件夹下；输入python可以进入python环境，测试输出print("hello word")，如下代表python环境安装成功了；输入exit()代表退出python编辑环境

![img](https://cdn.jsdelivr.net/gh/Killer-89757/PicBed/images/2024%2F05%2FFnTZClog_QAOZsLqNWTir5aa33EL-4219a4.png)

