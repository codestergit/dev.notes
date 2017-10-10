# 创建模型
```
php artisan make:model Foo
php artisan make:model Foo -m // -m migration

// 指定目录  Laravel 5.2/5.3
php artisan make:model App\\Models\\Foo
```

运行测试用例 (laravel5.4)
```
# 执行一个文件
./vendor/bin/phpunit --filter filepath/className.php
./vendor/bin/phpunit tests/Feature/PaymentTest.php

# 执行一个方法
./vendor/bin/phpunit --filter [methodName] filepath/className.php
./vendor/bin/phpunit --filter testExample tests/Feature/PaymentTest.php
```