# 基本教程

https://www.sjkjc.com/postgresql/explain/



## 查看版本

```sql
SELECT version();

SHOW server_version;
```



# 目录结构

https://blog.csdn.net/sinat_36528886/article/details/135028706

https://blog.csdn.net/weixin_48154829/article/details/134382728

## 安装目录

```
/bin： 该目录通常包含PostgreSQL的可执行文件，如psql（PostgreSQL命令行客户端）和其他实用程序。
	clusterdb：聚簇一个PostgreSQL数据库           
	createdb：创建一个新的PostgreSQL数据库
	createuser：定义一个新的PostgreSQL用户账户
	dropdb：移除一个PostgreSQL数据库
	dropuser：移除一个PostgreSQL用户账户
	ecpg：嵌入式 SQL C 预处理器
	initdb：创建一个新的 PostgreSQL 数据库
	pg_amcheck：在一个或多个PostgreSQL数据库中检查损坏
	pg_archivecleanup： 清理PostgreSQL WAL归档文件
	pg_basebackup：获得一个PostgreSQL集簇的一个基础备份
	pgbench：在PostgreSQL上运行一个基准测试
	pg_checksums
	pg_config：获取已安装的PostgreSQL的信息
	pg_controldata：显示 PostgreSQL 数据库簇控制信息.
	pg_ctl    
	pg_dump：把PostgreSQL数据库抽取为一个脚本文件或其他归档文件
	pg_dumpall:将一个PostgreSQL数据库集簇抽取到一个脚本文件中
	pg_isready:检查一个PostgreSQL服务器的连接状态
	pg_receivewal：以流的方式从一个PostgreSQL服务器得到预写式日志    
	pg_recvlogical：控制 PostgreSQL 逻辑解码流
	pg_resetwal：重置 PostgreSQL 数据库集群的预写日志和其他控制信息
	pg_restore：从一个由pg_dump创建的归档文件恢复一个PostgreSQL数据库
    pg_rewind：
	pg_test_fsync：PostgreSQL判断最快的 wal_sync_method
	pg_test_timing：测量定时开销
	pg_upgrade：升级服务器实例
	pg_verifybackup：验证PostgreSQL集群的基础备份的完整性    
	postgres  
	psql：PostgreSQL的交互式终端
	reindexdb：重索引一个PostgreSQL数据库
	vacuumdb：vacuumdb — 对一个PostgreSQL数据库进行垃圾收集和分析

/data： 这是PostgreSQL存储其数据文件的常见目录，包括主数据库集群。数据目录在PostgreSQL安装过程中指定，并包含诸如base等子目录，其中存储实际的表数据。

/lib： 该目录通常包含PostgreSQL所需的共享库。

/share： 该目录可能包含PostgreSQL使用的与架构无关的文件，例如错误消息、时区信息和其他共享资源。（插件及配置）
	extension存放插件目录

/doc： PostgreSQL的文档文件可能存放在这里。

/include： 编译与PostgreSQL交互的程序所需的头文件
```



## 数据文件目录

```
base/：存储每个数据库的基本数据文件
存储每个数据库的基本数据文件。每个数据库都有一个以其 OID（对象标识符）命名的子目录，里面包含了该数据库的所有表和索引的数据文件。

global/：包含了全局性质的系统表空间文件
包含了全局性质的系统表空间文件。这里存放了所有数据库共享的系统表，如 pg_database、pg_authid 等。

pg_tblspc/：包含了表空间的符号链接
包含了表空间的符号链接。每个符号链接指向实际的表空间目录，表空间是用于组织数据库物理存储的一种方式。

pg_twophase/：包含了两阶段提交中使用的文件
包含了两阶段提交中使用的文件。两阶段提交用于确保分布式事务的一致性。

pg_stat_tmp/：包含了一些临时文件，用于存储统计信息

pg_stat/：包含了 PostgreSQL 收集的统计信息文件
包含了 PostgreSQL 收集的统计信息文件。这些文件记录了数据库服务器运行时的性能统计信息，如查询计划、锁等。

pg_logical/：包含了用于逻辑复制的文件
包含了用于逻辑复制的文件。逻辑复制允许将特定表、特定数据库对象或特定的数据更改复制到另一个数据库。

pg_replslot/：包含了复制插槽信息的文件
包含了复制插槽信息的文件。复制插槽用于流复制中，确保备用节点能够持续接收主节点的 WAL（Write-Ahead Logging）。

pg_subtrans/：包含了用于存储子事务信息的文件
包含了用于存储子事务信息的文件。子事务用于处理并发事务中的多个子操作。

pg_notify/：包含了用于存储异步通知信息的文件。
包含了用于存储异步通知信息的文件。异步通知允许数据库中的一个会话通知其他会话有关特定事件的发生。

pg_snapshots/：包含了用于存储快照信息的文件。
包含了用于存储快照信息的文件。快照是一种数据库的一致性视图，用于支持可重复读事务隔离级别。

pg_serial/：包含了用于存储序列信息的文件
包含了用于存储序列信息的文件。序列是 PostgreSQL 中生成唯一标识符的一种方式。
```



一些重要的配置文件

```
postgresql.conf：存放着 PostgreSQL 服务器的配置参数，如端口号、日志设置等。

pg_hba.conf：存放着 PostgreSQL 的身份验证规则，定义了哪些主机和用户能够连接到数据库，以及使用哪种身份验证方法。

pg_ident.conf：存放着标识映射规则，用于将操作系统用户映射到 PostgreSQL 数据库用户。
```



# 数据类型

```
Primitives:Integer, Numeric,Boolean
基本：整数、数值、布尔值

Structured: Date/Time, Array, Range / Multirange, UUID
结构：日期/时间、数组、范围/多范围、UUID

Document:JSON/JSONB, XML, Key-value (Hstore)
文档：JSON/JSONB、XML、键值 （Hstore）

Geometry:Point, Line, Circle, Polygon
几何图形：点、线、圆、多边形

Customizations:Composite, Custom Types
自定义：复合、自定义类型
```

## 数字类型

```
smallint: 2 字节，范围：-32768 到 32767，默认值：0
	123
	
integer: 4 字节，范围：-2147483648 到 2147483647，默认值：0
	456789
	
bigint: 8 字节，范围：-9223372036854775808 到 9223372036854775807，默认值：0
	123456789012
	
decimal(p,s): 变长，精度 p，规模 s，默认值：0
	12.34 (p=5, s=2)
	
numeric(p,s): 变长，精度 p，规模 s，默认值：0
	12.34 (p=5, s=2)
	
real: 4 字节，范围：1.17549435e-38 到 3.40282347e+38，默认值：0
	3.14159
	
double precision: 8 字节，范围：4.9e-324 到 1.8e+308，默认值：0
	3.14159265359
```

## 字符类型

```
char(n): 固定长度，n 字节，默认值：''（空字符串）
varchar(n): 变长，最大 n 字节，默认值：''（空字符串）；默认长度255
text: 变长，默认值：''（空字符串）
```

## 日期和时间类型

```
date: 4 字节，范围：4713 BCE 到 5874897 CE，默认值：当前日期
	2022-07-25

time: 4 字节，范围：00:00:00 到 23:59:59，默认值：当前时间
	14:30:00

timestamp: 8 字节，范围：4713 BCE 到 5874897 CE，默认值：当前时间戳
	2022-07-25 14:30:00

timestamptz: 8 字节，范围：4713 BCE 到 5874897 CE，默认值：当前时间戳带时区
	2022-07-25 14:30:00+08

interval: 12 字节，范围：-178000000 年到 178000000 年，默认值：0
	1 year 2 months 3 days 4 hours 5 minutes 6 seconds
```

1. **timestamp**:
   - 存储的日期时间数据是不带时区信息的，也就是说它存储的是一个特定的日期和时间，但不指定具体的时区信息。
   - 例如，`'2024-07-17 12:00:00'` 是一个 `timestamp` 类型的数据，表示的是无论在哪个时区，都是这个具体的日期和时间。
2. **timestamptz**:
   - 存储的日期时间数据包含了时区信息，即带有时区的时间戳。
   - 例如，`'2024-07-17 12:00:00+00'` 是一个 `timestamptz` 类型的数据，表示的是在 UTC（协调世界时）时区下的特定日期和时间。这个时间戳会自动转换成其他时区的时间，以确保时间在不同时区下的一致性。

主要区别在于 `timestamptz` 会将存储的时间戳转换成 UTC 时间存储，并在需要时自动转换回所需的时区，而 `timestamp` 则仅存储时间而不考虑时区。





## 布尔类型

```
boolean: 1 字节，true 或 false，默认值：false
```

## 数组类型

```
array: 变长，默认值：空数组
	{1, 2, 3, 4, 5}
```

## JSON 类型

```
json: 变长，默认值：空 JSON 对象
	{"name": "John", "age": 30}

jsonb: 变长，默认值：空 JSON 对象
	{"name": "John", "age": 30}
```

**JSON**

`JSON` 数据类型是在 PostgreSQL 9.2 中引入的。它将 JSON 数据存储为字符串，并提供了一组函数来操作和查询 JSON 数据。

以下是 `JSON` 数据类型的一些特征：

- 将 JSON 数据存储为字符串
- 不支持索引
- 不支持二进制存储
- 支持有限的一组函数来操作和查询 JSON 数据

**JSONB**

`JSONB` 数据类型是在 PostgreSQL 9.4 中引入的。它将 JSON 数据存储在二进制格式中，从而允许更高效的存储和查询。

以下是 `JSONB` 数据类型的一些特征：

- 将 JSON 数据存储在二进制格式中
- 支持索引，从而允许更快的查询
- 支持二进制存储，从而减少存储开销
- 支持更丰富的一组函数来操作和查询 JSON 数据

**关键差异**

