# PHP必知必会100点
----

>参考：[Markdown基本语法](https://www.jianshu.com/p/191d1e21f7ed)  
>前提：php 7.2

* empty()判断空值时的特例
```
<?php
$val = '0';
var_dump(empty($val)); //true

```
* display_errors()
* error_reporting(E_ALL)
* date_default_timezone_set('UTC');
* & | ~ 的含义
* << >> 的含义
* composer.json版本限定符
```
~1.2 相当于 >=1.2 <2.0
~1.2.3 相当于 >=1.2.3 <1.3.0
^1.2.3 相当于 >=1.2.3 <2.0.0
```
* xdebug_debug_zval()
* memory_get_usage()
* php中引用的含义
* php写时拷贝
* php的普通赋值和引用赋值
* static::延迟绑定
* strtotime的特殊用法
```
<?php
echo strtotime("now"), "\n";
echo strtotime("10 September 2000"), "\n";
echo strtotime("+1 day"), "\n";
echo strtotime("+1 week"), "\n";
echo strtotime("+1 week 2 days 4 hours 2 seconds"), "\n";
echo strtotime("next Thursday"), "\n";
echo strtotime("last Monday"), "\n";
```
* $_SERVER['REQUEST_TIME'] 中保存了发起该请求时刻的时间戳
* mktime()的用法
* array_filter()
* PDO
* set_exception_handler()
* set_error_handler()
* intdiv() 与 floor() 与 ceil() 与 round()
* is_scalar()
```
作用：检测变量是否是一个标量。
 类型为 integer、float、string 或 boolean 的变量为标量，而类型为 array、object 和 resource 的变量不是标量。
```
* is_iterable()
```
作用：检测变量的是否是一个可迭代的值。
```
* 函数别名
```
doubleval()==floatval()
is_double()==is_float
is_real()==is_float()
is_integer()==is_int()
is_long()==is_int()
```
* yield 的用法
* serialize() 与 unserialize()
* base64_encode() 与 base64_decode()
* var_export()的用法
* split() 与 str_split() 与 chunk_split()
* array_filter() 与 array_map() 与 array_walk()
* list 的用法
* ord() 的使用
* gmstrftime()的使用
* 数据库事务四种隔离级别
```
读未提交（read-uncommitted）所有事务都可以看到其他未提交事务的执行结果。很少用于实际应用，因为它的性能也不比其他级别好多少。会产生脏读，不可重复读以及幻读
不可重复读（read-committed）这是大多数数据库系统的默认隔离级别（但不是 MySQL 默认的）。它满足了隔离的简单定义：一个事务只能看见已经提交事务所做的改变。会产生不可重复读，幻读
可重复读（repeatable-read）这是 MySQL 的默认事务隔离级别，它确保同一事务的多个实例在并发读取数据时，会看到同样的数据行。不过理论上，会导致另一个棘手的问题：幻读 （Phantom Read）。简单的说，幻读指当用户读取某一范围的数据行时，另一个事务又在该范围内插入了新行，当用户再读取该范围的数据行时，会发现有新的 “幻影” 行。InnoDB 和 Falcon 存储引擎通过多版本并发控制（MVCC，Multiversion Concurrency Control）机制解决了该问题。
串行化（serializable）这是最高的隔离级别，它通过强制事务排序，使之不可能相互冲突，从而解决幻读问题。简言之，它是在每个读的数据行上加上共享锁。在这个级别，可能导致大量的超时现象和锁竞争。
```
* mysql 的三种锁
```
表级锁：开销小，加锁快；不会出现死锁；锁定粒度大，发生锁冲突的概率最高，并发度最低。
行级锁：开销大，加锁慢；会出现死锁；锁定粒度最小，发生锁冲突的概率最低，并发度也最高。
页面锁：开销和加锁时间界于表锁和行锁之间；会出现死锁；锁定粒度界于表锁和行锁之间，并发度一般
```
* INNODB 锁并发问题
```
1、脏读：事务 A 读取了事务 B 更新的数据，然后 B 回滚操作，那么 A 读取到的数据是脏数据
2、不可重复读：事务 A 多次读取同一数据，事务 B 在事务 A 多次读取的过程中，对数据作了更新并提交，导致事务 A 多次读取同一数据时，结果 不一致。
3、幻读：系统管理员 A 将数据库中所有学生的成绩从具体分数改为 ABCDE 等级，但是系统管理员 B 就在这个时候插入了一条具体分数的记录，当系统管理员 A 改结束后发现还有一条记录没有改过来，就好像发生了幻觉一样，这就叫幻读。
4、更新丢失（Lost Update）：当两个或多个事务选择同一行，然后基于最初选定的值更新该行时，由于每个事务都不知道其他事务的存在，就会发生丢失更新问题－－最后的更 新覆盖了由其他事务所做的更新。例如，两个编辑人员制作了同一文档的电子副本。每个编辑人员独立地更改其副本，然后保存更改后的副本，这样就覆盖了原始文 档。最后保存其更改副本的编辑人员覆盖另一个编辑人员所做的更改。如果在一个编辑人员完成并提交事务之前，另一个编辑人员不能访问同一文件，则可避免此问题。
不可重复读的和幻读很容易混淆，不可重复读侧重于修改，幻读侧重于新增或删除。解决不可重复读的问题只需锁住满足条件的行，解决幻读需要锁表
```
* nginx 的负载均衡有 4 种模式
```
轮询（默认）每个请求按时间顺序逐一分配到不同的后端服务器，如果后端服务器 down 掉，能自动剔除。
Weight 指定轮询几率，weight 和访问比率成正比， 用于后端服务器性能不均的情况。
ip_hash 每个请求按访问 ip 的 hash 结果分配，这样每个访客固定访问一个后端服务器，可以解决 session 共享的问题。
fair（第三方）按后端服务器的响应时间来分配请求，响应时间短的优先分配。
url_hash（第三方）
```
* nginx 与 apache
```
最核心的区别在于 apache 是同步多进程模型，一个连接对应一个进程；nginx 是异步的，多个连接（万级别）可以对应一个进程 （nginx 处理请求是异步非阻塞的，而 apache 则是阻塞型的）
在高并发下 nginx 能保持低资源低消耗高性能。
apache 相对于 nginx 的优点： rewrite ，比 nginx 的 rewrite 强大 模块超多，基本想到的都可以找到 少 bug 。
```
* MyISAM 和 InnoDB
```
MyISAM 是非事务安全型的，而 InnoDB 是事务安全型的。
MyISAM 锁的粒度是表级，而 InnoDB 支持行级锁定。
MyISAM 支持全文类型索引，而 InnoDB 不支持全文索引。
MyISAM 相对简单，所以在效率上要优于 InnoDB，小型应用可以考虑使用 MyISAM。
MyISAM 表是保存成文件的形式，在跨平台的数据转移中使用 MyISAM 存储会省去不少的麻烦。
InnoDB 表比 MyISAM 表更安全，可以在保证数据不会丢失的情况下，切换非事务表到事务表（alter table tablename type=innodb）。
```
* Mysql 的存储引擎和索引
```
InnoDB 使用的是聚簇索引，将主键组织到一棵 B + 树中，而行数据就储存在叶子节点上，若使用 "where id = 14" 这样的条件查找主键，则按照 B + 树的检索算法即可查找到对应的叶节点，之后获得行数据。若对 Name 列进行条件搜索，则需要两个步骤：第一步在辅助索引 B + 树中检索 Name，到达其叶子节点获取对应的主键。第二步使用主键在主索引 B + 树种再执行一次 B + 树检索操作，最终到达叶子节点即可获取整行数据。
MyISM 使用的是非聚簇索引，非聚簇索引的两棵 B + 树看上去没什么不同，节点的结构完全一致只是存储的内容不同而已，主键索引 B + 树的节点存储了主键，辅助键索引 B + 树存储了辅助键。表数据存储在独立的地方，这两颗 B + 树的叶子节点都使用一个地址指向真正的表数据，对于表数据来说，这两个键没有任何差别。由于索引树是独立的，通过辅助键检 i 索无需访问主键的索引树。
```
* Mysql 索引为什么选择 B + 树
```
mysql 主要是由 server 层和存储层两部分构成的。server 层主要包括连接器、查询缓存，分析器、优化器、执行器。存储层主要是用来存储和查询数据的，常用的存储引擎有 InnoDB、MyISAM，MySQL 5.5.5 版本后使用 InnoDB 作为默认存储引擎。
几种常见的数据类型哈希表适合等值查询，由于是无序的，区间查询会很慢有序数组适合等值和区间查询，但是数组具有连续性，插入和删除操作都可能需要移动其他元素。二叉搜索树由于树的高度，区间查询需要中序遍历，都会导致查询效率很慢。 B+ 树就是通过二叉搜索树推演改进的
B+ 树就是一种多叉树，是由二叉搜索树不断演变过来的，为了满足区间快速查询，B+ 树的叶子节点通过双向链表串联起来。
这里使用双向链表是为了支持顺序和倒序查询，虽然双向链表相对于单向链表虽然会浪费一倍的指针空间，但是在硬盘中这点空间几乎微乎其微，用这点空间换时间是一件很值得的事情。
B+ 树的子节点数不超过 m 个，同时也不能少于 m/2 个，一旦超过就需要分裂，一旦少于就需要合并。
而 InnoDB 在底层是采用 B+ 树这种数据结构来存储数据的。
```
* Mysql Explain 返回参数说明
```
table 显示这一行的数据是关于哪张表的
type 这是重要的列，显示连接使用了何种类型。从最好到最差的连接类型为 const、eq_reg,ref、range、indexhe 和 ALL
possible_keys 显示可能应用在这张表中的索引。如果为空，没有可能的索引。
key 实际使用的索引。如果为 NULL，则没有使用索引。
key_len 使用的索引的长度。在不损失精确性的情况下，长度越短越好
ref 显示索引的哪一列被使用了，如果可能的话，是一个常数
rows MYSQL 认为必须检查的用来返回请求数据的行数
```
* 多路 I/O 复用模型
```
多路 I/O 复用模型是利用 select、poll、epoll 可以同时监察多个流的 I/O 事件的能力，在 空闲的时候，会把当前线程阻塞掉，当有一个或多个流有 I/O 事件时，就从阻塞态中唤 醒，于是程序就会轮询一遍所有的流（epoll 是只轮询那些真正发出了事件的流），并且只 依次顺序的处理就绪的流，这种做法就避免了大量的无用操作。 这里 “多路” 指的是多个网络连接，“复用” 指的是复用同一个线程。采用多路 I/O 复用 技术可以让单个线程高效的处理多个连接请求（尽量减少网络 IO 的时间消耗），且 Redis  在内存中操作数据的速度非常快，也就是说内存内的操作不会成为影响 Redis 性能的瓶颈， 主要由以上几点造就了 Redis 具有很高的吞吐量。
```
* mysql group_concat()的使用
```
参考：https://www.cnblogs.com/wenxinphp/p/5841430.html
```
* MySQL的索引
```
参考：https://mp.weixin.qq.com/s/OMgyqqi-r44KI-TjYKP59g
https://learnku.com/articles/25020
```