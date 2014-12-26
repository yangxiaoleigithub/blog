title: Swift菜鸟学习第二天
date: 2014-12-20 00:29:32
categories: Swift
tags: ios
---
# 奖金问题，主要学习：变量参数，不管穿原则，元组。
<!-- more -->
### 参考[菜鸟30天学习Swift笔记](http://muzining.github.io/swift-cookbook/chapter1/2.html)
##问题：

企业发放的奖金根据利润提成:

. 利润低于或等于10万元时，奖金可提10%；

. 利润高于10万元，低于20万元时，低于10万元的部分按10%提成，高于10万元的部分，可提成7.5%；

. 20万到40万之间时，高于20万元的部分，可提成5%；

. 40万到60万之间时高于40万元的部分，可提成3%；

. 60万到100万之间时，高于60万元的部分，可提成1.5%;

. 高于100万元时，超过100万元的部分按1%提成。

已知当月利润n，求应发放奖金总数？

---
## 使用if else
```
func calcBonus(var 当月利润 n:Int) -> Double {
    var bonus = 0.0
    if n > 100_0000 {
        bonus += Double(n - 100_0000) * 0.01
        n -= 100_0000
    }
    if n > 60_0000 {
        bonus += Double(n - 60_0000) * 0.015
        n -= 60_0000
    }
    if n > 40_0000 {
        bonus += Double(n - 40_0000) * 0.03
        n -= 40_0000
    }
    if n > 20_0000 {
        bonus += Double(n - 20_0000) * 0.05
        n -= 20_0000
    }
    if n > 10_0000 {
        bonus += Double(n - 10_0000) * 0.075
        n -= 10_0000
    }
    bonus += Double(n) * 0.1
    
    return bonus
}

```
我们来分析一下这段代码：

定义函数`calcBonus`，参数是一个定义的变量`n`,`n`类型是`Int`。你会发现n之前有一个`当月利润`，这是函数参数的外部可见参数名称。当你调用着这个参数时`calcBonus(当月利润: <#Int#>)
`他就会显示出来，这样的话就会提示你这个变量到底是什么，所以写一个有意义的外部变量名是很有意义的。有人就会说，他写的形参本来就有意义，在写一个岂不是麻烦,这时你就可以这样写`func calcBonus(var #n:Int) -> Double `,加上一个#号，就会把形参也当作一个外部名称了。

函数参数默认是常量，试图在函数体中更改参数值将会导致编译错误。如果要修改参数，需在其前面加上var关键字，这时参数称为变量参数。例如，上面代码函数中，n便是变量参数。如果将var去掉，n -= *等操作将报错。

`func calcBonus(var 当月利润 n:Int) -> Double `->后边就表示的函数的返回类型，这里是Double。如果没有返回类型就这样写`func calcBonus(var 当月利润 n:Int)`。 `var bonus = 0.0`,Swift会推断bonus是Double类型。`100_0000`你会发现有一个下划线，这里没有影响，只是为了更加方便阅读。

`bonus += Double(n - 100_0000) * 0.01`,因为n是一个Int类型，所以不能与Double进行运算。这里将`n-100_0000`强制转化成Double类型。

##使用switch

```
func calcBonus(var #n:Int) -> Double {
    var bonus = 0.0

    switch n {
    case 1000001..<Int.max:
        bonus += Double(n - 1000000) * 0.01
        n -= 1000000
        fallthrough
    case 600001...1000000:
        bonus += Double(n - 600000) * 0.015
        n -= 600000
        fallthrough
    case 400001...600000:
        bonus += Double(n - 400000) * 0.03
        n -= 400000
        fallthrough
    case 200001...400000:
        bonus += Double(n - 200000) * 0.05
        n -= 200000
        fallthrough
    case 100001...200000:
        bonus += Double(n - 100000) * 0.075
        n -= 100000
        fallthrough
    default:
        bonus += Double(n) * 0.1
    }

    return bonus
}
```

我们来分析一下这段代码：

`1000001..<Int.max`和`600001...1000000`想必大家已经不陌生了，前者代表[1000001,Int.max)，后者代表[600001,1000000]。

大家会感觉到奇怪，和一些别的语言的switch语句补胎一样，case之后没有break。是的，Swift中，switch不用break，但是不用break并不代表着它会执行下边的语句，相反不会。在这段代码中我们却希望它会匹配后边case，那我们加上关键字`default`，就会在执行完一条case后执行下一条。因为Swift的switch具有不贯穿原则，所以这里要使用fallthrough，使其匹配每一个可能的资金区间。fallthrough的作用，是继续向下匹配。

使用数组

如果奖金制度过几天变化了，奖金比例数值调整了，这时候便只能修改程序代码。如果将奖金制度描述为配置数据，这样当业务逻辑更改时，只需要更改配置信息就可以了。以下是修改之后的代码：

```
let bonusRange = [(0.01,1000000)
    ,(0.015,600000)
    ,(0.03,400000)
    ,(0.05,200000)
    ,(0.075,100000)
    ,(0.1,0)
]

func calcBonus(var n:Int) -> Double {
    var bonus = 0.0

    for (rate,limit) in bonusRange {
        if n > limit {
            bonus += Double(n - limit) * rate
            n -= limit
        }
    }

    return bonus
}

```

在这里定义了一个名为bonusRange的数组，数组元素的类型为元组。将各个数值段的奖金比例及临界点写入数组，然使用for循环处理分配逻辑。关于元组，我在[第一篇关于Swift的介绍](http://dowhile.net/2014/12/15/Swiftno1/)中有介绍过。