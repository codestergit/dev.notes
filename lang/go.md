# Go
##布尔类型
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