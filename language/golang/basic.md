#  Go基础

## Go程序设计的一些规则

Go之所以会那么简洁，是因为它有一些默认的行为：

大写字母开头的变量是可导出的，也就是其它包可以读取的，是公有变量；小写字母开头的就是不可导出的，是私有变量。
大写字母开头的函数也是一样，相当于class中的带public关键词的公有函数；小写字母开头的就是有private关键词的私有函数。

## 定义变量
```
//定义一个名称为“variableName”，类型为"type"的变量
var variableName type

//定义三个类型都是“type”的变量
var vname1, vname2, vname3 type

//初始化“variableName”的变量为“value”值，类型是“type”
var variableName type = value

//定义三个类型都是int的变量,并且分别初始化为相应的值
var vname1, vname2, vname3 int = 1, 2, 3
//忽略类型声明 Go编译器进行类型推导
var vname1, vname2, vname3 = 1, 2, 3
//跟简单的方法 利用:=
vname1, vname2, vname3 := 1, 2, 3
```
现在是不是看上去非常简洁了？`:=`这个符号直接取代了`var`和`type`,这种形式叫做简短声明。不过它有一个限制，那就是它只能用在函数内部；在函数外部使用则会无法编译通过，所以一般用var方式来定义全局变量
`_`（下划线）是个特殊的变量名，任何赋予它的值都会被丢弃。在这个例子中，我们将值`3`赋予`b`，并同时丢弃`2`：
```
_, b := 2, 3
```
Go对于已声明但未使用的变量会在编译阶段报错，比如下面的代码就会产生一个错误：声明了i但未使用。
对于声明了未使用的变量可以注释掉或者用上边`_`（下划线）变量接收
```
package main

func main() {
    var i int
}
```

## 常量
所谓常量，也就是在程序编译阶段就确定下来的值，而程序在运行时无法改变该值。在Go程序中，常量可定义为数值、布尔值或字符串等类型。

它的语法如下：
```
const constantName = value
//如果需要，也可以明确指定常量的类型：
const Pi float32 = 3.1415926
```
下面是一些常量声明的例子：
```
const Pi = 3.1415926
const i = 10000
const MaxThread = 10
const prefix = "astaxie_"
```
Go 常量和一般程序语言不同的是，可以指定相当多的小数位数(例如200位)， 若指定給float32自动缩短为32bit，指定给float64自动缩短为64bit，详情参考链接

## 数值类型
整数类型有无符号和带符号两种。Go同时支持int和uint，这两种类型的长度相同，但具体长度取决于不同编译器的实现。Go里面也有直接定义好位数的类型：rune, int8, int16, int32, int64和byte, uint8, uint16, uint32, uint64。其中rune是int32的别称，byte是uint8的别称。

> 需要注意的一点是，这些类型的变量之间不允许互相赋值或操作，不然会在编译时引起编译器报错。

> 如下的代码会产生错误：invalid operation: a + b (mismatched types int8 and int32)

> > var a int8

> > var b int32

> > c:=a + b

> 另外，尽管int的长度是32 bit, 但int 与 int32并不可以互用。
浮点数的类型有float32和float64两种（没有float类型），默认是float64。

这就是全部吗？No！Go还支持复数。它的默认类型是complex128（64位实数+64位虚数）。如果需要小一些的，也有complex64(32位实数+32位虚数)。复数的形式为RE + IMi，其中RE是实数部分，IM是虚数部分，而最后的i是虚数单位。下面是一个使用复数的例子：

```
var c complex64 = 5+5i
//output: (5+5i)
fmt.Printf("Value is: %v", c)
```

## 字符串
Go中的字符串都是采用UTF-8字符集编码。字符串是用一对双引号（`""`）或反引号（`\` \``）括起来定义，它的类型是`string`
```
var str string
var emptyString string = ""
func test() {
    hello := "hello"
    yes, no := "yes", "no"
    str = "hello world"
}
```
在Go中字符串是不可变的，代码编译时会报错：cannot assign to，下面的代码可以实现：
```
str := "hello"
str2 := []byte(str) // 将字符串 str 转换为 []byte 类型
str2[0] = "H"
str3 := string(str2) // 再转换回 string 类型
fmt.Printf("%s\n", str3) // output: Hello
```
Go中可以使用+操作符来连接两个字符串
```
str := "Hello"
str2 := str + " World"
fmt.Printf("%s\n", str2)
```
多行的字符在通过`\``来声明
```
str = `hello
        world`
```

