## elif
+ 想一想:  
        if能完成当xxx时做事情

        if-else能完成当xxx时做事情1，否则做事情2

        如果有这样一种情况：当xxx1时做事情1，当xxx2时做事情2，当xxx3时做事情3，那该怎么实现呢？

+ 答:

        elif
---
### <1> elif的功能
+ elif的使用格式如下:  
        if xxx1:
            事情1
        elif xxx2:
            事情2
        elif xxx3:
            事情3
+ 说明:  
        当xxx1满足时，执行事情1，然后整个if结束
        当xxx1不满足时，那么判断xxx2，如果xxx2满足，则执行事情2，然后整个if结束
        当xxx1不满足时，xxx2也不满足，如果xxx3满足，则执行事情3，然后整个if结束
+ demo:  
        score = 77
        if score>=90 and score<=100:
            print('本次考试，等级为A')
        elif score>=80 and score<90:
            print('本次考试，等级为B')
        elif score>=70 and score<80:
            print('本次考试，等级为C')
        elif score>=60 and score<70:
            print('本次考试，等级为D')
        elif score>=0 and score<60:
            print('本次考试，等级为E')
### <2> 注意点
+ 可以和else一起使用  
       if 性别为男性:
           输出男性的特征
           ...
       elif 性别为女性:
           输出女性的特征
           ...
       else:
           第三种性别的特征
           ...
说明:  
        + 当 “性别为男性” 满足时，执行 “输出男性的特征”的相关代码
        + 当 “性别为男性” 不满足时，如果 “性别为女性”满足，则执行 “输出女性的特征”的相关代码
        + 当 “性别为男性” 不满足，“性别为女性”也不满足，那么久默认执行else后面的代码，即 “第三种性别的特征”相关代码
+ elif必须和if一起使用，否则出错
