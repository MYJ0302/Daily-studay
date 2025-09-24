# <center>Linux第一天</center>
## 一、linux常用命令  
#### 1.基础命令
##### 1）查看当前系统名称或修改当前系统名称&emsp;&emsp; <font color=red>hostname</font>  
- 查看当前系统名称 <font color=blue>hostname</font> 
- 修改当前系统名称 <font color=blue>hostname 新名字</font> （设置完成后，关闭终端再打开就会生效） 
  
##### 2）查看当前系统时间和日历  
- 查看当前系统时间 <font color=blue>del</font>
- 查看当前系统日历 <font color=blue>date</font>  

##### 3）帮助命令&emsp;&emsp; <font color=red>man</font>  
&emsp;使用格式：<font color=blue>man  需要查看的命令</font>  
##### 4）查看当前工作目录&emsp;&emsp;<font color=red>pwd</font>  
&emsp;&emsp;在Linux系统中创建目录或文件之前，一定一定一定要知道自己当前在哪里  
#### 2.用户和组命令 &emsp;&emsp;<font color=green>管理员可用</font>  
&emsp;&emsp;Linux系统可以创建用户和组。创建用户时，用户就会创建同名组，并且将用户和组进行关联。
##### 1）与用户和组有关文件  
- 当创建完成用户后，可以查看用户信息：  与用户有关文件&emsp;&emsp;<font color=blue>/etc/passwd </font>  
- 当创建组，可以查看组信息：与组有关文件&emsp;&emsp;<font color=blue>/etc/group</font>   
- 存放用户密码文件：&emsp;&emsp;<font color=blue>/etc/shadow</font>   

##### 2）创建组  &emsp;&emsp; <font color=red>groupadd</font>  
格式：<font color=blue>groupadd   [命令选项]  组名称</font>&emsp;&emsp;说明：中括号中内容是可有可无的  
命令选项：  
<font color=blue>-g  新建组的编号</font> &emsp;&emsp;编号唯一   
编号1000---9999之间  

##### 3）创建用户 &emsp;&emsp; <font color=red>useradd</font>  
格式：<font color=blue>useradd  [命令选项]  用户名</font>
命令选项：
- <font color=blue>-u</font>   &emsp;&emsp; 用户分配编号
- <font color=blue>-g</font>   &emsp;&emsp; 用户所属主组编号或名称        &emsp;&emsp; 主组：大学主修专业    &emsp;&emsp; 只能有一个
- <font color=blue>-G</font>   &emsp;&emsp; 用户所属附加组（附属组）编号或名称      &emsp;&emsp; 附属组：大学加入各种社团    &emsp;&emsp; 可以有多个
- <font color=blue>-d</font>   &emsp;&emsp; 用户家目录路径                 &emsp;&emsp; 指定该用户家目录  
- 
&emsp;&emsp;查看创建成功后用户信息，使用命令：<font color=blue>id   用户名</font> ，还可以使用   <font color=blue>groups   用户名</font>
<font color=blue>clear</font>： 清理屏幕
<font color=blue>tab</font> ：自动补齐  
useradd使用说明：
（1）useradd中使用组名称或组编号一定是已存在 （已经被创建好）
（2）useradd中的用户编号是唯一的
<font color=blue>useradd  -d</font>  创建用户家目录  

##### 4）删除用户 &emsp;&emsp;<font color=red>userdel</font>  
格式：<font color=blue>userdel  [命令选项]   用户名</font>
命令选项：  
<font color=blue>-r</font>&emsp;&emsp;删除用户的同时，将该用户所有信息都删除（包括家目录） 

##### 5）删除组&emsp;&emsp;<font color=red>groupdel</font>   
格式：<font color=blue>groupdel  组名称</font>  
注意事项：  
（1）需要删除的这个组没有任何用户时，可以随时删除  
（2）但是需要删除组有成员，两个处理方式：
- 删除该组中用户，然后再删除组
- 将该组中用户，修改到其他组下，然后再删除组  

##### 6）修改用户&emsp;&emsp;<font color=red>usermod</font>  
格式：<font color=blue>usermod [命令选项] 需要修改用户</font>
命令选项：
- <font color=blue>-u 用户编号</font>&emsp;&emsp;修改用户的编号uid
- <font color=blue>-g主组编号</font>&emsp;&emsp;修改用户的主组gid
- <font color=blue>-a -G  附属组的编号</font>&emsp;&emsp;修改了用户附属组，可以将用户添加到附属组

