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
