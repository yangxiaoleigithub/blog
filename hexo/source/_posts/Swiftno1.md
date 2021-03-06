title: Swift初见
date: 2014-12-15 20:37:55
categories: Swift
tags: ios
---
# Swift?什么是Swift？它是苹果最新的编程语言，在老码团队写的*《玩转Swift江湖》*一书中给Swift写了这么一段碑文
<!--more-->
## 1. Swift支持所有C和Object－C的基本类型，如整形（Integers）、浮点型（Floating－point Values）、布尔类型（Boolean Values）和文本类型（Textual Data）。


## 2. Swift还提供了两种功能强劲的集合类型（Collection types），Array和Dictionary。


##3. Swift还提供一种新的高级的类型，元组（Tuple），元组可以让你方便的创建和传递一元组数据，而且当它作为函数返回值时，可以一次返回多个数据。


##4. Swfit提供了一种新的声明方式，即可选类型（Optional typle），来处理空值。


##5. Swift支持字面变量扩展。


##6.Swift支持Lambda表达式、闭包的特性。

##7. Swift支持脚本语言的特性，但会高效地编译运行。

##8. Swift是一种类型安全的语言。

##9.Swift生于公元2014年6月，卒年不详。

---

自从苹果官方推出了Swift我就一直很关注它，因为它给了我接近苹果编程的兴趣，原本的Object－C那难懂的语法让我晕晕乎乎。从官方给出的数据来看，Object－C比Python快2.8倍，而Swift比Python快3.9倍，简直棒极了。

###  在这里给出现由成都老码维护的[Swift中文文档](https://github.com/numbbbbb/the-swift-programming-language-in-chinese)，非常适合我这种英文不好的屌丝来学习这高富帅的Swfit。

###我在这里所写的所有都不能和他们想提并论，我也不是在这里充当什么大神来分享技术，但是我写这些干什么呢？我想说给自己看吧，给自己的学习Swift过程有所纪录，学习的笔记吧。从Swift推出到现在我看过了3本书，第一个就是上边提到的Swift中文文档，第二本就是[《Swift语言快速入门》](http://item.jd.com/11551751.html)，第三本就是[《玩转Swift江湖》](http://item.jd.com/1411111300.html)。
---
###话不多说开始我的Swift之旅吧。

####第一个让我感觉到特别的就是类型别名（Type Aliases）
	类型别名就是可以给一个已经存在的类型定义一个别名，其关键字为typealias。来让我见识一下它的厉害吧！
	
	
```
typealias BookNumber = UInt
//给UInt起一个别名BookNumber
var myBookNumber: BookNumber = 3
//myBookNumber用来记录我的书的数目，类型为BookNumber。实则它的类型是无符号的Int类型
myBookNumber = -1
//我尝试着给它一个负数，Xcode立马就会显示出小红点，提示我这里出错了。

```
你会看到我上边的代码没有分号，是的，没有分号对于Swift来说是可以的。对变量的显性地声明类型就在变量名的后边加上冒号然后写上类型。
###类也是一种类型，那我是不是也可以给一个我自己创建的类也来个别名呢？试试吧。

```
class  BookNumbers{
    }
//声明一个BookNumbers类
typealias BookNumber = BookNumbers
//给BookeNumbers起一个类型别名BookNumber
var myBookNumbers = BookNumber()
//用类的别名来实例化一个对象

```
#### Nice,没有报错哦，还算可以的。

### 第二个让我感觉到不一样的就是元组
元组不同于数组和字典，元组可以把不同类型的数据放在一起，而数组和字典只能把相同类型的数据放在一起。
####元组的声明
```
var 邮编 = (城市: "太原",邮编号: "030000")
//邮编的类型为元组(String,Stringb)，其值为("太原","030000")
```
####元组解绑

我们要使用元组里面的值的时候需要对元组进行解绑


#####方法一
```
var 邮编 = (城市: "太原",邮编号: "030000")
//邮编的类型为元组(String,Stringb)，其值为("太原","030000")
let (城市,邮编号) = 邮编
println(" 城市是：\(城市)")
//打印结果是：城市是：太原
println("邮编号是：\(邮编号)")
//打印结果是：邮编号是：030000

```
#####方法二
如果我们只需要元组中的某些数据，可以用下划线来过滤掉元组中不需要关注的数据

```
var 邮编 = (城市: "太原",邮编号: "030000")
//邮编的类型为元组(String,Stringb)，其值为("太原","030000")
let (城市,_) = 邮编
println(" 城市是：\(城市)")
//打印结果是：城市是：太原
let (_,邮编号)  = 邮编
println("邮编号是：\(邮编号)")
//打印结果是：邮编号是：030000

```
##### 方法三

```
var 邮编 = (城市: "太原",邮编号: "030000")
//邮编的类型为元组(String,Stringb)，其值为("太原","030000")
println(" 城市是：\(邮编.0)")
//打印结果是：城市是：太原
println("邮编号是：\(邮编.0)")
//打印结果是：邮编号是：030000


```
##### 方法四
通过给元组里面的数据取名的方式

```
var 邮编 = (城市: "太原",邮编号: "030000")
//邮编的类型为元组(String,Stringb)，其值为("太原","030000")
println(" 城市是：\(邮编.城市)")
//打印结果是：城市是：太原
println("邮编号是：\(邮编.邮编号)")
//打印结果是：邮编号是：030000

```

##今天就先写到这里吧，感觉不好写呀，我要调整下思路，看怎么能更加深我对Swift的理解。