- **存储格式**：`JSON` 将 JSON 数据存储为字符串，而 `JSONB` 将其存储在二进制格式中。
- **索引**：`JSONB` 支持索引，从而允许更快的查询，而 `JSON` 不支持。
- **二进制存储**：`JSONB` 支持二进制存储，从而减少存储开销，而 `JSON` 不支持。
- **功能**：`JSONB` 支持更丰富的一组函数来操作和查询 JSON 数据，包括对 JSON 路径查询的支持

**场景**

- 使用 `JSON` 时：
  需要存储少量的 JSON 数据。
  不需要对 JSON 数据进行复杂的查询。
  正在使用较旧版本的 PostgreSQL，不支持 `JSONB`。
- 使用 `JSONB` 时：
  需要存储大量的 JSON 数据。
  需要对 JSON 数据进行复杂的查询。
  想利用索引和二进制存储。



## 其他类型

```
bytea: 变长，默认值：空字节数组
	\x01\x02\x03\x04\x05

uuid: 16 字节，默认值：随机 UUID；使用gen_random_uuid()生成
	12345678-1234-1234-1234-123456789012

xml: 变长，默认值：空 XML 文档
	<person><name>John</name><age>30</age></person>
	
point: 16 字节，默认值：(0,0)
	(1, 2)

line: 32 字节，默认值：((0,0),(0,0))
	((1, 2), (3, 4))

lseg: 32 字节，默认值：((0,0),(0,0))
	((1, 2), (3, 4))

box: 32 字节，默认值：((0,0),(0,0))
	((1, 2), (3, 4))

circle: 24 字节，默认值：((0,0),0)
	((1, 2), 3)

polygon: 变长，默认值：空多边形
	((1, 2), (3, 4), (5, 6), (7, 8))
```





# 约束

```
UNIQUE, NOT NULL 唯一，非空
Primary Keys 主键
Foreign Keys 外键
Exclusion Constraints 排除约束
Explicit Locks, Advisory Locks
显式锁、咨询锁
```



# 连接 PostgreSQL

```sql
psql -h host -p port -d dbname -U  user -W

-h host: 指定数据库服务器的主机名或IP地址。
-p port: 指定连接数据库服务器的端口号。
-d dbname: 指定要连接的数据库名。
-U user: 指定连接数据库所使用的用户名。
-W: 提示输入密码进行连接。

# 简化
psql -d dbname -U  user -W
```



# 身份认证

## 角色

​	PostgreSQL 使用角色的概念管理数据库访问权限。角色是一系列相关权限的集合。为了管理方便，通常把一系列相关的数据库权限赋给一个角色，如果哪个用户需要这些权限，就把角色赋给相应的用户。由于用户也拥有一系列的相关权限，为了简化管理，在 PostgreSQL 中，角色与用户是没有区别的，一个用户也是一个角色，我们可以把一个用户的权限赋给另一个用户

​	用户和角色在整个数据库实例中是全局的，在同一个实例中的不同数据库中，看到的用户都是相同的。在初始化数据库系统时有一个预定义的超级用户，这个用户的名称与初始化该数据库的操作系统用户名相同。如果数据库是建在操作系统用户“postgres”（通常我们把数据库安装在此用户下）下的，那么这个数据库超级用户的名称也叫“postgres”。可以用这个超级用户连接数据库，然后创建出更多的普通用户或其他超级用户。
  在 SQL 标准中，用户和角色之间的区别很清楚，并且用户不会自动继承权限而角色会继承。这种行为在 PostgreSQL 中也可以实现：为要用作 SQL 角色的角色给予 INHERIT 属性，而为要用作 SQL 用户的角色给予 NOINHERIT 属性。不过，为了向后兼容 8.1 以前的发布（在其中用户总是拥有它们所在组的权限），PostgreSQL 默认给所有的角色 INHERIT 属性

### PUBLIC 角色

​	PUBLIC 是 PostgreSQL 数据库中一个特殊的角色组，在元数据表（pg_roles）中都查不到该角色，数据库中所创建的角色都可以理解为是 PUBLIC 角色组成员。而且对 PUBLIC 权限的继承完全不受 NOINHERIT 的控制，一旦创建了一个拥有 login 权限的角色，它会立即继承 PUBLIC 角色组拥有的权限，此时如果想通过 revoke（比如 revoke connect on database）来回收的话不会成功，只能从 PUBLIC 组回收相关权限（比如 revoke connect on database from PUBLIC）

**PUBLIC 默认权限**

- 数据库的 connect，temp/temprary 权限。任何新建的数据库，系统会自动为 PUBLIC 角色赋予connect 和在任何 schema 下创建临时表的权限
- public 模式的 usage，create 权限。在任何新建的数据库的 public 模式下有 usage 和 create 的权限
- 函数的 execute 权限（仅限于 public 模式下）
- 语言和数据类型（包括域）的 usage 权限



### 查看角色权限

```sql
SELECT * FROM pg_roles WHERE rolname = 'rolename';

\dp rolename：显示指定角色的权限，例如 \dp myrole
\z tablename：显示指定表的权限，例如 \z mytable
```



### 列出所有角色

```sql
SELECT rolname FROM pg_roles;
```

### 创建角色

```sql
CREATE ROLE role_name;
```

### 重命名角色

```sql
ALTER ROLE rolename RENAME TO newrolename;
```

### 删除角色

```sql
DROP ROLE role_name;
```

### 创建新的角色并设置密码

```sql
CREATE ROLE rolename WITH PASSWORD 'password';
```

### 创建新的角色并赋予创建数据库的权限

```sql
CREATE ROLE rolename WITH CREATEDB;
```

### 创建新的角色并赋予创建角色权限

```sql
CREATE ROLE rolename WITH CREATEROLE;
```

### 创建新的角色并赋予超级用户权限

```sql
CREATE ROLE rolename WITH SUPERUSER;
```

### 修改角色密码

```sql
ALTER ROLE rolename WITH PASSWORD 'newpassword';
```

### 赋予角色创建数据库的权限

```sql
ALTER ROLE rolename WITH CREATEDB;
```

### 赋予角色创建角色权限

```sql
ALTER ROLE rolename WITH CREATEROLE;
```

### 赋予角色超级用户权限

```sql
ALTER ROLE rolename WITH SUPERUSER;
```

### 赋予角色登录权限

```sql
GRANT LOGIN ON database_name TO role_name;
```





### 授权权限

```sql
GRANT ALL PRIVILEGES ON database_name TO role_name;
```





## 用户

### 角色与用户绑定

PostgreSQL 可以把用户分组在一起，权限可以被授予一整个组或从一整个组回收。一旦组角色存在，可以使用 GRANT 和 REVOKE 命令增加和移除成员

- 一个用户可以是多个组的成员。
- 不允许环状的成员关系。
- 不允许把一个用户授予给 PUBLIC

```sql
GRANT group_role TO role1, ... ;
REVOKE group_role FROM role1, ... ;
```



### 查看用户权限

```sql
SELECT * FROM pg_user WHERE usename = 'username';

\l+：显示当前数据库中的所有用户和他们的权限。
\du username：显示指定用户的权限，例如 \du myuser
```



### 添加用户

```sql
create user iuser with password '123123';
```

### 创建新的用户并赋予创建数据库的权限

```sql
CREATE USER username WITH CREATEDB;
```

### 创建新的用户并赋予创建角色权限

```sql
CREATE USER username WITH CREATEROLE;
```

### 创建新的用户并赋予超级用户权限

```sql
CREATE USER username WITH SUPERUSER;
```



### 赋予用户创建数据库的权限

```sql
ALTER USER username WITH CREATEDB;
```

### 赋予用户创建角色权限

```sql
ALTER USER username WITH CREATEROLE;
```

### 赋予用户超级用户权限

```sql
ALTER USER username WITH SUPERUSER;
```



### 指定用户创建数据库

```sql
create database work_base owner iuser;
```

### 登录work_base数据库

```sql
psql -U postgres -d work_base -p 5432
```

### 授权

```sql
# 授予用户 iuser 在数据库 work_base 中的所有权限，包括创建、删除、修改数据库对象的权限
grant all privileges on database work_base to iuser;

# 授予用户 iuser 在公共模式 (public schema) 中的使用权限，允许用户访问公共模式中的对象
grant usage on schema public to iuser;
 
# 授予用户 iuser 在公共模式 (public schema) 中的所有表上的所有权限，包括 select、insert、update、delete 等权限
grant all privileges on all tables in schema public to iuser;

# 授予用户 iuser 在公共模式 (public schema) 中的所有序列 (sequence) 上的所有权限，包括使用、修改序列的权限
grant all privileges on all sequences in schema public to iuser;

# 授予用户 iuser 在公共模式 (public schema) 中的所有表上的 select、insert、update、delete 权限
grant select,insert,update,delete on all tables in schema public to iuser;

# 授予用户 iuser 在公共模式 (public schema) 中的所有权限，包括创建、删除、修改模式中的对象，使用、修改序列，使用、修改表等权限
grant all on schema public to iuser;
```



PostgreSQL在表级别提供了各种DDL和DML权限：

- SELECT：允许从表中提取数据。
- INSERT：允许向表中添加新行。
- UPDATE：修改表中的现有行。
- DELETE：授予从表中删除行的功能。
- REFERENCES：允许创建外键约束。
- TRIGGER：允许在表上创建触发器。
- TRUNCATE：允许在表上使用TRUNCATE

**授权表**

```sql
# 授予INSERT和UPDATE权限：
Grant insert,update on table tablename to testuser;

# 授予单个表上的所有权限：
Grant all on table tablename to testuser;

授予schema中所有表的所有权限：
Grant all on all tables in schema schemaname to testuser;

```



### 修改用户名

```sql
ALTER USER username RENAME TO newusername;
```



### 修改用户密码

```sql
# ALTER USER username WITH PASSWORD 'new_password';

ALTER USER iuser WITH PASSWORD 'new_password';

# 想使用当前会话的用户名来修改密码
ALTER USER CURRENT_USER WITH PASSWORD 'new_password';

# 也可以使用 psql 命令行工具来修改用户密码
psql -U postgres -c "ALTER USER iuser WITH PASSWORD 'new_password';"
```



