#赶集mysql军规

总是在灾难发生后,才想起容灾的重要性.
总是在吃过亏后,才记得曾经有人提醒过.

##一,核心军规
1. 不在数据做计算,CPU计算务必移至业务层
2. 控制单表数据量,单表记录控制在千万级
3. 控制列数量,字段数控制在20以内
4. 平衡范式和冗余,为提高效率可以牺牲范式设计,冗余数据
5. 拒绝3B,大SQL,大事物,大批量

##二,字段类军规
1. 用好数据类型
* tinyint(1Byte)
* smallint(2Byte)
* mediumint(3Byte)
* int(4Byte)
* bigint(8Byte)
* bad case :int(1)/int(11)

2. 有些字符转化为数字
* 用int而不是char(15)存储ip

3. 优先使用enum或set
* 例如:sex enum('F','M')

4. 避免使用NULL字段
* NUll字段很难查询优化
* NULL字段的索引需要额外空间
* NULL字段的复合索引无效
* bad case：
* `name` char(32) default null
* `age` int not null
* good case：
* `age` int not null default 0
5. 不在数据库中存图片

##三,索引类军规
1. 谨慎合理使用索引
* 改善查询 减慢更新
* 索引一定不是越多越好(能不加就不加,要加的一定得加)
* 覆盖记录条数过多不适合建索引,例如"性别"

2. 字符字段必须建前缀索引

3. 不在索引做列运算
* bad case:
* select id where age + 1 = 10;

4. innodb主键合理使用自增列
* 主键建立聚簇索引
* 主键不应该被修改
* 字符串不应该做主键
* 如果不指定主键,innodb会使用唯一且空值索引代替

5. 不用外键,请由程序保证约束

##四,SQL类军规
1 SQL语句尽可能简单
* 一条SQL只能在一个CPU运算
* 大语句拆小语句,减少锁时间
* 一条大SQL可以堵死整个库

2 简单的事务
* 事务时间尽可能短
* bad case
* 上传图片事务

3 避免使用触发器,用户自定义函数,请由程序取而代之

4 不用select *
* 消耗CPU,io,内存,带宽
* 这种程序不具有扩展性

5 OR改写为IN()

6 OR改写为UNION

7 limit高效分页
* limit越大,效率越低
* select id from t limit 10000, 10;
* 应改为 select id form t where id > 10000 limit 10;

8 使用union all替代union,union有去重开销

9 尽量不用连接join

10 务必请使用"同类型"进行比较,否则可能全表扫描

11 打散批量更新

12 使用性能分析工具
* show profile;
* mysqlsla;
* mysqldumpslow;
* explain;
* show slow log;
* show processlist;
* show query_response_time(percona)
    