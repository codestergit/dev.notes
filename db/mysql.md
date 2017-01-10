# mysql

## 事务 ACID
* Atomicity（原子性）
* Consistency（稳定性）
* Isolation（隔离性）
* Durability（可靠性）


## 查询优化
### count max优化
count max字段加索引
### 子查询优化：
### group by 优化

## error 
ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';  
ERROR 1819 (HY000): Your password does not satisfy the current policy requirements  
set global validate_password_policy=0;  

Laravel error  os:centos
```
  [Doctrine\DBAL\Driver\PDOException]
  SQLSTATE[HY000]: General error: 2006 MySQL server has gone away

  [PDOException]
  SQLSTATE[HY000]: General error: 2006 MySQL server has gone away
```
修改`/etc/mysql.cnf`  
```
[mysqld]
wait_timeout=165535
max_allowed_packet = 128M
```