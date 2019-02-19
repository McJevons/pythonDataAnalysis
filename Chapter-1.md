Anaconda是python的一个环境管理工具，刚准备开始接触，先从安装配置开始学。

### 1-1 <span id='1-1'>下载安装</span>

先下载最新版本的Anaconda5.3.1：[https://www.anaconda.com/download](https://www.anaconda.com/download)  
这个版本包含了python3.7版本，而我电脑上已经有了python3.6版本，不知道到时怎么切换，先安装了再慢慢琢磨。  
安装过程不说了，在安装时让我选择是否将其添加进环境变量path里，提示是不建议添加因为会干扰其他软件，可以在安装完成后通过Anaconda Navigator或Anaconda Prompt运行。  
安装完成后运行Anaconda Navigator，界面如下：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181122205328233.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pld2VseQ==,size_16,color_FFFFFF,t_70)

### 1-2 <span id='1-2'>关于vscode及python版本的切换</span>

在Navigator里发现还可以安装vscode，而我电脑里已经安装过了vscode，不知道如果安装了它里面的vscode会不会冲突，手痒点击了install，没任何提示自动开始下载安装，也没有取消按钮，有点紧张生怕以前的vscode配置会丢失。等安装完成后点击lanch运行里面的vscode，然后我在进程管理器查看运行的vscode文件所在位置，原来就是我以前那个vscode，但提示有的vscode插件不存在。在vscode终端查看python版本是3.7版。开始怀疑以前的python3.6是不是已经不起作用了，调出windows的cmd窗口运行查看python版本，还好还是3.6的，再运行以前的vscode查看python版本，也是3.6，看来Anaconda有点像沙盒，在其里面运行的程序比如vscode，会自动使用Anaconda建立的环境，包括python3.7版本以及独立的vscode配置，而单独运行vscode还是使用3.6版本和原先的配置，怪不得安装时不建议把Anaconda添加到环境变量里，不然就没办法这么容易切换版本了。  
这样的话，要使用3.7版本，必须所有操作都在Anaconda里进行，在其外执行的任何python都是3.6版本。  
（关于vscode的说法好像有些不对，因为我又换了个win7电脑，同样的操作，但Anaconda里的vscode直接安装到了系统盘里，而不是覆盖安装原来的vscode，但两个vscode都共用一个存放在user目录里的配置，因此配置相同。另外很奇怪为什么新装的vscode包含的插件也与原来的vscode一样，不知道配置文件里是不是也包含了已安装插件，因此新vscode会自动安装插件）

### 1-3 <span id='1-3'>安装第三方包</span>

在Anaconda Navigator界面的环境项里，可以看到有个默认的base\(root\)环境，这就是Anaconda里的python3.7环境，旁边列表是已经安装的各种第三方包。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181122214446223.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pld2VseQ==,size_16,color_FFFFFF,t_70)  
运行Anaconda Prompt调出命令行模式，用`pip install pymssql`添加一个mssql支持库，但安装完成后在列表中并未显示出来，但可以正常使用。看到网上说在Anaconda环境里建议使用conda命令安装第三方包，于是先把pymssql卸载，然后使用`conda install pymssql`命令安装，安装完成重启Navigator后，在列表中可以看到pymssql库了。  
卸载可使用`conda remove pymssql`或者`conda uninstall`命令，使用`pip uninstall pymssql`命令也可以卸载，但列表无法更新，仍旧还可以看到。

### 1-4 <span id='1-4'>修改下载源为国内镜像</span>

在Prompt里执行命令即可：

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
```

### <span id='abc'>1-5 环境管理</span>



##### 新建环境

在Navigator里的环境项Environments里，可以进行环境管理，点击Create可以添加新的环境，或者在Prompt里执行命令`conda create -n py36 python=36`，会自动下载python3.6版本，并新建一个名为py36的python3.6运行环境。这个新的python3.6安装路径在Anaconda安装目录的envs目录里。  
另外在Navigator的环境项里还有克隆及移除环境选项。

##### 查看环境列表

命令：`conda env list`  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181122220212472.png)

##### 切换环境

Navigator的home项里可以选择查询使用哪种环境运行  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181122220950261.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pld2VseQ==,size_16,color_FFFFFF,t_70)  
也可以在Prompt里执行切换命令`activate py36`，提示符前面的\(base\)会变为\(py36\)，但这个切换似乎只对Prompt起作用，并不影响Navigator里程序运行的环境，另外重启Prompt后仍旧是默认的\(base\)环境。

##### 新环境的第三方包

新环境除了几个必要的包外，是不包含其他第三方包的，可以使用conda命令进行安装，也可以在Navigator的环境里，选择新环境，显示not installed包列表，这里可以看到其他环境里安装过的包，勾选需要安装的包，点击apply进行安装。但并不清楚这种安装方法是直接把其他环境的包复制过来还是重新下载安装？  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181122222309591.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2pld2VseQ==,size_16,color_FFFFFF,t_70)

##### 使用已存在的python建立新环境

由于我电脑里的python已经使用了一段时间，安装了不少包，如果在Anaconda默认环境或者新建环境里，要重新安装这些包，因此考虑是否可以根据已存在的python建立新的环境。  
把原来的python3.6安装目录Python36复制到envs目录，然后选择添加新环境，但在Navigator里只能选择3.6版本，其实安装的是3.6.3版本，而我用的是3.6.0版本，因此使用命令建立环境`conda create -n Python36 python=3.6.0`，**环境名必须和目录名相同**。  
执行命令后，也不检测是否已经存在了，而是傻乎乎的重新下载python，覆盖安装到我复制过来的目录里，完成后查看包列表，仍旧只有几个必须的包。但注意到包列表上方有个`Update index...`按钮，不知道什么作用，但感觉有点用处，点了试试看，在列表下方出现了`updating package index and metadata...`滚动条，片刻果真所有的包都出现在列表里了。  
再试试看，不复制以前的python目录，新建一个环境，然后只把以前python目录里的包目录lib内容复制到新环境的包目录里，然后update index，所有包也出现在了包列表中。但这些包没有pip install也没conda install，可用吗？测试了下，看来是我多虑了，完全可用。

至此，以后可以方便的进行各种python版本切换，不怕影响其他设置了。

