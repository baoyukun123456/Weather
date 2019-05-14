## while循环嵌套
+ 前面学习过if的嵌套了，想一想if嵌套是什么样子的？

+ 类似if的嵌套，while嵌套就是：while里面还有while
---
### <1>while嵌套的格式
    while 条件1:

        条件1满足时，做的事情1
        条件1满足时，做的事情2
        条件1满足时，做的事情3
        ...(省略)...

        while 条件2:
            条件2满足时，做的事情1
            条件2满足时，做的事情2
            条件2满足时，做的事情3
            ...(省略)...
### <2>while嵌套应用一
要求：打印如下图形：

    *
    * *
    * * *
    * * * *
    * * * * *
参考代码：

    i = 1
    while i<=5:

        j = 1
        while j<=i:
            print("* ",end='')
            j+=1

        print("\n")
        i+=1
### <3>while嵌套应用二：九九乘法表

![alt文本](Images/Snip20161017_87.png "Title")

参考代码：

    i = 1
    while i<=9:
        j=1
        while j<=i:
            print("%d*%d=%-2d "%(j,i,i*j),end='')
            j+=1
        print('\n')
        i+=1
