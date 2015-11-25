## MySql


#### 分表原则
    1. 表多数据多 垂直拆分
    2. 表少数据多 水平拆分（hash ID）
    
####  主键生成策略
    1. UUID消耗太多空间，索引性能较差
    2. 结合数据库维护Sequence表，单点瓶颈及故障
    3. flickr 方案，两台数据ID生成服务器，一台起始值1步长为2，另一台其实值为2步长为2
    
### High Performance
#### 数据类型
    1. 尽量选择占用空间小的数据类型
    2. 尽量悬着简单/恰当的类型
    3. 尽量将字段设置为not null
        3.1 MySql服务器自身的 查询优化功能将会受影响
        3.2 MySql针对null值的字段需要额外的存储空间以及处理
        3.3 如果一个null值是索引的一部分，那么索引的效果也会收到影响
#### Alter Table
    更新用户表的默认密码为888888
    1. ALTER TABLE `user` MODIFY COLUMN `pwd` VARCHAR(32) NOT NULL DEFAULT '888888';
    执行show status发现大量的insert操作，数据量大会消耗太多时间
    2. ALTER TABLE `user` ALTER COLUMN `pwd` VARCHAR(32) NOT NULL DEFAULT '888888';
    执行show status大量的insert操作不见了，时间缩短了
    
    时间缩短的原因为：
    （1） 表字段的默认值是放在表的frm(.frm:表结构文件  .MYD:表数据文件  .MYI:表索引)文件中
    （2） ALTER COLUMN会更新frm文件，而不会涉及到表的内容
    （3） MODIFY COLUMN会涉及到表数据的内容
    
    并不是所有的alter table都可以通过修改frm文件方式来提高修改效率，下面的一些改动可以通过修改frm文件的方式达到更新的目的：
    （1） 更改字段的默认值
    （2） 增加/删除字段的AUTO_INCREMENT属性
    （3） 增加/删除/修改 ENUM的常量值。对于删除操作，如果有字段引用了这个常量值，则在删除后查询的结构为空字符串
