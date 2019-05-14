## import导入模块

### 1. import 搜索路径

import sys  
sys.path  

![alt文本](Images/Snip20161106_8.png "Title")  

路径搜索

* 从上面列出的目录里依次查找要导入的模块文件
* ' ' 表示当前路径  

程序执行时导入模块路径

    sys.path.append('/home/itcast/xxx')
    sys.path.insert(0, '/home/itcast/xxx')    #可以确保先搜索这个路径
    In [37]: sys.path.insert(0,"/home/python/xxxx")
    In [38]: sys.path
    Out[38]:
    ['/home/python/xxxx',
     '',
     '/usr/bin',
     '/usr/lib/python35.zip',
     '/usr/lib/python3.5',
     '/usr/lib/python3.5/plat-x86_64-linux-gnu',
     '/usr/lib/python3.5/lib-dynload',
     '/usr/local/lib/python3.5/dist-packages',
     '/usr/lib/python3/dist-packages',
     '/usr/lib/python3/dist-packages/IPython/extensions',
     '/home/python/.ipython']  

### 2. 重新导入模块

模块被导入后，import module不能重新导入模块，重新导入需用
* 测试模块内容  
![alt文本](Images/Snip20161106_9.png "Title")

* 调用模块中的方法  
![alt文本](Images/Snip20161106_10.png "Title")

* 修改测试模块  
![alt文本](Images/Snip20161106_11.png "Title")

* 重新加载模块  
![alt文本](Images/Snip20161106_12.png "Title")
