### Shell脚本练习
### 1、比较两个数的大小
#### test命令学习
|test命令|说明
|---|---
|1）判断表达式
|if test  |(表达式为真)
|if test ! |表达式为假
|test 表达式1 –a 表达式2    |              两个表达式都为真
|test 表达式1 –o 表达式2     |            两个表达式有一个为真
|2）判断字符串
|test –n 字符串                |                   字符串的长度非零
|test –z 字符串                |                    字符串的长度为零
|test 字符串1＝字符串2             |       字符串相等
|test 字符串1！＝字符串2            |   字符串不等
|3）判断整数
|test 整数1 –eq 整数2            |            整数相等
|test 整数1 –ge 整数2             |           整数1大于等于整数2
|test 整数1 –gt 整数2              |           整数1大于整数2
|test 整数1 –le 整数2               |          整数1小于等于整数2
|test 整数1 –lt 整数2                |          整数1小于整数2
|test 整数1 –ne 整数2                 |       整数1不等于整数2
|4）判断文件
|test  File1 –ef  File2            |                两个文件具有同样的设备号和i结点号
|test  File1 –nt  File2             |               文件1比文件2 新
|test  File1 –ot  File2              |              文件1比文件2 旧
|test –b File                         |                  文件存在并且是块设备文件
|test –c File                          |                 文件存在并且是字符设备文件
|test –d File                           |                文件存在并且是目录
|test –e File                            |               文件存在
|test –f File                             |               文件存在并且是正规文件

答案
    #!/bin/bash  
    echo "please enter two number"  
    read a      //传参
    read b  
    if test $a -eq $b   当我们检查文件是否存在，或者检查文件的属性时，可以使用test命令。例如检测/abc是否存在，可以用:
                        test -e /abc && echo "exist" || echo "not exist"
    then echo "NO.1 = NO.2"  
    elif test $a -gt $b  
    then echo "NO.1 > NO.2"  
    else echo "NO.1 < NO.2"   
    fi  

### 2、添加10个用户user1到user10
       #!/bin/bash
       for ((i=1;i<11;i=i+1));do            | 表示管道，上一条命令的输出，作为下一条命令参数，如 echo 'yes' | wc -l
                                            || 表示上一条命令执行失败后，才执行下一条命令，如 cat nofile || echo "fail"
       useradd user$i
       done
### 3、传递两个整数给脚本，让脚本分别计算并显示这两个整数的和，差，积，商
    #!/bin/bash
    echo "first number $1"  （表示输出第一个数）
    echo "second number $2" （表示输出第二个数）
    echo " $(($1+$2))"      （输出两数之和）
    echo "$[$1-$2]"         （输出两数之差）
    echo "$[$1*$2]"         （输出两数之积）
    echo "$[$1/$2]"         （输出两数之商）
### 4、函数
    #!/bin/bash
    p ()  
    {  
        echo "hello"  
    }  
    p  
### 5、给函数传递参数
    #!/bin/bash  
    p_num ()  
    {  
        num=$1  
        echo $num  
    }  
    for n in $@  
    do  
        p_num $n  
    done
### 6、创建文件夹
    #!/bin/bash  
    while :  
    do  
        echo "please input file's name:"  
        read a  
        if test -e /root/$a  
        then  
             echo "the file is existing Please input new file name:"  
        else  
            mkdir $a  
            echo "you aye sussesful!"  
            break   
        fi  
    done


## 作业
### 作业一
1. 显示当前系统日期和时间，而后创建目录/tmp/lstest
2. 切换工作目录至/tmp/lstest
3. 创建目录a1d，b56e，6test
4. 创建空文件xy，x2y，732
5. 列出当前目录下以a，x或者6开头的文件或目录
6. 列出当前目录下以字母开头，后跟一个任意数字，而后跟任意长度字符的文件或目录
### 作业二
1. 通过ping命令测试192.168.0.151到192.168.0.254之间的所有主机是否在线
2. 如果在线，就显示“ip is up”
3. 如果不在线，就显示“ip is down”

### 作业三
1.切换工作目录至/var
2.依次向/var目录中的每个文件或子目录问好，形如：
（提示：for FILE in /var/*;或for FILE in `ls /var`;)
Hello,log
3.统计/var目录下共有多个文件，并显示出来
