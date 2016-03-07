# PHP

## 重载 overloading
PHP所提供的"重载"（overloading）是指动态地"创建"类属性和方法。我们是通过魔术方法（magic methods）来实现的。  
当调用当前环境下未定义或不可见的类属性或方法时，重载方法会被调用。  

### 属性重载
```
public void __set ( string $name , mixed $value )
public mixed __get ( string $name )
public bool __isset ( string $name )
public void __unset ( string $name )
```
在给不可访问属性赋值时，__set() 会被调用。  
读取不可访问属性的值时，__get() 会被调用。  
当对不可访问属性调用 isset() 或 empty() 时，__isset() 会被调用。  
当对不可访问属性调用 unset() 时，__unset() 会被调用。  

### 方法重载
```
public mixed __call ( string $name , array $arguments )
public static mixed __callStatic ( string $name , array $arguments )
```
在对象中调用一个不可访问方法时，__call() 会被调用。
用静态方式中调用一个不可访问方法时，__callStatic() 会被调用。