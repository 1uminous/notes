# MySQL 

### part 1. 数据库搭建

使用docker搭建mysql服务，这里有踩个坑 官方镜像启动的MySQL字符编码是latin1, 这里修改mysql的配置文件来加载字符编码配置

```yaml
[client]
default-character-set=utf8mb4
[mysql]
default-character-set=utf8mb4
[mysqld]
collation-server=utf8mb4_general_ci
character-set-server=utf8mb4
init-connect='SET NAMES utf8mb4'
```

保存为mysql.conf

然后运行docker 命令 一把梭哈😄

```shell
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password -v /root/mysql.cnf:/etc/mysql/conf.d/mysql.cnf --hostname mysql --name mysql --restart unless-stopped mysql
```

下载datawhale 课程给的sql脚本

```
wget https://raw.githubusercontent.com/datawhalechina/wonderful-sql/main/materials/00%E5%BB%BA%E8%A1%A8%E8%AF%AD%E5%8F%A5/shop.sql
```

导入数据文件到数据库

```sql
docker cp ./shop.sql mysql:/etc/shop.sql
docker exec -it mysql /bin/bash
mysql -u root -p
...
...
create database shop;
use shop;
source /etc/shop.sql;
```

使用DBeaver测试连接数据库
坑2 ... 连接报错 public key retrieval is not allowed  [参考](https://stackoverflow.com/questions/50379839/connection-java-mysql-public-key-retrieval-is-not-allowed)
客户端的连接选项需要添加两个属性允许公钥和不验证ssl
key: rewriteBatchedStatements value: true
key: useSSL value: false

至此完成搭建测试过程

## 练习题

1.1-1.2 一把梭哈


```sql
DROP TABLE IF EXISTS `Addressbook`;

CREATE TABLE `Addressbook` (
  `regist_no` int NOT NULL,
  `name` varchar(128) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL,
  `address` varchar(256) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL,
  `tel_no` char(10) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL,
  `mail_address` char(20) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL,
  `postal_code` char(8) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL;
  PRIMARY KEY (`regist_no`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
保存 为 sql.sql
use shop;
source sql.sql;

cli 1.1-1.2 图
![图1](https://raw.githubusercontent.com/1uminous/notes/b2e03312b37cf9559e466bd8b73a9cc9487f5f7e/Screen%20Shot%202022-07-11%20at%209.27.23%20PM.png)
![图2](https://raw.githubusercontent.com/1uminous/notes/b2e03312b37cf9559e466bd8b73a9cc9487f5f7e/Screen%20Shot%202022-07-11%20at%209.32.07%20PM.png)

1.3 DROP table Addressbook;

1.4 no backup = gg

