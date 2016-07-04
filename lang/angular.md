#angular js

## 内部指令(directive)
* ng-app - 该指令启动一个AngularJS应用。
* ng-init - 该指令初始化应用程序数据。
* ng-model - 此指令定义的模型，该模型是变量在AngularJS使用。
* ng-repeat - 该指令将重复集合中的每个项目的HTML元素。
* ng-bind

## scope 
AngularJS启动并生成视图时,会将根ng-app元素同$rootScope进行绑定。$rootScope是所
有$scope对象的最上层  
$scope对象在AngularJS中充当数据模型,但与传统的数据模型不一样,$scope并不负责处 理和操作数据,它只是视图和HTML之间的桥梁,它是视图和控制器之间的胶水。
$scope的所有属性,都可以自动被视图访问到。  
功能:  
* 提供观察者以监视数据模型的变化;
* 可以将数据模型的变化通知给整个应用,甚至是系统外的组件; 
* 可以进行嵌套,隔离业务功能和数据;
* 给表达式提供运算时所需的执行环境