### 重置密码

- 找到 PostgreSQL 数据库服务器的配置文件 `pg_hba.conf`

  - Windows：ostgreSQL 安装目录的 `data` 目录下，比如： `C:\Program Files\PostgreSQL\14\data`
  - Linux 上， PostgreSQL 数据库服务器的配置文件位于：/etc/postgresql/14/main/pg_hba.conf

- 修改配置文件之前备份 配置文件，以便进行恢复

  - ```sh
    cp pg_hba.conf pg_hba.conf.bak
    ```

-  将配置文件中的 `scram-sha-256` 或者 `md5` 修改为 `trust`

- ```
  local   all             all                                     peer
  # IPv4 local connections:
  host    all             all             127.0.0.1/32            trust
  # IPv6 local connections:
  host    all             all             ::1/128                 trust
  # Allow replication connections from localhost, by a user with the
  # replication privilege.
  local   replication     all                                     peer
  host    replication     all             127.0.0.1/32            trust
  host    replication     all             ::1/128                 trust
  
  ```

- 重启 PostgreSQL 数据库服务器

  - Windows 中， 可以在服务列表窗口重启 PostgreSQL
  - Linux 中，可以使用 `systemctl restart postgresql` 重启 PostgreSQL

- 登录PostgreSQL

  - ```sql
    psql -U postgres
    ```

- 使用命令修改 `postgres` 用户的密码、

  - ```sql
    ALTER USER postgres WITH PASSWORD 'new_password';
    ```

- 恢复 `pg_hba.conf` 配置文件。 将 `pg_hba.conf.bak` 文件的内容覆盖 `pg_hba.conf`

- 重启 PostgreSQL 数据库服务器。 当登陆时， PostgreSQL 应该会提示输入密码





## 指定IP登录

### 使用 `pg_hba.conf` 文件

`pg_hba.conf` 文件是 PostgreSQL 认证的主要配置文件。可以添加一行到这个文件以限制访问特定 IP 地址或 IP 地址范围。

例如，要允许用户 `myuser` 只从 IP 地址 `192.168.1.100` 登录

```sql
host  mydatabase  myuser  192.168.1.100/32  md5
```

允许用户 `myuser` 只从 localhost 登录

```sql
host  mydatabase  myuser  127.0.0.1/32  md5
```

### 使用SQL命令

允许用户 `myuser` 只从 IP 地址 `192.168.1.100` 登录

```sql
ALTER USER myuser SET CONNECTION LIMIT ADDR '192.168.1.100/32';
```

允许用户 `myuser` 只从 localhost 登录

```sql
ALTER USER myuser SET CONNECTION LIMIT ADDR '127.0.0.1/32';
```

### 使用 `pg_ctl` 命令

允许用户 `myuser` 只从 IP 地址 `192.168.1.100` 登录

 `/32` 是一种指定单个、精确 IP 地址的方式，而不是一个 IP 地址范围

不使用 `/32` 将使 PostgreSQL 允许来自一个更大的 IP 地址范围的连接，而不是单个主机

```sql
pg_ctl -D /path/to/data/directory add-allowed-hosts "myuser 192.168.1.100/32"
```

允许用户 `myuser` 只从 localhost 登录

```sql
pg_ctl -D /path/to/data/directory add-allowed-hosts "myuser 127.0.0.1/32"
```





# psql 下常用命令

## <span id="selectDatabase">列出所有库</span>

```sql
# 要列出当前 PostgreSQL 数据库服务器中的所有数据库
\l
\l+

# 以从 pg_database 表中查询所有的数据库；pg_database 表是 PostgreSQL 内置的一个表，它存储了所有的数据库
SELECT datname FROM pg_database;


# 连接数据库请使用 \c 或者 \connect 命令
# 使用当前用户连接到新的数据库
\c dbname

# 使用新的用户连接到当前数据库
\c - username
```

## 列出所有库中的表

```sql
# 列出当前数据库中的表
\dt
\dt+

# 显示表结构
\d table_name
\d product # 列出product表结构
```

## 列出当前数据库中的可用函数

```sql
\df
```

## 列出可用视图

```sql
\du
```

## 开启查询执行时间

```sql
\timing
```



## 获取 SQL 命令的帮助

```sql
\h sql_command

\h TRUNCATE	# 获取 TRUNCATE帮助
```

## 获取 psql 的帮助

```sql
\?
```

## 退出 psql

```sql
\q
```



# 数据库操作

## 创建数据库

**CREATE DATABASE 语法**

```sql
CREATE DATABASE db_name
[ [ WITH ] [ OWNER [=] user_name ]
       [ TEMPLATE [=] template ]
       [ ENCODING [=] encoding ]
       [ LOCALE [=] locale ]
       [ LC_COLLATE [=] lc_collate ]
       [ LC_CTYPE [=] lc_ctype ]
       [ TABLESPACE [=] tablespace_name ]
       [ ALLOW_CONNECTIONS [=] allowconn ]
       [ CONNECTION LIMIT [=] connlimit ]
       [ IS_TEMPLATE [=] istemplate ] ]
```

```
db_name
要创建的数据库的名字。

user_name
将拥有新数据库的用户的角色名称。您可以使用 DEFAULT 表示执行命令的用户。

template
用于创建新数据库的模板名称。您可以使用 DEFAULT 表示默认模板的模板名称 (template1)。

encoding
要在新数据库中使用的字符集编码。您可以指定一个字符串常量（例如，'SQL_ASCII'），或者一个整数编码号，或者 DEFAULT (模板数据库的编码)。点击这里以查看 PostgreSQL 支持的字符集。默认：UTF8

locale
这是一个设置 LC_COLLATE 和 LC_CTYPE 的快捷方式。如果指定此项，则不能指定其中任何一个参数。

lc_collate
要在新数据库中使用的整理顺序 (LC_COLLATE)。这会影响应用于字符串的排序顺序。默认：C

lc_ctype
要在新数据库中使用的字符分类 (LC_CTYPE)。这会影响字符的分类，例如小写、大写和数字。默认：C

tablespace_name
将与新数据库关联的表空间的名字。您可以使用 DEFAULT 以使用模板数据库的表空间的名称。默认：pg_default

allowconn
是否允许连接到此数据库。如果为 false，则没有人可以连接到该数据库。默认值为 true，允许连接。

connlimit
连接数限制。-1（默认）表示没有限制。

istemplate
是否为模版数据库。 如果为 true，则任何具有 CREATEDB 权限的用户都可以克隆此数据库；如果为 false（默认值），则只有超级用户或数据库所有者可以克隆它
```



```sql
CREATE DATABASE db_name;

# 如果不存在，则创建该数据库；如果已经存在，则不执行任何操作，也不会报错
CREATE DATABASE IF NOT EXISTS dbname;

```



## 删除数据库

**`DROP DATABASE` 语句将永久删除数据库和数据库中的所有表**



```sql
DROP DATABASE [IF EXISTS] database_name;


# cannot drop the currently open database
# 不能删除当前打开的数据库


# ERROR:  database "test_db" is being accessed by other users
# DETAIL:  There is 1 other session using the database.
# 数据库 test_db 正在被其他用户访问
```



**从 `pg_stat_activity` 视图中查询数据库中的活动连接**

```sql
SELECT
  pid,
  usename,
  application_name
FROM
  pg_stat_activity
WHERE
  datname = 'test_db';

```

**使用 `pg_terminate_backend()` 函数结束刚刚返回的活动连接**

```sql
# 37771为上一步命令查出的id
SELECT pg_terminate_backend(37771);
```

## 修改数据库

**`ALTER DATABASE` 可以修改数据库的各种信息，包括名称、属性、所有者、表空间等**

### 重命名一个数据库

```sql
ALTER DATABASE name RENAME TO new_name;

ALTER DATABASE test_db RENAME TO test_new_db;


# current database cannot be renamed
# 不能重命名当前打开的数据库
```

### 修改数据库的所有者

```sql
ALTER DATABASE name OWNER TO
{ new_owner | CURRENT_ROLE | CURRENT_USER | SESSION_USER };

# 数据库 test_new_db 的所有者是 postgres，下面说明了如何要将其所有者修改为 test
# 创建 test 用户
CREATE USER test PASSWORD '123456';

# 将数据库的所有者修改为 test
ALTER DATABASE test_new_db OWNER TO test;
```

### 修改数据库的选项

```sql
ALTER DATABASE name [WITH] ALLOW_CONNECTIONS { true | false};
ALTER DATABASE name [WITH] CONNECTION LIMIT connlimit;
ALTER DATABASE name [WITH] IS_TEMPLATE { true | false};

# ALLOW_CONNECTIONS 是否允许连接到此数据库
# CONNECTION LIMIT 连接数限制
# IS_TEMPLATE 是否为模版数据库

# 修改数据库是否允许连接
ALTER DATABASE test_new_db ALLOW_CONNECTIONS false;
# 修改数据库的连接数
ALTER DATABASE test_new_db CONNECTION LIMIT 10;
# 修改数据库是否为模板数据库
ALTER DATABASE test_new_db IS_TEMPLATE true;
```

### 修改数据库的表空间

```sql
ALTER DATABASE name SET TABLESPACE new_tablespace;

# 创建表空间
CREATE TABLESPACE test_tablespace OWNER postgres LOCATION 'D:\\data\\pg_tablespaces\\test_tablespace';
# 修改数据库的表空间
ALTER DATABASE test_new_db SET TABLESPACE test_tablespace;
```

### 重置数据库的配置参数的值

```sql
ALTER DATABASE name RESET configuration_parameter;
```

### 重置数据库所有的配置参数的值

```sql
ALTER DATABASE name RESET ALL;
```

### 修改数据库的配置参数

```sql
ALTER DATABASE name SET configuration_parameter { TO | = } { value | DEFAULT };
ALTER DATABASE name SET configuration_parameter FROM CURRENT;
```



## 查询数据库

<a href="#selectDatabase">点击此查看</a>

## 复制数据库

### 从模板数据库复制数据库

