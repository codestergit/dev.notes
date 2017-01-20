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

ssh-copy-id
ssh-copy-id -i ~/.ssh/id_rsa.pub root@ip


vi编辑是没有权限需要sudo
```
:w !sudo tee %
```

查看文件夹大小
```
du -h
```

## PHP
1、查看服务器php.ini配置文件是哪一个：
```
php -i | grep 'Configuration File'
```
2、查看Linux服务器上运行的是哪一个PHP：
```
which php
```
3、查看系统当前在使用哪一个版本的php.ini及其位置：
```
php --ini
```
