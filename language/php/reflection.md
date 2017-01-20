# Reflection 和 Laravel中的使用
PHP提供一套检测class, interface, trait, property, method的两个工具包：Introspection Functions和Reflection API，类似于探针一样的东西来探测这些一等公民。

## Introspection Functions
`class_exists` 判断指定类是否存在  
`interface_exists`检查接口是否存在    
`method_exists`检查类的方法(private,protected,public)是否存在于指定的类对象或类名中，Laravel中很多处用到了这个函数，如Application中的register()检查service provider中register是否存在，和bootProvider()中检查service provider中boot()方法是否存在  
`property_exists`检查该属性(private, protected, public)是否存在于类对象或类名中，Laravel很多地方用到了该函数，如`\Illuminate\Foundation\Auth\RedirectsUsers::redirectPath()`  
`trait_exists`检查trait是否存在   
`class_alias`给指定类取别名，Laravel中只有一处使用了class_alias()，用来给config/app.php中$aliases[ ]注册别名  
`get_class`获取对象的类名，这个函数在Laravel中大量地方在用了，如Application::getProvider($provider)方法，是个很好用的方法获取类的父类名  
`get_parent_class`获取类的父类名  
`get_called_class`获取后期静态绑定类即实际调用类的名称   
`get_class_methods`获取类的方法名组成一个数组(测试只能是public)，Laravel只有一处用到了该方法`\Illuminate\Database\Eloquent\Model::cacheMutatedAttributes() `:line 3397  
`get_class_vars`只会读取类的public属性组成一个数组，类似于get_class_methods()，若属性没有默认值就为null  
`get_object_vars`只会读取对象的public属性组成一个数组，类似于get_class_vars(), get_class_methods()，且属性没有默认值就是null，Laravel中只有一处使用到`\Illuminate\Mail\Jobs\HandleQueuedMessage::__sleep() :line 78`  
`is_subclass_of`判断给定类对象是否是另一给定类名的子类  
`is_a`用来判定给定类对象是否是另一给定类名的对象或是子类，和is_subclass_of()有点类似，只是is_a()还可以判定是不是该类的对象，is_a()类似于instanceof操作符  


## Reflection API