```sql
# 为了数据的安全性，在操作之前需要先将要操作数据库复制备份
# 使用 CREATE DATABASE 将此数据库复制为一个新数据库
CREATE DATABASE new_db WITH TEMPLATE old_db;
```

`old_db` 必须是模板数据库才能被复制。如果它不是模板数据库，您可以使用 `ALTER DATABASE` 语句[将此数据库修改为模板数据库](https://www.sjkjc.com/postgresql/alter-database/)

```sql
ALTER DATABASE old_db WITH IS_TEMPLATE true;
```

## 备份数据库

### pg_dump

**用于备份单个 PostgreSQL 数据库**

```sql
pg_dump -U username -W -F t db_name > output.tar
```

```
-U username: 指定连接 PostgreSQL 数据库服务器的用户。您可以在 username 位置使用自己的用户名。

-W: 强制 pg_dump 在连接到 PostgreSQL 数据库服务器之前提示输入密码。按回车后， pg_dump 会提示输入 postgres 用户密码。

-F : 指定输出文件的格式，它可以是以下格式之一：
    c: 自定义格式
    d: 目录格式存档
    t: tar 文件包
    p: SQL 脚本文件
    db_name 是要备份的数据库的名字。

output.tar 是输出文件的路径
```



### pg_dumpal

**用于备份 PostgreSQL 服务器中的所有的数据库**

```sql
pg_dumpall -U username > output.sql
```



## 恢复数据库

- `pg_restore` 工具用于恢复由 `pg_dump` 工具产生的 tar 文档和目录文档。
- `psql` 工具可以导入 `pg_dump` 和 `pg_dumpall` 工具产生的 SQL 脚本文件。
- `\i` 命令可以导入 `pg_dump` 和 `pg_dumpall` 工具产生的 SQL 脚本文件



### pg_restore方案

```sql
pg_restore [option...] file_path

pg_restore -d db_name path_to_db_backup_file.tar
```

```
file_path 是要恢复的文件或者目录的路径。
option 是一些恢复数据时用到的参数，比如，数据库，主机，端口 等。 您可以使用如下选项
```

| 参数                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `-a` `--data-only`                                           | 只恢复数据，而不恢复表模式（数据定义）。                     |
| `-c` `--clean`                                               | 创建数据库对象前先清理（删除）它们。                         |
| `-C` `--create`                                              | 在恢复数据库之前先创建它。                                   |
| `-d dbname` `--dbname=dbname`                                | 与数据库 dbname 联接并且直接恢复到该数据库中。               |
| `-e` `--exit-on-error`                                       | 如果在向数据库发送 SQL 命令的时候碰到错误，则退出。缺省是继续执行并且在恢复 结束时显示一个错误计数。 |
| `-f filename` `--file=filename`                              | 声明生成的脚本的输出文件，或者出现-l 选项时用于列表的文件，缺省是标准输出。 |
| `-F format` `--format=format`                                | 声明备份文件的格式。                                         |
| `-i` `--ignore-version`                                      | 忽略数据库版本检查。                                         |
| `-I index` `--index=index`                                   | 只恢复命名的索引。                                           |
| `-l` `--list`                                                | 列出备份的内容。这个操作的输出可以用 -L 选项限制和重排所恢复的项目。 |
| `-L list-file` `--use-list=list-file`                        | 只恢复在 list-file 里面的元素，以它们在文件中出现的顺序。    |
| `-n namespace` `--schema=schema`                             | 只恢复指定名字的模式里面的定义和/或数据。不要和 -s 选项混淆。这个选项可以和 -t 选项一起使用。 |
| `-O` `--no-owner`                                            | 不要输出设置对象的权限，以便与最初的数据库匹配的命令。       |
| `-s` `--schema-only`                                         | 只恢复表结构（数据定义）。不恢复数据，序列值将重置。         |
| `-S username` `--superuser=username`                         | 设置关闭触发器时声明超级用户的用户名。只有在设置了 –disable-triggers 的时候 才有用。 |
| `-t table` `--table=table`                                   | 只恢复表指定的表的定义和/或数据。                            |
| `-T trigger` `--trigger=trigger`                             | 只恢复指定的触发器。                                         |
| `-v` `--verbose`                                             | 声明冗余模式。                                               |
| `-x` `--no-privileges` `--no-acl`                            | 避免 ACL 的恢复（grant/revoke 命令）                         |
| `-X use-set-session-authorization` `--use-set-session-authorization` | 输出 SQL 标准的 SET SESSION AUTHORIZATION 命令，而不是 OWNER TO 命令。 |
| `-X disable-triggers` `--disable-triggers`                   | 这个选项只有在执行仅恢复数据的时候才相关。                   |
| `-h host` `--host=host`                                      | 声明服务器运行的机器的主机名。                               |
| `-p port` `--port=port`                                      | 声明服务器侦听的 TCP 端口或者本地的 Unix 域套接字文件扩展。  |
| `-U username`                                                | 以给出用户身分联接。                                         |
| `-W`                                                         | 强制给出口令提示。如果服务器要求口令认证，那么这个应该自动发生 |

### psql方案

```sql
psql -U username -f path_to_db_backup_file.sql
```



### \i导入sql

```sql
# 启动 psql 工具并连接 PostgreSQL 服务器
.\psql.exe -U postgres

# 创建 sakila 数据库
CREATE DATABASE sakila;

# 连接 sakila 数据库
\c sakila;

# 使用以下两个语句以导入刚刚下载的两个文件 postgres-sakila-schema.sql 和 postgres-sakila-insert-data.sql
\i C:/Users/Adam/Downloads/postgres-sakila-schema.sql
\i C:/Users/Adam/Downloads/postgres-sakila-insert-data.sql

```







# 数据表操作

## 创建表

```sql
CREATE TABLE [IF NOT EXISTS] table_name (
   column_name data_type column_contraint
   [, ...]
   table_constraint
);

```

- `table_name` 是要创建的表的名字。表名应该符合以下规则：
  - 表名可由字母、数字、下划线和美元符号组成，表名最大长度为 63 个字符。
  - 表名在一个数据库中是唯一的。
- `IF NOT EXISTS` 指示只有给定的表不存在的时候才进行创建。它是可选的。 如果你给定一个已经存在的表名，又没有使用 `IF NOT EXISTS` 子句，服务器会返回一个错误。
- `column_name` 是该列的名字。 列名应该符合以下规则：
  - 列名可由字母、数字、下划线和美元符号组成，列名最大长度为 63 个字符。
  - 列名在一个表中是唯一的。
- `data_type` 是该列要存储的数据的数据类型， 比如： [`VARCHAR`](https://www.sjkjc.com/postgresql/strings-types/), [`INTEGER`](https://www.sjkjc.com/postgresql/integer-type/), [`BOOLEAN`](https://www.sjkjc.com/postgresql/boolean-type/), [`DATE`](https://www.sjkjc.com/postgresql/date-type/), [`TIME`](https://www.sjkjc.com/postgresql/time-type/), [`TIMESTAMP`](https://www.sjkjc.com/postgresql/timestamp-type/), [`ARRAY`](https://www.sjkjc.com/postgresql/array-type/), [`JSON`](https://www.sjkjc.com/postgresql/json-type/) 等。
- `column_contraint` 是该列的约束，比如:
  - [`PRIMARY KEY`](https://www.sjkjc.com/postgresql/primary-key/)
  - [`FOREIGN KEY`](https://www.sjkjc.com/postgresql/foreign-key/)
  - [`NOT NULL`](https://www.sjkjc.com/postgresql/not-null/)
  - [`UNIQUE`](https://www.sjkjc.com/postgresql/unique/)
  - [`CHECK`](https://www.sjkjc.com/postgresql/check-constraint/)
  - [生成列](https://www.sjkjc.com/postgresql/generated-columns/)
  - [标识列](https://www.sjkjc.com/postgresql/identity-columns/)
- `column_name data_type column_contraint` 为一个列的定义。您可以在表中定义多个列，多个列定义使用逗号分隔。
- `table_constraint` 是表上的约束，包括：[`PRIMARY KEY`](https://www.sjkjc.com/postgresql/primary-key/), [`FOREIGN KEY`](https://www.sjkjc.com/postgresql/foreign-key/), [`UNIQUE`](https://www.sjkjc.com/postgresql/unique/) 和 [`CHECK`](https://www.sjkjc.com/postgresql/check-constraint/)
- `;` 不是语句的一部分，它只是表示语句的结束

```sql
CREATE TABLE users (
  user_id INTEGER NOT NULL PRIMARY KEY,
  name VARCHAR(45) NOT NULL,	# 最多为 45 个字符；如果超出45个字符，则会把超出部分截断
  age INTEGER,
  locked BOOLEAN NOT NULL DEFAULT false,
  created_at TIMESTAMP NOT NULL
);

# 如果varchar和INTEGER没有设置NOT NULL；并且也没有插入值，那么字符串会默认为空串，数字类型是NULL
```

```sql
CREATE TABLE user_hobbies (
  hobby_id SERIAL NOT NULL,
  user_id INTEGER NOT NULL,
  hobby VARCHAR(45) NOT NULL,
  created_at TIMESTAMP NOT NULL,
  PRIMARY KEY (hobby_id),
  CONSTRAINT fk_user
    FOREIGN KEY (user_id)
    REFERENCES users (user_id)
    ON DELETE CASCADE
    ON UPDATE RESTRICT);
```

- `hobby_id` 列的数据类型是 `INTEGER`。它不能为 `NULL`，并且它是一个自增序列。
- `user_id` 列的数据类型是 `INTEGER`。它不能为 `NULL`。它通过外键指向了 `users` 表的 `user_id` 列。
- `hobby` 列的数据类型是 `VARCHAR`，它最多为 45 个字符。 它不能为 `NULL`。
- `created_at` 列的数据类型是 `TIMESTAMP`。它不能为 `NULL`。

`user_hobbies` 表的约束有：

- `PRIMARY KEY (hobby_id)` 子句表明 `hobby_id` 列是主键。
- `CONSTRAINT fk_user` 定义了一个[外键约束](https://www.sjkjc.com/postgresql/foreign-key/)。这个外键将 `user_id` 列引用了 `users` 表的 `user_id` 列
- `ON DELETE CASCADE` `user_id` 关联的行被删除时，该外键约束指定了级联删除的动作。这意味着如果 `users` 表中的某个用户被删除，所有关联到该用户的 `user_hobbies` 行也会被删除
- `ON UPDATE RESTRICT` `user_id` 关联的行不允许更新。换句话说，如果 `users` 表中的某个用户的 `user_id` 被更新，`user_hobbies` 表中相关的行不允许自动更新，除非手动调整



## 从已有的表创建新表

```sql
CREATE TABLE [IF NOT EXISTS] table_name
AS TABLE existing_table_name
[WITH NO DATA];

```



- `table_name` 是要创建的表的名字。
- `existing_table_name` 是已存在的表的名字。
- `WITH NO DATA` 指示只创建表而不拷贝数据。它是可选的。如果省略它，则即创建表又拷贝原表中的数据



```sql
CREATE TABLE users_copy
AS TABLE users;

```



## 从结果集创建新表

```sql
CREATE TABLE [IF NOT EXISTS] table_name
AS
SELECT ...;

```

```sql
CREATE TABLE users_copy
AS
SELECT * FROM users;


# 创建 users_copy 表， 不拷贝 users 表中的数据行
CREATE TABLE users_copy
AS
SELECT * FROM users WHERE false;

```

## 删除表

```sql
DROP TABLE [ IF EXISTS ] table_name [, ...]
[ CASCADE | RESTRICT ];

```

- `table_name` 是要删除的表的名称。
- 您可以在一个 `DROP TABLE` 语句中删除多个表，请使用逗号分隔表名。
- `IF EXISTS` 选项是可选的，它可以避免由于输入的表名 `table_name` 不存在引发的错误。
- `CASCADE | RESTRICT` 是可选的，它指示了如果有其他对象（比如[外键](https://www.sjkjc.com/postgresql/foreign-key/)、视图、触发器、存储过程等）引用了要删除的表的处理策略。其中：
  - `CASCADE` - 允许删除指定的表和引用此表的对象。
  - `RESTRICT` - 如果有对象引用此表，拒绝删除此表，并给出错误。它是默认的选项

```sql
# 强制删除此表，使用 CASCADE
DROP TABLE users;

# users 表被删除了，并且 user_hobbies 表上的外键约束 fk_user 也被级联删除了
DROP TABLE users CASCADE;

# 先判断在删除
DROP TABLE IF EXISTS x;
```



## 修改表

```sql
ALTER TABLE [IF EXISTS] table_name
   [alter_action options]
   [, ...];

```

`table_name` 是要修改的表的名字。 `IF EXISTS` 是可选的，

其中 `alter_action` 是一个修改动作，主要包括以下关键字：

- `ADD` 关键字可用来添加列和约束。
- `DROP` 关键字可用来删除列和约束。
- `ALTER` 关键字可用来修改现有的列和约束。
- `RENAME` 关键字可用来重命名表、列、和约束。
- `SET` 关键字可用来修改表的架构、表空间。
- `ENABLE` 关键字可用来启用触发器、规则、和行安全策略。
- `DISABLE` 关键字可用来禁用触发器、规则、和行安全策略。



### 重命名表

```sql
ALTER TABLE table_name
  RENAME TO new_name

```

### 修改表架构

```sql
ALTER TABLE table_name
  SET SCHEMA new_schema
```

### 修改表空间

```sql
ALTER TABLE table_name
  SET TABLESPACE new_tablespace
```

### 添加列

https://www.sjkjc.com/postgresql/alter-column/

```sql
ALTER TABLE table_name
  ADD [COLUMN] [IF NOT EXISTS] column_name data_type [ column_constraint [ ... ] ]
```

### 删除列

```sql
ALTER TABLE table_name
  DROP [ COLUMN ] [ IF EXISTS ] column_name [ RESTRICT | CASCADE ]
```

### 重命名列

```sql
ALTER TABLE table_name
  RENAME [ COLUMN ] column_name TO new_column_name
```

### 修改列类型

```sql
ALTER TABLE table_name
  ALTER [ COLUMN ] column_name [ SET DATA ] TYPE data_type

```

### 列设置默认值

```sql
ALTER TABLE table_name
  ALTER [ COLUMN ] column_name SET DEFAULT expression
```

### 删除列默认值

```sql
ALTER TABLE table_name
  ALTER [ COLUMN ] column_name DROP DEFAULT

```

### 列添加 `NOT NULL`

```sql
ALTER TABLE table_name
  ALTER [ COLUMN ] column_name SET NOT NULL
```

### 删除列 `NOT NULL`

```sql
ALTER TABLE table_name
  ALTER [ COLUMN ] column_name DROP NOT NULL
```



### 标识列

```sql
ALTER TABLE table_name
  ALTER [ COLUMN ] column_name ADD GENERATED { ALWAYS | BY DEFAULT }
      AS IDENTITY [ ( sequence_options ) ]
```

### 修改为普通列

```sql
ALTER TABLE table_name
  ALTER [ COLUMN ] column_name DROP IDENTITY [ IF EXISTS ]
```

### 添加约束

```sql
ALTER TABLE table_name
  ADD [ CONSTRAINT constraint_name ]
      { CHECK ( expression ) [ NO INHERIT ] |
        UNIQUE ( column_name [, ... ] ) index_parameters |
        PRIMARY KEY ( column_name [, ... ] ) index_parameters |
        EXCLUDE [ USING index_method ] ( exclude_element WITH operator [, ... ] ) index_parameters [ WHERE ( predicate ) ] |
        FOREIGN KEY ( column_name [, ... ] ) REFERENCES reftable [ ( refcolumn [, ... ] ) ]
          [ MATCH FULL | MATCH PARTIAL | MATCH SIMPLE ] [ ON DELETE referential_action ] [ ON UPDATE referential_action ] }
      [ DEFERRABLE | NOT DEFERRABLE ] [ INITIALLY DEFERRED | INITIALLY IMMEDIATE ]

```

### 删除约束

```sql
ALTER TABLE table_name
  DROP CONSTRAINT [ IF EXISTS ]  constraint_name [ RESTRICT | CASCADE ]

```

### 重命名约束

```sql
ALTER TABLE table_name
  RENAME CONSTRAINT constraint_name TO new_constraint_name

```





# 数据列操作案例

## 添加列

将新列添加到现有表

```sql
ALTER TABLE table_name
ADD [COLUMN] [IF NOT EXISTS] column_name data_type column_contraint
[, ADD [COLUMN] ...];

```

- `table_name` 是要在其中添加列的表。
- `ADD [COLUMN] ...` 子句用来添加一个列。其中 `COLUMN` 关键字是可以省略的。如果要在一个语句中添加多个列，请使用多个逗号分隔的 `ADD [COLUMN] ...` 子句。
- `column_name` 是要添加的列的名字。 列名应该符合以下规则：
  - 列名可由字母、数字、下划线和美元符号组成，列名最大长度为 63 个字符。
  - 列名在一个表中是唯一的。
- `data_type` 是要添加的列要存储的数据的数据类型， 比如： [`VARCHAR`](https://www.sjkjc.com/postgresql/strings-types/), [`INTEGER`](https://www.sjkjc.com/postgresql/integer-type/), [`BOOLEAN`](https://www.sjkjc.com/postgresql/boolean-type/), [`DATE`](https://www.sjkjc.com/postgresql/date-type/), [`TIME`](https://www.sjkjc.com/postgresql/time-type/), [`TIMESTAMP`](https://www.sjkjc.com/postgresql/timestamp-type/), [`ARRAY`](https://www.sjkjc.com/postgresql/array-type/), [`JSON`](https://www.sjkjc.com/postgresql/json-type/) 等。
- `column_contraint` 是要添加的列的约束，比如 [`NOT NULL`](https://www.sjkjc.com/postgresql/not-null/), [`UNIQUE`](https://www.sjkjc.com/postgresql/unique/), [`PRIMARY KEY`](https://www.sjkjc.com/postgresql/primary-key/), [`FOREIGN KEY`](https://www.sjkjc.com/postgresql/foreign-key/) 和 [`CHECK`](https://www.sjkjc.com/postgresql/check-constraint/) 等。
- `IF NOT EXISTS` 可以避免因为给出的重复的列名而导致的错误。它是可选的。

新的列将会被添加到表的末尾。您不能为新的列指定位置。

如果表中已有一些行，新的列的约束可能会导致错误，您可以在列定义上添加默认值，或者通过以下步骤解决：

1. 添加不带约束的列。
2. 更新新加的列的数据。
3. 为新的列添加约束。



```sql
INSERT INTO users (name) values ('Tim');
```

```sql
# 创建库
CREATE DATABASE testdb;

# 切换库
\c testdb;

# \d 命令查看此表中的所有列
\d users;

# 创建表
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);


# 在 users 表保存用户的年龄，你需要使用以下语句向 users 表中添加 age 列
ALTER TABLE users ADD COLUMN age INTEGER NOT NULL;

ERROR:  column "age" contains null values
# 因为表不是一个空表，它已经有了一行。 要添加的 age 列是 NOT NULL 的 导致了这个错误的发生。要避免这个错误，可以为 age 列指定一个默认值

ALTER TABLE users ADD COLUMN age INTEGER NOT NULL DEFAULT 18;




# 向 users 表中添加 email 和 cellphone 列
ALTER TABLE users
ADD COLUMN email VARCHAR(100),
ADD COLUMN cellphone VARCHAR(100);
```





## 查看表中所有的列

```sql
\d table_name


# 从 information_schema.columns 表中查找一个表中所有的列
SELECT column_name
FROM information_schema.columns
WHERE table_schema = 'public'
  AND table_name = 'table_name';
```



## 删除列

```sql
ALTER TABLE table_name
DROP [COLUMN] [IF EXISTS] column_name [RESTRICT | CASCADE]
[, DROP [COLUMN] ...];

```

- `table_name` 是要在其中添加列的表。
- `DROP [COLUMN] ...` 子句用来删除一个列。其中 `COLUMN` 关键字是可以省略的。如果要在一个语句中删除多个列，请使用多个逗号分隔的 `ADD [COLUMN] ...` 子句。
- `IF EXISTS` 是可选的， 它可以避免因为给出的列名不存在而导致的错误。
- `column_name` 是要删除的列的名字。
- `CASCADE | RESTRICT` 是可选的， 它指示了如果有其他对象（比如[外键](https://www.sjkjc.com/postgresql/foreign-key/)、视图、触发器、存储过程等）引用了要删除的列的处理策略。其中：
  - `CASCADE` - 允许删除此列和引用此列的对象。
  - `RESTRICT` - 如果有对象引用此列，拒绝删除此列，并给出错误。它是默认的选项。

当您从表中删除一列时，PostgreSQL 将自动删除所有涉及删除列的[索引](https://www.sjkjc.com/postgresql/indexes/)和约束。



**有以下两表**

```sql
CREATE TABLE users (
  user_id INTEGER NOT NULL PRIMARY KEY,
  name VARCHAR(45) NOT NULL,
  age INTEGER,
  locked BOOLEAN NOT NULL DEFAULT false,
  created_at TIMESTAMP NOT NULL
);

CREATE TABLE user_hobbies (
  hobby_id SERIAL NOT NULL,
  user_id INTEGER NOT NULL,
  hobby VARCHAR(45) NOT NULL,
  created_at TIMESTAMP NOT NULL,
  PRIMARY KEY (hobby_id),
  CONSTRAINT fk_user
    FOREIGN KEY (user_id)
    REFERENCES users (user_id)
    ON DELETE CASCADE
    ON UPDATE RESTRICT);
```

```sql
# 删除 users 表中的 user_id 列
ALTER TABLE users DROP COLUMN user_id;

# ERROR:  cannot drop column user_id of table users because other objects depend on it
# DETAIL:  constraint fk_user on table user_hobbies depends on column user_id of table users
# HINT:  Use DROP ... CASCADE to drop the dependent objects too.
# user_hobbies 表中的外键 fk_user 引用了 users 表中的 user_id 列，不能删除此列， PostgreSQL 给出一个错误提示

# 要强制删除此列，使用 CASCADE 选项
# user_id 列被删除了，并且 user_hobbies 表上的外键约束 fk_user 也被级联删除了
ALTER TABLE users DROP COLUMN user_id CASCADE;

```



## 修改列

```sql
ALTER TABLE table_name
ALTER [COLUMN] column_name alter_action
[, ALTER [COLUMN] ...];

```

- `table_name` 是要在其中添加列的表。
- `ALTER [COLUMN] column_name alter_action` 子句用来修改由列名 `column_name` 指定的列。其中 `COLUMN` 关键字是可以省略的。
- `alter_action` 是修改动作，您可以使用以下动作之一：
  - 修改列的数据类型: `[ SET DATA ] TYPE data_type [ COLLATE collation ] [ USING expression ]`
  - 修改列的默认值：`SET DEFAULT expression`
  - 删除列的默认值：`DROP DEFAULT`
  - 设置或删除不能为 NULL: `{ SET | DROP } NOT NULL`
  - 将生成列转为普通列: `DROP EXPRESSION [ IF EXISTS ]`
  - 修改列为标识列: `ADD GENERATED { ALWAYS | BY DEFAULT } AS IDENTITY [ ( sequence_options ) ]`
  - 修改标识列的生成策略: `{ SET GENERATED { ALWAYS | BY DEFAULT } | SET sequence_option | RESTART [ [ WITH ] restart ] } [...]`
  - 将标识列转为普通列: `DROP IDENTITY [ IF EXISTS ]`
  - 设置列的统计信息手机目标: `SET STATISTICS integer`
  - 设置属性选项: `SET ( attribute_option = value [, ... ] )`
  - 重置属性: `RESET ( attribute_option [, ... ] )`
  - 设置列的存储模式: `SET STORAGE { PLAIN | EXTERNAL | EXTENDED | MAIN }`
  - 设置列的压缩方法: `SET COMPRESSION compression_method`





### 修改列类型

```sql
ALTER TABLE table_name
  ALTER [ COLUMN ] column_name [ SET DATA ] TYPE data_type [ USING expression ]

```

- 在 `ALTER TABLE` 关键字后指定要更改的列的表名。
- 在 `ALTER COLUMN` 子句后指定要更改数据类型的列的名称。
- 为 `TYPE` 关键字后的列提供新的数据类型。该 `SET DATA TYPE` 和 `TYPE` 是等价的。
- PostgreSQL 允许您通过添加 `USING` 子句在修改数据类型时将列的值转换为新的值。



```sql
# 创建表
CREATE TABLE orders (
    id serial PRIMARY KEY,
    order_no VARCHAR NOT NULL
);

# 插入数据
INSERT INTO orders(order_no)
VALUES('10001'), ('10002');

# 将 order_no 列的数据类型更改为 INT
ALTER TABLE orders ALTER COLUMN order_no TYPE INT;


# ERROR:  column "order_no" cannot be cast automatically to type integer
# HINT:  You might need to specify "USING order_no::integer".

ALTER TABLE orders ALTER COLUMN order_no TYPE INT USING order_no::integer;

```





# 数据操作

## 新增数据

```sql
INSERT INTO table_name(column1, column2, …)
VALUES
  (value11, value12, …) [, (value21, value22, …), ...]
[ON CONFLICT conflict_target conflict_action]
[RETURNING expr];

```

- `INSERT INTO` 和 `VALUES` 是关键字
- `table_name` 是要插入数据行的表名。
- `(column1, column2, …)` 是列列表，其中是通过逗号分隔的各个列。
- `(value11, value12, …)` 是值列表，其中是通过逗号分隔的各个列的值。值列表中的值于列列表中的列一一对应。
- 要一次插入多个数据行，请使用多个使用逗号分隔的值列表。
- `ON CONFLICT` 用来[在 PostgreSQL 中实现 upsert 操作](https://www.sjkjc.com/postgresql/insert-on-conflict/)。
- `RETURNING` 子句是可选的。它用于返回插入的行的信息。 `expr` 可以是列名，或表达式等。



### RETURNING 子句

`INSERT` 语句有一个可选 `RETURNING` 子句，用于返回插入行的信息。如果具有 `RETURNING` 子句时，`INSERT` 语句按照 `RETURNING` 子句返回，否则它返回成功插入的行



返回指定的列，使用列表。多个列使用逗号分隔

```sql
RETURNING column1
RETURNING column1, column2

```

还可以使用 `AS` 对列名指定别名

```sql
RETURNING column1 AS column1_new_1
RETURNING column1 AS column1_new_1, column2 AS column1_new_2
```

返回新行的所有的列，使用星号 (`*`)

```sql
RETURNING *
```

返回一个表达式计算的值

```sql
RETURNING expr
```



### 不带 `RETURNING` 子句的返回值

没有指定 `RETURNING` 子句的 `INSERT` 语句的返回值具有以下形式

```sql
INSERT oid count
```

- `oid` 是一个对象标识符。PostgreSQL 在内部将 `oid` 用作其系统表的[主键](https://www.sjkjc.com/postgresql/primary-key/)。通常， `INSERT` 语句返回 `oid` 值为 0。
- `count` 是 `INSERT` 语句成功插入的行数。





### 案例

```sql
# 创建表
DROP TABLE IF EXISTS student;
CREATE TABLE student (
  id SERIAL PRIMARY KEY,
  name VARCHAR(50) NOT NULL,
  gender CHAR(1) NOT NULL,
  birthday DATE,
  notes VARCHAR(255)
);


# 插入一条数据
INSERT INTO student(name, gender) VALUES ('Tom', 'M');

# 向表中插入单行并指定返回值
INSERT INTO student(name, gender) VALUES ('Lucy', 'F') RETURNING *;

# 由于 INSERT 语句带有 RETURNING * 子句，因此语句返回了插入的新行中的所有列。如果只想返回其中的一列或者几列，在 RETURNING 子句指定具体的列
INSERT INTO student(name, gender) VALUES ('Jack', 'M') RETURNING id AS "Student ID", name, gender;


# 向表中插入多行
INSERT INTO student(name, gender) VALUES ('Jim', 'M'), ('Kobe', 'M'), ('Linda', 'F') RETURNING *;

# 向 student 表中插入一行带有生日的数据
INSERT INTO student (name, gender, birthday) VALUES('Alice', 'F', '2012-04-21') RETURNING *;


```



### `INSERT ON CONFLICT`插入或更新

```sql
INSERT INTO table_name(column_list)
VALUES(value_list)
ON CONFLICT conflict_target conflict_action
[RETURNING {* | column_names}];;

```

比较于 `INSERT` 语句来说，`INSERT ON CONFLICT` 只是多了 `ON CONFLICT` 子句。

这里：

- `conflict_target` 是存在冲突的对象，它可以是以下之一：
  - 一个列名。该列必须是主键或者唯一索引。
  - `ON CONSTRAINT constraint_name`， 并且 `constraint_name` 必须是[唯一约束](https://www.sjkjc.com/postgresql/unique/) 的名称。
  - [`WHERE`](https://www.sjkjc.com/postgresql/where/) 子句。
- `conflict_action` 是存在冲突时要采取的动作，它可以是以下之一：
  - `DO NOTHING`: 如果存在冲突，不采取任何动作。
  - `DO UPDATE`: 如果存在冲突，使用 `DO UPDATE SET column_1 = value_1, .. WHERE condition` 更新表中的字段。



### 案例

```sql
# 建表
DROP TABLE IF EXISTS users;
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  nickname VARCHAR(50) NOT NULL,
  login_name VARCHAR(50) UNIQUE,
  notes VARCHAR(255)
);

# 插入数据
INSERT INTO
    users (nickname, login_name, notes)
VALUES
    ('Tim', 'tim', 'This is Tim'),
    ('Tom', 'tom', 'This is Tom');

# 再插入一个新行，其中带有和已有行重复的 login_name
INSERT INTO
    users (nickname, login_name, notes)
VALUES
    ('Tim2', 'tim', 'This is Tim2');


# ERROR:  duplicate key value violates unique constraint "users_login_name_key"
# DETAIL:  Key (login_name)=(tim) already exists.
# 重复的键值违反了唯一约束“ users _ login _ name _ key”
# 密钥(login _ name) = (tim)已经存在


# 使用 DO NOTHING 选项，如果冲突就不操作
INSERT INTO
    users (nickname, login_name, notes)
VALUES
    ('Tim2', 'tim', 'This is Tim2')
ON CONFLICT (login_name) DO NOTHING;


# 使用 DO UPDATE 更新其他的字段
INSERT INTO
    users (nickname, login_name, notes)
VALUES
    ('Tim2', 'tim', 'This is Tim2')
ON CONFLICT (login_name)
    DO UPDATE SET nickname = 'Tim2', notes = 'This is Tim2'
RETURNING *;


# 在 DO UPDATE 子句中，还可以使用 EXCLUDED 对象引用引发冲突的数据
INSERT INTO
    users (nickname, login_name, notes)
VALUES
    ('Tim2', 'tim', 'This is Tim2')
ON CONFLICT (login_name)
    DO UPDATE SET nickname = EXCLUDED.nickname,
                  notes = EXCLUDED.notes
RETURNING *;



# 在冲突对象中，除了字段名称，您还可以使用约束名称。上面的语句可以使用约束名称 users_login_name_key 代替列名 login_name
INSERT INTO
    users (nickname, login_name, notes)
VALUES
    ('Tim3', 'tim', 'This is Tim3')
ON CONFLICT ON CONSTRAINT users_login_name_key
    DO UPDATE SET nickname = EXCLUDED.nickname,
                  notes = EXCLUDED.notes
RETURNING *;

```



## 删除数据

```sql
DELETE FROM table_name
[where_clause]
[RETURNING expr];

```

- 在 `DELETE FROM` 关键字后的 `table_name` 是要从中删除数据的表的名称。

- `where_clause` 是 [`WHERE`](https://www.sjkjc.com/postgresql/where/) 子句。 您可以在其中使用条件来指定要删除表中的哪些行。

- `WHERE` 子句是可选的。如果不指定 `WHERE` 子句，表中的所有行将被删除。

- `RETURNING` 子句是可选的。它用于返回删除的行的信息。

  `expr` 可以是列名或者表达式，多个列或者表达式请使用逗号分隔。 您还可以使用 `*` 表示表中的所有的列。

  如果不指定 `RETURNING` 子句， `DELETE` 语句将返回删除的行数。

如果您要更加高效率的清空一个表，请优先使用 [`TRUNCATE TABLE`](https://www.sjkjc.com/postgresql/truncate-table/) 语句



```sql
# 建表
CREATE TABLE film_copy AS SELECT * FROM film;

# 中删除 film_id 为 1 的 1 个影片
DELETE FROM film_copy
WHERE film_id = 1;


# 从 film_copy 表中删除 film_id 为 2, 3 或者 4 的 3 个影片
DELETE FROM film_copy
WHERE film_id in (2, 3, 4);

# 从 film_copy 表中删除所有的影片
DELETE FROM film_copy;
```

### PostgreSQL DELETE 删除并返回删除的行

```sql
# 从 film_copy 表中删除 film_id 为 10 或者 11 的 2 个影片，并返回删除的影片的标题
DELETE FROM film_copy
WHERE film_id in (10, 11)
RETURNING film_id, title
```



## 清空表

```sql
TRUNCATE [TABLE] [ONLY] table_name [ * ] [, ... ]
    [RESTART IDENTITY | CONTINUE IDENTITY] [ CASCADE | RESTRICT ]

```

- `TABLE` 关键字是可选的。
- `ONLY` 关键字是可选的。如果在表名前指定了 `ONLY`，则只清空此表，不包含它的子表。否则，此表和它的子表都将被清空。
- `table_name` 是要清空的表的名字。 表名后的 `*` 明确的指示子表也将被清空。
- 您可以在一个 `TRUNCATE` 语句中清空多个表。 多个表名使用逗号分隔。
- `RESTART IDENTITY` 选项指示自动重置表中的列拥有的序列。 `CONTINUE IDENTITY` 选项指示不改变表中的序列的值，它是默认的。
- `CASCADE` 选项指示同时清空那些通过外键引用 `table_name` 的表。 `RESTRICT` 选项指示如果有外键引用要清空的表，则拒绝操作。



```sql
# 建表
CREATE TABLE test_truncate (
  v INTEGER
);


# 查询
INSERT INTO test_truncate (v)
SELECT generate_series(1, 10000000) v;

# 从表中删除 10000000 行，总共耗费 6566.458 
DELETE FROM test_truncate;
# 清空表，共耗费 31.785 毫秒
TRUNCATE TABLE test_truncate;
```



## 修改数据

```sql
UPDATE [IGNORE] table_name
SET
    column_name1 = value1,
    column_name2 = value2,
    ...
[WHERE clause]
[RETURNING expr];

```

- `UPDATE` 关键字后指定要更新数据的表名。

- 使用 `SET` 子句设置列的新值。多个列使用逗号分隔。列的值可以是普通的字面值，也可以是表达式运算，还可以是子查询。

- 使用 [`WHERE`](https://www.sjkjc.com/postgresql/where/) 子句指定要更新的行的条件。只有符合 `WHERE` 条件的行才会被更新。

- `WHERE` 子句是可选的。如果不指定 `WHERE` 子句，则更新表中的所有行。

- `RETURNING` 子句是可选的。它用于返回更新的行的信息。

  `expr` 可以是列名或者表达式，多个列或者表达式请使用逗号分隔。 您还可以使用 `*` 表示表中的所有的列。

  如果不指定 `RETURNING` 子句， `UPDATE` 语句将返回更新的行数。

`UPDATE` 语句中的 `WHERE` 子句非常重要。除非您特意，否则不要省略 `WHERE` 子句。





```sql
# 先查询一次数据
SELECT first_name, last_name, email
FROM customer
WHERE customer_id = 1;


# UPDATE 语句更新 email 列的值
UPDATE customer
SET email = 'NEW.MARY.SMITH@sakilacustomer.org'
WHERE customer_id = 1;

# UPDATE 修改多列值
UPDATE customer
SET first_name = 'Tim',
    last_name = 'Duncan',
    email = 'Tim.Duncan@sakilacustomer.org'
WHERE customer_id = 1
RETURNING first_name, last_name, email;

```

**可以使用以下 `RETURNING` 子句直接查看更新后的数据**

```sql
UPDATE customer
SET email = 'NEW.MARY.SMITH@sakilacustomer.org'
WHERE customer_id = 1
RETURNING first_name, last_name, email;

```



**使用表达式更新**

```sql
UPDATE customer
SET email = REPLACE(email, 'sakilacustomer.org', 'sjkjc.com')
RETURNING first_name, last_name, email;

```



**使用子查询更新**

```sql
UPDATE customer
SET store_id = (
    SELECT store_id
    FROM store
    ORDER BY random()
    LIMIT 1
  )
WHERE store_id IS NULL;

```



## UPDATE ... FROM 用法

有时候，需要根据另一个表中的数据更新一个表中的数据。比如：根据产品销量明细表更新销量统计表

```sql
UPDATE [IGNORE] table_name
SET
    column_name1 = value1,
    column_name2 = value2,
    ...
FROM another_table[, ...]
WHERE clause
[RETURNING expr];

```

- 和普通的 [`UPDATE`](https://www.sjkjc.com/postgresql/update/) 语句相比，此语句多了 `FROM` 子句，并且 `WHERE` 子句是必须的。
- 您需要在 `WHERE` 子句中指定两个表连接的条件



```sql
# 对于 a 表的每一行，该 UPDATE 语句都检查 b 表的每一行。如果值 a 表的 b_id 列的值等于在 b 表的 id 列，该 UPDATE 语句将更新 b 的表 c2 列的值到 a 表的 c1 列
UPDATE a
SET a.c1 = b.c2
FROM b
WHERE a.b_id = b.id;

```



```sql
# 现在有一个需求，需要更新 city 表中的城市名称，在其后添加 @ 和国家名
UPDATE city_copy a
SET city = city || '@' || b.country
FROM country b
WHERE b.country_id = 1 or b.country_id = 2
RETURNING city_id, city;

# 也可以使用子查询实现上面的需求
UPDATE city_copy a
SET city = (
  SELECT a.city || '@' || b.country
  FROM country b
    WHERE a.country_id = b.country_id
)
RETURNING city_id, city;

```



## 查询数据

### 基本查询

```sql
SELECT
    expr_list
FROM
    table_name
[other_clauses];
```

- `SELECT` 和 `FROM` 是关键字。
- `expr_list` 是要选择的列或者表达式的列表。多个列或表达式需要使用逗号分隔。
- `table_name` 是要查询的数据表。
- `FROM table_name` 是可选的。如果你不查询任何表中的行，则可以省略 `FROM` 子句。
- `other_clauses` 是 `SELECT` 语句支持的子句。 `SELECT` 语句支持很多子句，包括：
  - 使用 [`DISTINCT`](https://www.sjkjc.com/postgresql/distinct/) 运算符选择不同的行。
  - 使用 [`ORDER BY`](https://www.sjkjc.com/postgresql/order-by/) 子句对行进行排序。
  - 使用 [`WHERE`](https://www.sjkjc.com/postgresql/where/) 子句过滤行。
  - 使用 [`LIMIT`](https://www.sjkjc.com/postgresql/limit/) or [`FETCH`](https://www.sjkjc.com/postgresql/fetch/) 子句从表中选择行的子集。
  - 使用 [`GROUP BY`](https://www.sjkjc.com/postgresql/group-by/) 子句将行分组。
  - 使用 [`HAVING`](https://www.sjkjc.com/postgresql/having/) 子句过滤组。
  - 使用诸如 `INNER JOIN`, `LEFT JOIN`, `FULL OUTER JOIN`, `CROSS JOIN` 之类的与其他表[连接](https://www.sjkjc.com/postgresql/join/)。
  - 使用 [`UNION`](https://www.sjkjc.com/postgresql/union/) ， [`INTERSECT`](https://www.sjkjc.com/postgresql/intersect/) 和 [`EXCEPT`](https://www.sjkjc.com/postgresql/except/) 执行集合运算

### where条件

```sql
SELECT columns_list
FROM table_name
WHERE query_condition;


# 查找名字和姓氏为 JAMIE 和 RICE 的客户
SELECT last_name,
  first_name
FROM customer
WHERE first_name = 'JAMIE'
  AND last_name = 'RICE';
  
  
# 查找姓氏为 RODRIGUEZ 或名字为 ADAM 的客户
SELECT first_name,
  last_name
FROM customer
WHERE last_name = 'RODRIGUEZ'
  OR first_name = 'ADAM';


# 返回名字为 ANN, ANNE, 或 ANNIE 的客户
SELECT first_name,
  last_name
FROM customer
WHERE first_name IN ('ANN', 'ANNE', 'ANNIE');


# 返回名字以字符串 ANN 开头的所有客户
SELECT first_name,
  last_name
FROM customer
WHERE first_name LIKE 'ANN%';

# 查找名字以字母 A 开头并包含 3 到 5 个字符的客户
SELECT first_name,
  LENGTH(first_name) name_length
FROM customer
WHERE first_name LIKE 'A%'
  AND LENGTH(first_name) BETWEEN 3 AND 5
ORDER BY name_length;


# 查找名字以 BRA 开头而姓氏不以 MOTLEY 开头的客户
SELECT first_name,
  last_name
FROM customer
WHERE first_name LIKE 'BRA%'
  AND last_name <> 'MOTLEY';
```

- `=` : 相等
- `>` : 大于
- `<` : 小于
- `>=` : 大于或等于
- `<=` : 小于或等于
- `<>` : 不相等
- `!=` : 不相等，等同于 `<>`
- `AND` : 逻辑与运算符
- `OR` : 逻辑或运算符
- [`IN`](https://www.sjkjc.com/postgresql/in/) : 如果值与列表中的任何值匹配，则返回 true
- [`BETWEEN`](https://www.sjkjc.com/postgresql/between/) : 如果一个值在一个值范围之间，则返回 true
- [`LIKE`](https://www.sjkjc.com/postgresql/like/) : 如果值与模式匹配，则返回 true
- [`IS NULL`](https://www.sjkjc.com/postgresql/is-null/) : 如果值为 NULL，则返回 true
- `NOT` : 否定其他运算符的结果





### ORDER BY排序

 `ORDER BY` 子句可以让我们对 `SELECT` 语句返回的结果集按照一个或这多个列升序或者降序排序

```sql
SELECT
   column1, column2, ...
FROM
   table_name
[WHERE clause]
ORDER BY
   column1 [ASC|DESC],
   [column2 [ASC|DESC],
   ...]
   [NULLS FIRST | NULLS LAST]
   ;

```

- 可以为 `ORDER BY` 子句指定一个或多个列或者表达式。

- `ASC` 代表升序，`DESC` 代表降序。这是可选的，默认值是 `ASC`。

- 当指定多个排序表达式时，首先按照前面的表达式排序，其次按照后面的列排序。

- `NULLS FIRST` 和 `NULLS LAST` 用来指定对 null 值排序规则：

  - `NULLS FIRST`： null 值在非 null 值之前。
  - `NULLS LAST`： null 值在非 null 值之后。

  默认情况下，PostgreSQL 采用升序排序时采用 `NULLS LAST`，降序排序时采用 `NULLS FIRST`。 也就是说， PostgreSQL 默认 null 值比非 null 值大。





```sql
# 按演员姓氏升序进行排序
SELECT
    actor_id, first_name, last_name
FROM
    actor
ORDER BY last_name;


# 按演员姓氏降序进行排序
SELECT
    actor_id, first_name, last_name
FROM
    actor
ORDER BY last_name DESC;


# 先按演员姓氏升序排序，再按演员名字升序排序
SELECT
    actor_id, first_name, last_name
FROM
    actor
ORDER BY last_name, first_name;


# 自定义顺序排序
# 根据影片的分级按照的 'G', 'PG', 'PG-13', 'R', 'NC-17' 顺序对影片进行排序
SELECT
    film_id, title, rating
FROM
    film
ORDER BY CASE rating
    WHEN 'G' THEN 1
    WHEN 'PG' THEN 2
    WHEN 'PG-13' THEN 3
    WHEN 'R' THEN 4
    WHEN 'NC-17' THEN 5
END;
```



**ORDER BY 和 NULL**

在 PostgreSQL 中的升序排序中， `NULL` 值出现在非 NULL 值之前

以下实例使用以下临时数据作为演示

```sql
SELECT 'A' AS v
UNION ALL
SELECT 'B' AS v
UNION ALL
SELECT NULL AS v
UNION ALL
SELECT '0' AS v
UNION ALL
SELECT '1' AS v;


# ASC 排序时， NULL 值默认排在非 NULL 值的后面
SELECT 'A' AS v
UNION ALL
SELECT 'B' AS v
UNION ALL
SELECT NULL AS v
UNION ALL
SELECT '0' AS v
UNION ALL
SELECT '1' AS v
ORDER BY v;


# ASC 排序采用 NULLS LAST 规则，所以 NULL 值在最后。 如果您想要改用 NULLS FIRST
SELECT 'A' AS v
UNION ALL
SELECT 'B' AS v
UNION ALL
SELECT NULL AS v
UNION ALL
SELECT '0' AS v
UNION ALL
SELECT '1' AS v
ORDER BY v NULLS FIRST;


# 使用 ORDER BY 子句降序 DESC 排序时， NULL 值排在非 NULL 值的前面。这是因为 DESC 排序默认采用 NULLS FIRST 规则
SELECT 'A' AS v
UNION ALL
SELECT 'B' AS v
UNION ALL
SELECT NULL AS v
UNION ALL
SELECT '0' AS v
UNION ALL
SELECT '1' AS v
ORDER BY v DESC;

```



### FETCH限定查询返回行数

```sql
FETCH { FIRST | NEXT } [ rows_count ] { ROW | ROWS } ONLY

```

- 可以使用 `FIRST` 和 `NEXT` 中的任意一个，他们含义相同。
- 可以使用 `ROW` 和 `ROWS` 中的任意一个，他们含义相同。
- `rows_count` 是要限制的行数，即返回的最大的行数。 它是可选的，默认值为 1。您应该为 `rows_count` 指定一个大于 0 的整数值。

```sql
SELECT column_list
FROM table_name
[other_clauses]
FETCH rows_count;

# other_clauses 是那些可以在 SELECT 语句中使用的其他子句，比如 WHERE, ORDER BY, OFFSET 等
# 需要在带有 FETCH 子句的 SELECT 语句中一同使用 ORDER BY 子句，这样您可以得到一个按照指定的顺序排序的结果集
```

```sql
SELECT column_list
FROM table_name
ORDER BY ...
OFFSET skipped_rows
FETCH FIRST rows_count ROWS ONLY;

```

- 第一页可以使用： `OFFSET 0 OFFSET FIRST 10 ROWS ONLY` 表示最多返回 10 行。
- 第二页可以使用： `OFFSET 10 OFFSET FIRST 10 ROWS ONLY` 表示跳过第一页的 10 行后最多返回 10 行。
- 第三页可以使用： `OFFSET 20 OFFSET FIRST 10 ROWS ONLY` 表示跳过前两页的 20 行后最多返回 10 行。
- 以此类推



```sql
#从 film 表查询时最多返回 5 行，使用下面的带有 FETCH 子句的 SELECT 语句
SELECT
  film_id,
  title,
  release_year
FROM film
ORDER BY film_id
FETCH FIRST 5 ROWS ONLY;

# 要获得租金最高的 10 部电影，可以按租金降序对电影进行排序，然后使用 FETCH 子句获得前 10 部电影
SELECT
  film_id,
  title,
  rental_rate
FROM film
ORDER BY rental_rate DESC, film_id
FETCH FIRST 10 ROWS ONLY;


```



### FETCH 和 OFFSET 分页查询示例

```sql
# film 表中共有 1000 行关于影片的信息
SELECT COUNT(*) FROM film;

# 需要每页显示 10 个影片信息，那么可以使用如下的语句获取第一页的所有行
# 为了让所有分页的顺序一致，我们使用 ORDER BY film_id 让影片按照 film_id 排序，并使用 FETCH FIRST 10 ROWS ONLY 限制了此查询最多返回 10 行
SELECT
  film_id,
  title,
  release_year
FROM film
ORDER BY film_id
FETCH FIRST 10 ROWS ONLY;


# 为了获取第二页要显示的 10 行，使用 OFFSET 10 子句跳过第一页的 10 行，并使用 FETCH FIRST 10 ROWS ONLY 限制了此查询最多返回 10 行
SELECT
  film_id,
  title,
  release_year
FROM film
ORDER BY film_id
OFFSET 10
FETCH FIRST 10 ROWS ONLY;


# 取第三页的所有行
# 使用 OFFSET 20 指示了跳过前两页的 20 行，并使用 FETCH FIRST 10 ROWS ONLY 限制了此查询最多返回 10 行
SELECT
  film_id,
  title,
  release_year
FROM film
ORDER BY film_id
OFFSET 20
FETCH FIRST 10 ROWS ONLY;

```



### LIMIT 子句













# 问题

数据库；表空间
表；标识列

FETCH 和 OFFSET分页和limit分页
