# 更改MySQL数据库的编码为utf8mb4

> utf-8编码可能1个字节、2个字节、3个字节、4个字节的字符，但是MySQL的utf8编码只支持最多3字节的数据，也就是说mysql最开始的时候，对utf-8的支持是不完整的。而emoji表情字符是4个字节的字符。

如果直接往采用utf-8编码的数据库中插入表情数据，将看到如下报错：

!> Incorrect string value: ‘\xF0\x9F\x92\x94’ for column ‘name’ at row 1

> 可以对4字节的字符进行编码存储，然后取出来的时候，再进行解码。但是这样做会使得任何使用该字符的地方都要进行编码与解码。
为了支持完整的utf-8编码，mysql推出了utf8mb4，它是mysql平台上utf8编码的超集，兼容utf8，并且能存储4字节的表情字符。
采用utf8mb4编码的好处是：存储与获取数据的时候，不用再考虑表情字符的编码与解码问题。

## 更改数据库的编码为utf8mb4

### 1. MySQL的版本

utf8mb4的最低mysql版本支持版本为5.5.3+，若不是，请升级到较新版本。

### 2. MySQL驱动

5.1.34可用，最低不能低于5.1.13

### 3. 修改MySQL配置文件

!> 如果不清楚MySQL当前使用的配置文件路径，可以尝试这样查看

```
# which mysqld
/usr/local/mysql/bin/mysqld
# /usr/local/mysql/bin/mysqld --verbose --help | grep -A 1 'Default options'
2020-09-20 18:11:35 2427 [Note] Plugin 'FEDERATED' is disabled.
Default options are read from the following files in the given order:
/etc/mysql/my.cnf /etc/my.cnf ~/.my.cnf 
```

修改mysql配置文件my.cnf（windows为my.ini）
my.cnf一般在/etc/mysql/my.cnf位置。找到后请在以下三部分里添加如下内容：

```
[client] 
default-character-set = utf8mb4 
[mysql] 
default-character-set = utf8mb4 
[mysqld] 
character-set-client-handshake = FALSE 
character-set-server = utf8mb4 
collation-server = utf8mb4_unicode_ci 
init_connect=’SET NAMES utf8mb4’
```

### 4. 重启数据库，检查变量
```
SHOW VARIABLES WHERE Variable_name LIKE  'character_set_%'  OR Variable_name LIKE 'collation%';
```

```
+--------------------------+----------------------------------+
| Variable_name            | Value                            |
+--------------------------+----------------------------------+
| character_set_client     | utf8mb4                          |
| character_set_connection | utf8mb4                          |
| character_set_database   | utf8mb4                          |
| character_set_filesystem | binary                           |
| character_set_results    | utf8mb4                          |
| character_set_server     | utf8mb4                          |
| character_set_system     | utf8                             |
| character_sets_dir       | /usr/local/mysql/share/charsets/ |
| collation_connection     | utf8mb4_unicode_ci               |
| collation_database       | utf8mb4_unicode_ci               |
| collation_server         | utf8mb4_unicode_ci               |
+--------------------------+----------------------------------+
```

必须保证下面几个变量必须是utf8mb4

- character_set_client：客户端来源数据使用的字符集
- character_set_connection：连接层字符集
- character_set_database：当前选中数据库的默认字符集
- character_set_results：查询结果字符集
- character_set_server：默认的内部操作字符集

### 5. 数据库连接配置

数据库连接参数中characterEncoding=utf8会被自动识别为utf8mb4，也可以不加这个参数，会自动检测。
而autoReconnect=true是必须加上的。

### 6. 将数据库和已经建好的表也转换成utf8mb4

更改数据库编码：

```
ALTER DATABASE caitu99 CHARACTER SET `utf8mb4` COLLATE `utf8mb4_general_ci`;
```

更改表编码：
```
ALTER TABLE `TABLE_NAME` CONVERT TO CHARACTER SET `utf8mb4` COLLATE `utf8mb4_general_ci`;
```

如有必要，还可以更改列的编码