## 布尔类型
Go语言中的布 类型与其他语言基本一 ,关键字也为bool,可赋值为 定义的true和false示例代码如下:  
```
var v1 bool
v1 = true
v2 := (1 == 2) // v2     为bool  
```
布类型不能接受其他类型的赋值,不支持自动或强制的类型 换。以下的示例是一些错误 的用法,会导 编译错误:  
```
var b bool
b = 1 //     
b = bool(1) //     
```
以下的用法才是正确的:  
```
var b bool
b = (1!=0) //   正 
fmt.Println("Result:", b) // 打   为Result: true
```

## 错误类型
Go内置有一个error类型，专门用来处理错误信息，Go的package里面还专门有一个包errors来处理错误：
```
err := errors.New("emit macho dwarf: elf header corrupted")
if err != nil {
    fmt.Print(err)
}
```

## 分组声明
同时声明多个常量、变量，或者导入多个包时，可采用分组的方式进行声明。  
例如：
```
import(
    "fmt"
    "errors"
)

const(
    i = 100
    language = "Golang"
)

var(
    i int
    str string
)
```

## iota枚举
Go里面有一个关键字iota，这个关键字用来声明enum的时候采用，它默认开始值是0，const中每增加一行加1：
```
const(
    x = iota  // x == 0
    y = iota  // y == 1
    z = iota  // z == 2
    w  // 常量声明省略值时，默认和之前一个值的字面相同。这里隐式地说w = iota，因此w == 3。其实上面y和z可同样不用"= iota"
)

const v = iota // 每遇到一个const关键字，iota就会重置，此时v == 0

const (
  e, f, g = iota, iota, iota //e=0,f=0,g=0 iota在同一行值相同
)

const （
    a = iota    //a=0
    b = "B"
    c = iota    //c=2
    d,e,f = iota,iota,iota //d=3,e=3,f=3
    g           //g = 4
）
```
> 除非被显式设置为其它值或iota，每个const分组的第一个常量被默认设置为它的0值，第二及后续的常量被默认设置为它前面那个常量的值，如果前面那个常量的值是iota，则它也被设置为iota。

---

## array、slice、map
### array 数组
数组的长度是固定的，不能动态修改
定义数组： 
```
var arr [n]type     // `n`表示数组的长度，`type`表示存储元素的类型
var arr1 [10]int    // 声明了一个int类型的数组
arr[0] = 11      // 赋值操作,数组下标是从0开始的

b := [10]int{1, 2, 3} // 声明了一个长度为10的int数组，其中前三个元素初始化为1、2、3，其它默认为0
c := [10]string{"1", "2", "3"} // 声明了一个长度为10的int数组，其中前三个元素初始化为1、2、3，其它默认为空
d := [...]int{4, 5, 6}   // 可以省略长度而采用`...`的方式，Go会自动根据元素个数来计算长度

// 声明了一个二维数组，该数组以两个数组作为元素，其中每个数组中又有4个int类型的元素
doubleArray := [2][4]int{[4]int{1, 2, 3, 4}, [4]int{5, 6, 7, 8}}

// 上面的声明可以简化，直接忽略内部的类型
easyArray := [2][4]int{{1, 2, 3, 4}, {5, 6, 7, 8}}
```
### slice 切片
在很多应用场景中，数组并不能满足我们的需求。在初始定义数组时，我们并不知道需要多大的数组，因此我们就需要“动态数组”。在Go里面这种数据结构叫slice
`slice`并不是真正意义上的动态数组，而是一个引用类型。`slice`总是指向一个底层`array`，`slice`的声明也可以像`array`一样，**只是不需要长度**。
```
// 和声明array一样，只是少了长度
var s []int 

// 声明并初始化
var slice := []{'a', 'b', 'c', 'd'}
```
slice可以从一个数组或一个已经存在的slice中再次声明。slice通过array[i:j]来获取，其中i是数组的开始位置，j是结束位置，但不包含array[j]，它的长度是j-i。
```
// 声明一个含有10个元素类型为byte的数组
var s = [10]byte {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'}

// 声明两个含有byte的slice
var a, b []byte

// a指向数组的第3个元素开始，并到第五个元素结束，
a = s[2:5]
//现在a含有的元素: s[2]、s[3]和s[4]

// b是数组s的另一个slice
b = s[3:5]
// b的元素是：s[3]s[4]
```
> 注意slice和数组在声明时的区别：声明数组时，方括号内写明了数组的长度或使用`...`自动计算长度，而声明slice时，方括号内没有任何字符。

它们的数据结构如下所示:
![](images/2.2.slice.png?raw=true)
