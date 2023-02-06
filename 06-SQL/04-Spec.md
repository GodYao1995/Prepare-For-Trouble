[TOC]

### 遵守规则

#### 库、表

|   规则   |                             说明                             | 等级 |
| :------: | :----------------------------------------------------------: | :--: |
|   注释   |                           字段注释                           | 强制 |
|   编码   |                utf8编码、存储表情采用utf8mb4                 | 强制 |
|    库    |       库名与应用名称一致,可采用业务名称_表的作用 命名        | 强制 |
| 表、字段 |   小写字母、数字、下划线;禁止数字开头;禁止保留字;禁止复数;   | 强制 |
| 必备字段 | 主键id unsigned bigint 递增步长为1;创建时间;修改时间,为datetime类型 | 强制 |
| 冗余字段 |             允许字段冗余;不能频繁修改、不能过长              | 推荐 |
| 是否字段 |               is_xx命名、unsigned tinyint类型                | 强制 |
|   索引   | 主键索引采用pk_字段名命名;唯一索引uk\_字段名;普通所以idx\_字段名命名 | 强制 |
| 小数类型 | 使用decimal; 禁止使用float与double,其存在精度损失;存储范围超过decimal,则可以整数小数分开存储 | 强制 |
| varchar  | 可变字符串、不预先分配存储空间、长度不要超过5000,如果大于5000,则用text在另一张表存储,用主键对应 | 强制 |
| 分库分表 |                        视业务场景而定                        | 推荐 |

#### 索引

|   类别   |                         规则                         | 等级 |                    备注                    |
| :------: | :--------------------------------------------------: | :--: | :----------------------------------------: |
| 唯一索引 |                 业务上唯一特性字段;                  | 强制 | 影响插入效率但是提高查询效率并且避免脏数据 |
|   join   |    禁止三张表join,需要join的字段数据类型必须一致     | 强制 |         保证表的关联字段需要建索引         |
| varchar  |           指定索引长度;没必要全字段建索引            | 强制 |                                            |
|   搜索   | 搜索禁止左模糊或者全模糊,无法遵循B Tree最左前缀原则; | 强制 |             请使用专业搜索引擎             |
| order by |            order by场景,注意索引的有序性;            | 强制 |                   不清晰                   |

#### SQL

|   类别   |                    规则                     | 等级 |            备注            |
| :------: | :-----------------------------------------: | :--: | :------------------------: |
|  count   |            使用count(*)统计行数             | 强制 |   count(col)不会统计nul    |
|  count   | count(distinct col)统计出Null外不重复的行数 | 强制 | count(distinct col1, col2) |
| is null  |               判断是否为Null                | 强制 |                            |
|   分页   |     若count为0应该直接返回避免后续查询      | 强制 |                            |
| 存储过程 |                禁止存储过程                 | 强制 |                            |
| 数据修改 |             先SELECT确认再修改              | 强制 |                            |
|    in    |        避免使用，in元素控制1000以内         | 推荐 |                            |
| truncate |                禁止truncate                 | 参考 |                            |