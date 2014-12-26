title: Swift菜鸟学习第三天
date: 2014-12-21 00:55:32
categories: Swift
tags: ios
---
#排序问题。主要学习：可变参数，元组，快速排序算法，数组的拼接，添加数组元素，异或位操作，swap函数
<!-- more -->
##问题：

三个整数x,y,z，请把这三个数由小到大输出。

###使用if else

```
func sortNumbers(var x:Int,var y:Int,var z:Int)->(x:Int,y:Int,z:Int){
    var empt = 0
    if x > y {
        empt = x
        x = y
        y = empt
    }
    if x > z{
        empt = x
        x = z
        z = empt
    }
    if y > z{
        empt = y
        y = z
        z = empt
    }
    return (x,y,z)
    
}

println(sortNumbers(1, 4, 0))
//(0, 1, 4)
```
上例代码极其简单，使用了可变参数。使用命名元组作为函数的返回类型，此时元组中的命名`x,y,z`与函数内部的`x,y,z`毫无关系。
---
###使用异或位操作符

按位异或运算符^比较两个数，然后返回一个数，这个数的每个位设为1的条件是两个输入数的同一位不同，如果相同就设为0。如下图所示： 

![](http://yangxiaolei.qiniudn.com/bitwiseXOR_2x.png)

任何一个数字，与另外一个数字，进行两次异或操作，都等于其本身。例如：

```
1 ^ 2 ^ 2 == 1
2 ^ 1 ^ 1 == 2

```

借助异或操作符，不使用临时变量，也可以交换两个变量的位置：

```
func sortNumbers(var x:Int,var y:Int,var z:Int)->(x:Int,y:Int,z:Int){
    if x > y{
        x ^= y
        y ^= x
        x ^= y
    }
    if x > z {
        x ^= z
        z ^= x
        x ^= z
    }
    if y > z{
        y ^= z
        z ^= y
        y ^= z
    }
    return (x,y,z)
    
}

println(sortNumbers(1, 4, 0))
//(0, 1, 4)
```
---

###使用swap

使用系统提供的swap函数，代码实现更加简洁：

```
func sortNumbers(var x:Int,var y:Int,var z:Int)->(x:Int,y:Int,z:Int){
    if x > y{
       swap(&x, &y)
    }
    if x > z {
        swap(&x, &z)
    }
    if y > z{
       swap(&y, &z)
    }
    return (x,y,z)
    
}

println(sortNumbers(1, 4, 0))
//(0, 1, 4)

```

`swap`的参数是传入传出参数，所以在调用时使用`&`操作符。
---

###通用的快速排序算法

快速排序法的原理：通过一趟扫描将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

 ```
 func quickSort(nums:[Int]) ->[Int] {
    var a1 = [Int]()
    var a2 = [Int]()
    var a = nums[0]
    
    for var i=0; i<nums.count; ++i {
        if a == nums[i] { continue }
        if nums[i] < a {
            a1.append(nums[i])
        }else{
            a2.append(nums[i])
        }
    }
    
    if a1.count > 1 {
        a1 = quickSort(a1)
    }
    if a2.count > 1 {
        a2 = quickSort(a2)
    }
    
    return a1 + [a] + a2
}
var a = quickSort([1,6,9,0,4,5,7,8,3,4,5])

for i in a{
    print(i)
}
//输出013456789

 ```

 `append`用于向一个数组中添加元素。`+`可直接将数组拼接，`1 + [a] + a2`是将三个数组拼接在一起。向数组推入元素，`append`的替换方法还有更简洁的`+=`，所以这段代码：

 ```
 if nums[i] < a {
    a1.append(nums[i])
}else{
    a2.append(nums[i])
}
 ```

 可以改为：

 ```
 if nums[i] < a {
    a1 += nums[i]
}else{
    a2 += nums[i]
}
 ```

 `+=`可用于向数组推入元素，但分开写却是不成的，比如这样：

```
a1 = a1 + nums[i]

```
Playground便编译不通过了。尼玛有时候`a = a+b`与`a += b`并不是等效的。所以这行代码：

```
return a1 + [a] + a2
```

并不能写成：

```
return a1 + a + a2
```
`quickSort`实现的是一个递归调用，将数组分成两部分，左边永远比右边所有元素小，从2至4至8，递归分组，直至每个组只有一个元素。
