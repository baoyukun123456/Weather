## while循环应用
### 1. 计算1~100的累积和（包含1和100）
参考代码如下:

    #encoding=utf-8
    i = 1
    sum = 0
    while i<=100:
        sum = sum + i
        i += 1

    print("1~100的累积和为:%d"%sum)
### 2. 计算1~100之间偶数的累积和（包含1和100）
参考代码如下:

    #encoding=utf-8

    i = 1
    sum = 0
    while i<=100:
        if i%2 == 0:
            sum = sum + i
        i+=1

    print("1~100的累积和为:%d"%sum)
