## shell编程
### linux内置变量的访问形式
|参数|说明
|---|---
|$?	|命令的返回值储存变量，返回刚刚执行命令的结果，0：不成功、!=0：失败
|$#	|获取参数个数
|$n   |获取第n个参数， $0：命令本身 $1：第一个参数...
|$@	|	得到所有参数
|shift	|   向左移动参数，左边的参数被覆盖掉


### linux内置命令
#### 1. if  

    #!/bin/bash
    if(($# < 1));then
		echo no param!!!
		exit;
	fi
#### 2. for
##### 0.查看帮助
    help for
##### 1.语法一
    for  NAME in world ...;do sss;done
    [例如]
    for a in 1 2 3 4;do echo $a;done
##### 2.语法二
    for（（；；））；do ;done
#### 3. while
##### 语法
    while ();do commands;done
##### 用法
    #!/bin/bash
    a=1
    while((a<=10));do echo $a
    a=a+1
    done

### 命令组合
1. a&&b  
    a成功后再执行b命令
2. a||b  
    a执行失败再执行b命令
3. a;b  
    多行命令一起写
4. （a;b）  
    同上，当前目录执行，不切换目录
