## 良好实践

### 验证数据
`filter_var`, `filter_input`
可以验证布尔、整数、浮点数、email、ip、url、正则
```
var_dump(filter_var('bob@example.com', FILTER_VALIDATE_EMAIL));
var_dump(filter_var('http://example.com', FILTER_VALIDATE_URL));
var_dump(filter_var('http://example.com', FILTER_VALIDATE_URL, FILTER_FLAG_PATH_REQUIRED));

//output:
string(15) "bob@example.com"
string(18) "http://example.com"
bool(false)

$isEmail = filter_var('bob@example.com', FILTER_VALIDATE_EMAIL);
if ($isEmail !== false) {
    echo "Success";
} else {
    echo "Fail";
}

$email = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
if (!$email) {
  echo "Invalid email";
}
```

### SQL
不能使用未过滤的输入数据，使用pdo

### 过滤输入
`htmlentities`  不会验证html输入，默认情况下不会转义单引号  
htmlpurifier: http://htmlpurifier.org/


### 转义输出
也是一种防御措施，能避免渲染恶意代码

### 密码
- 绝对不能知道用户的密码  
- 绝对不要约束用户的密码
- 绝对不能通过电子邮件发送用户的密码
密码使用哈希值不使用加密，哈希值是单项算法，加密是双向算法  
哈希算法：MD5、SHA1、bcrypt、scrypt  
bcrype 慢、最安全

### 保证数据库凭证安全
数据库凭证保存在文档根目录意外的文件中，不纳入版本控制中。

### 处理多字节字符串
mb_string替代php的字符串处理，  使用utf-8编码，`default_charset`

### 流
php://stdin, php://stdout, php://stderr  
file_get_contents, fopen, fgets, fwrite  
file://流封装协议，
```
//隐式使用file://流封装协议
$handle = fopen('/etc/hosts', 'rb');

//显示使用file://流封装协议
$handle = fopen('etc/hosts', 'rb');
```
php://流封装协议
- php://stdin 只读，数据来自标准输入
- php://stdout 只写，把数据写入到缓冲区
- php://memory 从内存读入或写入
- php://temp  数据写入临时文件

自定义流封装 streamWrapper
**流上下文**  stream_context_create
**流过滤器**  stream_filter_append
```
$handle = fopen('data.txt', 'rb');
stream_filter_append($handle, 'string.toupper');
while(feof($handle) !== true) {
    echo fgets($handle);  //输出的全是大写
}
fclose($handle);
```

### 错误和异常
Exception，必须抛出Exception类或子类
```
try {
  $pdo = new PDO('...')
} catch(PDOException $e) {
  //处理pdo异常
} catch(Exception $e) {
  //处理其他异常
} finally {
  //始终都执行
}
```
异常处理程序中记录异常，`set_exception_handler`注册异常， `restore_exception_handler`还原成前一个异常处理程序

### 错误
```ini
;显示错误
display_startup_errors = On
display_errors = On
;报告所有错误
error_reporting = -1
;记录错误
log_errors = On
``
全局错误处理程序，`set_error_handler`  
- `$errno`:错误等级（对应于一个E_*常量）
- `$errstr`:错误消息
- `$errfile`:错误文件
- `$errline`:错误行号
- `$errcontext`:数组，错误发生时可用的符号表


## 部署
### PHP-FPM
`emergency_restart_threshold = 10` 在制定的一段时间内，如果失效的PHP-FPM子进程数超过这个值，主进程就重启  
`emergency_restart_interval = 1m`设定上边选项的时间跨度  
引入进程池定义文件
```
// ubuntu
include=/etc/php5/fpm/pool.d/*.conf
// centos
include=/etc/php-fpm.d/*.conf

- `pm.max_children` PHP-FPM进程池最多进程数。获得最大进程数: (可用最大内存)/(每个进程占用内存大小)  
- `pm.start_servers` 预先准备好的进程数，根据实际需求而定。
- `pm.min_spare_servers` 最小进程数
- `pm.min_spare_servers` 最大进程数
- `pm.max_request` 最大HTTP请求数
- `slowlog = /path/to/slowlog.log`,`request_slowlog_timeout = 5s` 记录超过5秒的请求

## 调优
php.ini 工具phpiniscan

### 内存
- 能分配给PHP
- 单个PHP-FPM消耗多少内存
-
