# agenda
 
## 小组成员
### 利建鑫（master）
主要贡献：会议查询、创建、取消、退出、清空，增删会议参与者，持久化json的实现,cmd。
### 刘洋旗
主要贡献：用户注册、登陆、登出、查询、删除，log服务，cmd。
 
## 任务目标：
1.熟悉 go 命令行工具管理项目

2.综合使用 go 的函数、数据结构与接口，编写一个简单命令行应用 agenda

3.使用面向对象的思想设计程序，使得程序具有良好的结构命令，并能方便修改、扩展新的命令,不会影响其他命令的代码

4.项目部署在 Github 上，合适多人协作，特别是代码归并

5.支持日志（原则上不使用debug调试程序）
 
## 主要使用工具&方法
### cobra
cobra提供的功能：
1.简易的子命令行模式，如 app server， app fetch等等

2.完全兼容posix命令行模式

3.嵌套子命令subcommand

4.支持全局，局部，串联flags

5.使用Cobra很容易的生成应用程序和命令，使用cobra create appname和cobra add cmdname

6.如果命令输入错误，将提供智能建议，如 app srver，将提示srver没有，是否是app server

7.自动生成commands和flags的帮助信息

8.自动生成详细的help信息，如app help

9.自动识别-h，--help帮助flag

10.自动生成应用程序在bash下命令自动完成功能

11.自动生成应用程序的man手册

12.命令行别名

13.自定义help和usage信息

14.可选的紧密集成的viper apps
 
cobra具体使用方法参见：https://studygolang.com/articles/7588

具体实践代码地址：agenda/src/agenda/cmd
 
### json
1.encode:

1.1 将一个对象编码成JSON数据，接受一个interface{}对象，返回[]byte和error：

1.2 func Marshal(v interface{}) ([]byte, error)

1.3 Marshal函数将会递归遍历整个对象，依次按成员类型对这个对象进行编码，类型转换规则如下：

1.4 bool类型 转换为JSON的Boolean

1.5 整数，浮点数等数值类型 转换为JSON的Number

1.6 string 转换为JSON的字符串(带""引号)

1.7 struct 转换为JSON的Object，再根据各个成员的类型递归打包

1.8 数组或切片 转换为JSON的Array

1.9 []byte 会先进行base64编码然后转换为JSON字符串

1.10 map 转换为JSON的Object，key必须是string

1.11 interface{} 按照内部的实际类型进行转换

1.12 nil 转为JSON的null

1.13 channel,func等类型 会返回UnsupportedTypeError

2.decode:

2.1 将JSON数据解码

2.2 func Unmarshal(data []byte, v interface{}) error

2.3 类型转换规则和上面的规则类似

3.结构体：

3.1 结构体必须是大写字母开头的成员才会被JSON处理到，小写字母开头的成员不会有影响。

3.2 Mashal时，结构体的成员变量名将会直接作为JSON Object的key打包成JSON；Unmashal时，会自动匹配对应的变量名进行赋值，大小写不敏感。

3.3 Unmarshal时，如果JSON中有多余的字段，会被直接抛弃掉；如果JSON缺少某个字段，则直接忽略不对结构体中变量赋值，不会报错。

 
其他未使用情况不做赘述，json具体使用方法参见：http://blog.csdn.net/tiaotiaoyly/article/details/38942311

具体实践代码地址：agenda/src/agenda/entity/storage

### log
log具体使用方法参见：http://blog.csdn.net/cza55007/article/details/46039279

具体实践代码地址：agenda/log
 
## 实验结果
注：命令使用方法参见cmd_design.md

1.运行main.go

![image](https://github.com/ishoping/agenda/blob/master/image/res_1.png)

2.用户注册

![image](https://github.com/ishoping/agenda/blob/master/image/res_2.png)

3.列出所有用户

![image](https://github.com/ishoping/agenda/blob/master/image/res_3.png)

4.用户登录

![image](https://github.com/ishoping/agenda/blob/master/image/res_4.png)

5.删除用户

![image](https://github.com/ishoping/agenda/blob/master/image/res_5.png)

6.错误信息登录

![image](https://github.com/ishoping/agenda/blob/master/image/res_6.png)

7.注册重名用户

![image](https://github.com/ishoping/agenda/blob/master/image/res_7.png)


8.测试对象

 
![image](https://github.com/ishoping/agenda/blob/master/image/res_8.png)

9.创建会议

![image](https://github.com/ishoping/agenda/blob/master/image/res_9.png)

10.删除会议参与者

![image](https://github.com/ishoping/agenda/blob/master/image/res_11.png)

11.删除会议

![image](https://github.com/ishoping/agenda/blob/master/image/res_12.png)

