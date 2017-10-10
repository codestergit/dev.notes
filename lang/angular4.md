# Angular权威教程
## cli命令
```
ng new [name]
ng generate component [name]
ng serve -o 
ng generate component
ng serve --prod --aot
ng build --prod --aot
ng test
// 生成组件
ng generate component ./pages/article -m pages
ng g c ./pages/article -m pages
```
执行`ng serve`, Angular查找angular-cli.json确定入口文件


## 模块
`@NgModule`注解有三个属性:declarations、imports和bootstrap  
`declarations` 指定了在该模块中定义的组件  
`imports` 描述了该模块有哪些依赖  
`bootstrap` 告诉Angular把AppComponent加载为顶层组件

## Angular的工作原理
第一个重要概念:Angular应用是由组件构成的。  
当开发新的Angular应用时，先 出原型图，然后 分成组件。  
每个组件都由三个部分组成:
- 组件注解
- 视图
- 控制器

@Component注解是对组件进行配置的地方  
@Component注解明确了下面两项:  
- selector(选择器)用来告诉Angular要 配哪个HTML元素;  
- template(模板)用来定义视图。  