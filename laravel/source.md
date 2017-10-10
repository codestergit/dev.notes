
## 服务容器
Laravel 服务容器是管理类依赖和运行依赖注入的有力工具。依赖注入是一个花俏的名词，它实质上是指：类的依赖通过构造器或在某些情况下通过「setter」方法进行「注入」。
### 绑定基础
几乎所有服务容器的绑定都是在 服务提供者 中进行的。

> 但是，如果类没有依赖任何接口，那么就没有必要将类绑定到容器中了。容器绑定时，并不需要指定如何构建这些类，因为容器中会通过 PHP 的反射自动解析对象。

在服务提供者中，你经常可以通过 `$this->app` 属性访问容器。
我们可以通过 bind 方法注册一个绑定，通过传递注册类或接口的名称、及返回该实例的 Closure 作为参数：
```
$this->app->bind('HelpSpot\API', function ($app) {
    return new HelpSpot\API($app->make('HttpClient'));
});
```
注意，我们将获得的容器本身作为参数传递到解析器中，这样就可以使用容器来解决绑定对象对容器的子依赖。  
`singleton`绑定一个单例  
`instance`绑定实例   


## Facades
Facades /fəˈsäd/ 为应用程序的服务容器中可用的类提供了一个「静态」接口。

### Facades 工作原理
在 Laravel 应用中，一个 facade 其实就是一个提供访问容器中对象功能的类。其中最核心的部件就是 `Facade` 类。不管是 Laravel 自带的，还是用户自定义的 Facades，都是继承了 `Illuminate\Support\Facades\Facade` 这个类。

Facade 类利用了 `__callStatic()` 这个魔术方法来延迟调用容器中的对象的方法。
