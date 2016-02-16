# linux
显示一个路径的所有权限
```
namei -om /path/to/check
```

//php执行命令 sudoer配置
修改sudo配置文件，直接键如visudo命令编辑配置文件：

1. 注释Defaults requiretty
Defaults requiretty修改为 #Defaults requiretty， 表示不需要控制终端。
否则会出现sudo: sorry, you must have a tty to run sudo

2. 增加行 Defaults visiblepw
否则会出现 sudo: no tty present and no askpass program specified

3. 赋予apache用户执行svn权限
如，增加行：apache ALL=(ALL) NOPASSWD: /usr/bin/svn
注：NOPASSWD可以使在命令执行时不需要交互输入apache用户的密码 


