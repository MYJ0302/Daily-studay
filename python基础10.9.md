#### (3)循环结构  
循环：指的是程序要重复执行某刻语句  

##### 1.while循环  
(1)简单的while循环
语法：
**变量赋初始值
While 条件表达式:
满足条件时才会执行循环语句**  

代码执行的过程：  
1.定义了一个变量，并赋初始值  
2.判断循环条件是否成立：
(1)如果成立，才会执行循环语句
(2)如果不成立，就不会执行循环语句  

(2)while语句与if、else语句结合使用
例：打印出1-10之间所有奇数和偶数 
'''python 
i = 1   
while i <= 10:  
if i % 2 == 0:
print(i, “是一个偶数”)
else:
print(i, “是一个奇数”)
i = i + 1
'''

(3)嵌套的while循环  
语法：
**循环变量赋初始值
while 循环条件1：
While 循环条件2：
满足循环条件2时执行的代码**  
例：使用while嵌套循环实现打印一个五行十列的*图形  
'''python
i = 1
while i <= 5:
    j = 1
    while j <= 10:
        print("*", end="")
        j = j + 1
    print()
    i = i + 1
'''
练习：使用一个while嵌套循环打印如下图形  

'''python
i = 1
while i <=4:
    j = 1
    while j <= i:
        print("*", end=" ")
        j = j + 1
    print()
    i = i + 1
'''
(4)while循环与continue、break结合使用  
Continue语句：用来结束本次循环，直接进入到下一次循环，并不会结束整个循环，即在执行循环语句的时候遇到continue，后面的代码不会执行  
Break语句：用来结束整个循环，在执行循环的过程中，不会继续判断循环条件是否成立，即不论条件是否成立，循环都不会继续执行
例：用来打印1-10之间所有的奇数的，跳过偶数的打印
'''python
i = 1
while i <= 10:
    if i % 2 == 0:
        i += 1
        continue
    print(i, "是一个奇数")
    i += 1
'''

(5)while循环与else语句结合使用  
语法：
**循环变量赋初始值  
While 循环条件：
满足循环条件时执行的代码  
Else：
语句块**
执行的过程：  
当while循环正常执行，中间没有break语句的时候，会执行else语句中的代码，但是，如果while循环语句有不惹事看语句，则else语句中的代码不会执行

##### 2.for循环  
For循环在使用的时候需要结合range()函数来实现  
(1)range函数的使用  
语法：  
**range(start, stop, step)**  
- start：表示计数从start开始（包含start），没写默认从0开始   
- stop：表示计数到stop结束（不包含stop）  
- step：表示步长，默认是1，表示会隔（step-1）个值，取下一个值，step可以是负数，表示方向。如果step是正数，表示从左往右取值。如果step是负数，表示从右往左取值。  
如果步长为正数，则start的值要比stop的值小  
如果步长为复数，则start的值要比stop的值大 

例：
'''python
for i in range(1,6):
    print(i)
'''
打印出结果：12345
'''
for i in range(6, 1,-2):
    print(i)
'''
打印出结果：6 4 2  

(2)简单的for循环  
如果循环变量不参与运算，一般习惯上写一个下划线
如果循环变量参与运算，就不会写下划线
例：打印have a good day 这句话十遍  
'''python
for i in range(10):
    print("have a good day")
'''

(3)for循环与if、else结合使用  
语法：
**for 循环变量 in序列：  
if 条件表达式1：  
语句块  
else：   
语句块**

