title: Swift菜鸟学习第一天
date: 2014-12-18 01:50:35
categories: Swift
tags: ios
---
#蜗牛君之[菜鸟30天Swift笔记](http://muzining.github.io/swift-cookbook/index.html)，我来学习。因为艺哥写的比较早，很多语法已经更改了，那我们就来正式的语法来重新学习一下。
<!--more-->
## 之前的第一篇关于Swift的博客写了之后自我感觉很是不好，因为很多东西还不是现在的我所能总结出来的。所以，我接下来就以蜗牛君之前写过的菜鸟30天Swift笔记为基准，自己也来写一遍，但肯定不会照搬艺哥的，那样的话就没有意义了。

---
##菜鸟第一天，排列问题


###问题

有1、2、3、4个数字，能组成多少个互不相同且无重复数字的三位数？这些组合，都是多少？

```
var number = ""
	var count = 0

	for var i=1;i<5;++i {
    	for var j=1;j<5;++j {
        	for var k=1;k<5;++k {
            	if i != j && j != k && k != i {
                	number += "\(i) \(j) \(k), "
               	 	++count
            	}
        	}
    	}
	}
	println("组成\(count)个互不相同的无重复的三位数")
	println("分别是：\(number)")
	
	//输出结果是：
	//组成24个互不相同的无重复的三位数
	分别是：1 2 3, 1 2 4, 1 3 2, 1 3 4, 
	1 4 2, 1 4 3, 2 1 3, 2 1 4, 2 3 1, 
	2 3 4, 2 4 1, 2 4 3, 3 1 2, 3 1 4, 
	3 2 1, 3 2 4, 3 4 1, 3 4 2, 4 1 2, 
	4 1 3, 4 2 1, 4 2 3, 4 3 1, 4 3 2, 
```	

#### 代码中第一行`var number = ""`,是声明了一个空的字符串，其中`var`关键字用于声明一个变量。Swift是一个强类型安全语言，即使你没有显性的标注类型，Swift仍然可以进行正确的类型推断。所以Swift推断*number*的类型为字符串。同理，`var count = 0`则推断*count*为Int类型。对于`\(i)`，表示将变量i插入到字符串，是swift字符串插值的一个用法。其中`\(j)`便表示将变量j插入到字符串中等。

那么Swift怎么进行类型标注呢？看下边的代码：


```
var number : String = ""
	var count : Int = 0
```
#### 在变量名的后边加上冒号，再紧跟着类型名称。
---
## 使用区间操作符

刚才的代码是用了三个for循环的嵌套，在Swift中，for循环有一种更简洁的写法，即使用闭区间操作符。上面的代码可改成：

```
for i in 1...4 {
    for j in 1...4 {
        for k in 1...4 {
            if i != j && j != k && k != i {
                number += "\(i) \(j) \(k), "
                ++count
            }
        }
    }
}

	
```
#### 那么想必你已经猜出来了，`1...4`代表的就是闭区间的[1,4]，同样，..<是左闭右开区间操作符，如1..<5表示区间[1，5)。于是，上面代码又可以改写成：

```
for i in 1..<5 {
    for j in 1..<5 {
        for k in 1..<5 {
            if i != j && j != k && k != i {
                number += "\(i) \(j) \(k), "
                ++count
            }
        }
    }
}
```

##通用的排列算法

蜗牛君在这里还给出了一个通用的排列算法，让我们一起来看看是怎么回事吧。

[百度文库对全排列算法的详解](http://wenku.baidu.com/link?url=w110uh09kg5CmW4DEV8QYV2uidW-l51dOc58HN94ZIv-fNjl7mHcaAAZeVxK90GWQz1rmdCP5WPkrseBv59QKLR9HysJmVZJ1istUs_xxr_)



