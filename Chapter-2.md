## jupyter notebook优点

前几天装好了Anaconda，但一直没弄明白里面的jupyter notebook到底有什么好处。感觉就是一个在网页里运行代码的工具。  
研究了两天，渐渐发现优点了：

* 支持markdown，并且是所见及所得，编辑好一段文字后`Shift+Enter`即可即时看到文字效果，重新点击再`Enter`可以继续编辑；
* 可以很方便的在同一页面里既写文档又编辑运行代码，而以前需要开一个文档窗口一个代码窗口，还要手工将代码及运行结果复制到文档里；
* 已经运行的代码可以返回重新编辑，然后再次运行，以前如果运行代码时，发现之前的代码有错误，需要将出错的代码修改后重新运行，之后的其他代码也需要再次重新输入运行，而notebook可以直接点击编辑出错的代码，然后选择重新运行所有代码。

## 修改notebook默认目录

windows下notebook的默认目录是用户目录，这当然不是很方便，因此需要修改下默认目录。  
1. 运行Anaconda Prompt终端，输入以下命令查看配置文件路径：

```
jupyter notebook --generate-config
```

1. 根据上面的路径，找到并打开配置文件jupyter\_notebook\_config.py，查找配置项c.NotebookApp.notebook\_dir，去除注释标志，并修改内容为需要的目录，注意windows需要使用\；
2. 重启jupyter notebook。

## 常用快捷键

* 执行当前cell，并自动跳到下一个cell：Shift Enter

* 执行当前cell，执行后不自动调转到下一个cell：Ctrl-Enter

* 是当前的cell进入编辑模式：Enter

* 退出当前cell的编辑模式：Esc

* 删除当前的cell：双D

* 为当前的cell加入line number：单L

* 将当前的cell转化为具有一级标题的maskdown：单1

* 将当前的cell转化为具有二级标题的maskdown：单2

* 将当前的cell转化为具有三级标题的maskdown：单3

* 为一行或者多行添加/取消注释：Crtl /

* 撤销对某个cell的删除：z

* 浏览器的各个Tab之间切换：Crtl PgUp和Crtl PgDn

* 快速跳转到首个cell：Crtl Home

* 快速跳转到最后一个cell：Crtl End

---

作者：tina\_ttl  
来源：CSDN  
原文：[https://blog.csdn.net/tina\_ttl/article/details/51031113](https://blog.csdn.net/tina_ttl/article/details/51031113)

## 魔术命令

魔术命令其实是IPython的特殊命令，以%开头，用以完成特定任务，jupyter notebook基于IPython的，因此也可以使用魔术命令。

* %load 导入脚本，可以从文件导入，也可以使用url导入。导入后第一行显示导入命令，后面显示脚本的内容。
  例如执行`%load test.py`，结果如下：

```python
In [2]: %load test.py

In [3]: # %load test.py
   ...: import numpy as np
   ...: 
   ...: arr=np.array([1,2,3,4])
   ...: print(arr)
   ...: 
   ...: 
[1 2 3 4]
```

* %run 执行脚本命令

```python
In [4]: %run test.py
[1 2 3 4]
```

* %pwd 显示当前目录路径

```python
In [5]: %pwd
Out[5]: 'I:\\Users\\McJevons'
```

* %timeit 计算单行命令的执行时间，%%timeit 计算多行命令的执行时间

```
In [6]: %timeit n=[a**2 for a in range(10000)]
5.4 ms ± 276 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)

In [7]: %%timeit
   ...: n=[]
   ...: for a in range(10000):
   ...:     n.append(a**2)
   ...: 
5.93 ms ± 120 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
```

* %reset 删除所有变量

```python
In [8]: arr
Out[8]: array([1, 2, 3, 4])

In [9]: %reset

Once deleted, variables cannot be recovered. Proceed (y/[n])? y

In [10]: arr # 变量arr已经不存在了
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-10-a221b3019642> in <module>()
----> 1 arr # 变量arr已经不存在了

NameError: name 'arr' is not defined
```

* %xdel 删除单个变量

```python
In [11]: arr=[1,2,3,4]

In [12]: arr
Out[12]: [1, 2, 3, 4]

In [13]: %xdel arr

In [14]: arr
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-14-24a6d41c5b66> in <module>()
----> 1 arr

NameError: name 'arr' is not defined
```

* ? 查看帮助



