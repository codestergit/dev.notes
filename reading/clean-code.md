# Clearn Code

## 有意义的命名
### 名副其实
变量、函数、类的命名应该名副其实，不需要注释来说明。一旦发现有更好的名称，就换掉旧的。  

```
// bad
int d //消逝的时间，以日计

// good
int elapsedTimeInDays
```

选择体现本意的名称让人更容易理解和修改代码。
```
// bad
public List<int[]> getThem[] {
  List<int[]> list1 = new ArrayList<int[]>();
  for (int x[]: theList)
    if (x[0] == 4)
      list1.add(x);
  return list1;
}

// good
public List<int[]> getFlaggedCells[] {
  List<int[]> flaggedCells = new ArrayList<int[]>();
  for (int[] cell: gameBoard)
    if (cell[STATUS_VALUE] == FLAGGED)
      flaggedCells.add(cell);
  return flaggedCells;
}

//进一步改进
public List<Cell> getFlaggedCells[] {
  List<Cell> flaggedCells = new ArrayList<Cell>();
  for (Cell cell: gameBoard)
    if (cell.isFlagged())
      flaggedCells.add(cell);
  return flaggedCells;
}
```

避免误导或歧义，避免使用与本义相悖的词。  
避免冗余，废话都是冗余。`variable`不应该出现在变量名中，table不应该出现在表中，name要比nameString要好。  
使用读得出来的名称，恰当的英文单词，不要自造词
```
// bad
class DtaRcrd102 {
    private Date genymdhms;
    private Date modymdhms;
    private final String pszqint = "102";
}

// good
class Customer {
  private Date generationTimestamp;
  private Date modifactionTimestamp;
  private final String recordId = "102";
}
```
使用可搜索的名字，单字母或常用简单名称不易直接搜索到。

类名和对象名应该是名词和名词短语，不应当是动词。如Customer、WikiPage、Account和AddressParser。避免使用Manager、Processor、Data和Info  

方法名应当是动词或动词短语，如postPayment、deletePage和save。属性访问器、修改器和断言应该根据其值命名，并依据Javabean标准加上get、set和is前缀  

每个概念都只对应一个词，且只对应一个，如出现仓库，使用了storage, warehouse, building应该统一为一个

遵循一词一意，避免同一单词用于不同目的，同一术语用于不同概念，也就是别用双关语。  
使用解决方案领域的名称。添加有意义的语境，不要使用没用的语境。

> 取好名字最难的地方在于需要良好的描述技巧和共有文化背景。

## 函数
函数的第一规则是短小，第二规则还是短小。函数的缩进层级不应该多于一层或两层，这样已与阅读和理解。    
做一件事，做好这件事，只做这一件事情。

### 函数的抽象层级
向下规则：自顶向下读代码。每个函数后面跟着位于下一抽象层级的函数。
最理想的参数个数是零，参数尽量不要多于两个，尽量避免三个参数。三个以上可以考虑封装为对象。

分割指令与询问：函数要么做什么事，要么回答什么问题  
使用异常替代返回错误代码。抽离try/catch代码块。  

被重复自己，重复是软件中一切邪恶的根源。许多原则与实践规则都是为消除重复而创建。

### 结构化编程
Edsger Dijkstra的结构化编程规则，每个函数、函数中的代码块都应该有一个入口、一个出口。意味着函数中只有一个return，没有continue和break。不能有goto

## 注释
> 别给糟糕的代码加注释 -- 重新写吧。  

若编程语言有足够的表达力，就不那么需要注释。  
注释不能美化糟糕的代码  
用代码来阐述，代码自解释。
```
if (employee.flags && (employee.age > 65))

if (employee.isEligibleForFullBenefits)
```
### 有些注释是必须的
1. 法律信息   
2. 提供信息注释，对意图的解释，警示  
3. TODO注释，是程序员认为应该做，但由于某种原因没有做的工作列表  
4. API中的phpdoc 、javadoc  

### 坏注释
1. 喃喃自语，可有可无的注释  
2. 多余的注释，如果代码已经表达清楚就没必要写注释
3. 误导性注释、日志式注释。
4. 废话注释，注释太啰嗦。
5. 能用函数或变量名时就别用注释
6. 位置标记，只在特别有价值的时候用
7. 归属与署名，版本控制系统更合适
8. 注释掉的代码


## 格式
代码的可读性很重要 php代码格式参考psr规范
参考团队规范

## 类
单一职责原则（SRP），类或模块应该只有一条加以修改的理由。系统应该由许多短小的类组成，每个小类封装一个权责，只有一个修改的原因，并与少数其他类一起协同达成期望的系统行为。

### 内聚
保持内聚性会得到很多短小的类
为了修改而组织，添加或修改时尽可能少惹麻烦。在理想系统中，通过扩展系统而非修改现有代码来添加新特性。

## 系统
系统的构建和使用分开，启动过程和启动后的运行逻辑分开

### 依赖注入 (Dependency Injection,DI) 控制反转 (Inversion of Control)
依赖注入是分离构造和使用的方法，将第二权责从对象中拿出来，转移到另一个专注一次

## 跌进设计
简单设计原则：
- 运行所有测试
- 重构： 提升内聚性，降低耦合度，切分关注面，模块化系统关注面，缩小函数和类的尺寸，选用更好的名称。消除重复，保证表达力，尽可能减少类和方法的数量
- 不可重复
- 表达力 代码应当清晰地表达作者的意图。编写良好的单元测试也具有表达性，测试的主要目的之一就是通过实例起到文档的作用。


### 什么是整洁代码
代码逻辑应当直截了当，叫缺陷难以隐藏;尽量减少依赖关系，
使之便于维护;依据某种分层战略完善错误处理代码;性能调至最优，省得引诱别人做没规矩的优化，整洁的代码只做好一件事。  

---
  
