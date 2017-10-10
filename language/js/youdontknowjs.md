# 你不知道的JavaScript

## 作用域和闭包
“在传统编译语言的流程中，程序中的一段源代码在执行之前会经历三个步骤，统称为“编译”
1. 分词/词法分析（Tokenizing/Lexing）
2. 解析/语法分析（Parsing）
3. 代码生成

```
var i=10; 
function a() { 
    alert(i); 
	var i = 2; 
}; 
a(); 
// output: undefined
```

