
## 数组函数
`array_filter`用回调函数过滤数组中的单元。如果没有提供 callback 函数，array_filter() 将删除 input 中所有等值为 FALSE 的条目。

```
$array = [
   0 => 'foo',
   1 => false,
   2 => -1,
   3 => null,
   4 => ''
];
print_r(array_filter($array));
// output
Array
(
    [0] => foo
    [2] => -1
)
```

## 类型转换的判别  
PHP 的自动类型转换的一个例子是加号“+”。如果任何一个操作数是浮点数，则所有的操作数都被当成浮点数，结果也是浮点数。否则操作数会被解释为整数，结果也是整数。注意这并没有改变这些操作数本身的类型；改变的仅是这些操作数如何被求值以及表达式本身的类型。
```
$foo = "0";  // $foo 是字符串 (ASCII 48)
$foo += 2;   // $foo 现在是一个整数 (2)
$foo = $foo + 1.3;  // $foo 现在是一个浮点数 (3.3)
$foo = 5 + "10 Little Piggies"; // $foo 是整数 (15)
$foo = 5 + "10 Small Pigs";     // $foo 是整数 (15)

$a    = 'car'; // $a is a string
$a[0] = 'b';   // $a is still a string
echo $a;       // bar

$foo = 10;            // $foo 是一个整数
$str = "$foo";        // $str 是一个字符串
$fst = (string) $foo; // $fst 也是一个字符串
// 输出 "they are the same"
if ($fst === $str) {
    echo "they are the same";
}
```

转换为布尔值
当转换为 boolean 时，以下值被认为是 FALSE：  
- the 布尔值 FALSE 自身
- the 整型值 0 (零)
- the 浮点型值 0.0 (零)
- 空 字符串, 以及 字符串 "0"
- 不包括任何元素的数组
- 不包括任何成员变量的对象（仅PHP 4.0 适用）
- 特殊类型 NULL (包括尚未设定的变量)
- 从没有任何标记（tags）的XML文档生成的SimpleXML 对象

所有其它值都被认为是 TRUE（包括任何资源）。

```
var_dump((bool) "");        // bool(false)
var_dump((bool) 1);         // bool(true)
var_dump((bool) -2);        // bool(true)
var_dump((bool) "foo");     // bool(true)
var_dump((bool) 2.3e5);     // bool(true)
var_dump((bool) array(12)); // bool(true)
var_dump((bool) array());   // bool(false)
var_dump((bool) "false");   // bool(true)
```

### 整型
```
$a = 1234; // 十进制数
$a = -123; // 负数
$a = 0123; // 八进制数 (等于十进制 83)
$a = 0x1A; // 十六进制数 (等于十进制 26)
```
`PHP_INT_SIZE`Integer值的字长
如果给定的一个数超出了 integer 的范围，将会被解释为 float。同样如果执行的运算结果超出了 integer 范围，也会返回 float。
```
$large_number =  2147483647;
var_dump($large_number);
// 输出为：int(2147483647)

$large_number =  2147483648;
var_dump($large_number);
// 输出为：float(2147483648)

// 同样也适用于十六进制表示的整数： 从 2^31 到 2^32-1:
var_dump( 0xffffffff );
// 输出: float(4294967295)

// 不适用于大于 2^32-1　的十六进制表示的数:
var_dump( 0x100000000 );
// 输出: int(2147483647)

$million = 1000000;
$large_number =  50000 * $million;
var_dump($large_number);
// 输出: float(50000000000)
```

### 转换为整型
从布尔值转换: `false` 将产生出 0（零），`true` 将产生出 1（壹）。

从浮点数转换: 当从浮点数转换成整数时，将向零取整。
