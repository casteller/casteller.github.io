---
title: Redis基础
author: MZ-ZONE
top: true
cover: true
toc: true
mathjax: false
date: 2020-08-24 19:31:11
img:
headimg: https://cdn.jsdelivr.net/gh/volantis-x/cdn-wallpaper-minimalist/2020/019.jpg
coverImg:
password:
summary:
tags: redis
categories: redis
---
String
set，设置键
set name jack
get，获取键的值
get name
exists，判断该键是否存在，存在返回1，不存在返回0
exists name
append，如果该键不存在，则创建，返回当前value的长度；如果该键已经存在，则追加，返回追加后value的长度
append city beijing
如果值有空格，需要加引号
append city “ of china”
strlen，获取key的长度
strlen name
可以看到提示，有很多选项
EX和PX表示失效时间，单位为秒和毫秒，两者不能同时使用；
NX表示数据库中不存在时才能设置，XX表示存在时才能设置
ttl查看过期剩余时间，如果为-2表示已经过期
flushdb，清空数据库
keys * 查看所有键
incr，递增1
decr，递减1
del，删除键
删除后，get不到值，但是可以进行incr和decr操作，是基于默认值为0进行操作
incrby，递增，可以设置步长,不加步长会报错
incrby age 5
decrby，递减，可以设置步长 
getset，获取的同时并设置新的值
getset age 20
setex，设置过期时间，等同于set name jack ex 10
setex name 10 jack
setnx，当key不存在时才能设置，等同于set name jack nx；如果key存在，就不能设置
setrange，设置指定索引位置的字符，索引从0开始

超过的长度使用0代替
getrange，获取指定索引位置的字符，索引从0开始 
ep:获取索引为[1,7]之间的内容，闭区间
getrange name 1 7
setbit/getbit，设置/获取指定位的BIT值，应用场景：考勤打卡
设置从0开始计算的第七位BIT值为1，返回原有BIT值0
获取设置的结果，二进制的0000 0001的十六进制值为0x01
设置从0开始计算的第六位BIT值为1，返回原有BIT值0
获取设置的结果，二进制的0000 0011的十六进制值为0x03
mset，批量设置key
mset key1 "aaa" key2 "bbb"
mget，批量获取
mget key1 key2
msetnx，批量设置key，如果key都不存在，执行成功并返回1；如果有一个key存在，执行失败并返回0。
List
是按照插入顺序排序的字符串链表
lpush
创建键test及与其关联的List，然后将参数中的values从左到右依次插入【看着从左往右放的栈】
lrange
获取从位置0开始到位置2结束的3个元素
lrange test 0 2
获取链表中的全部元素，其中0表示第一个元素，­-1表示最后一个元素
lrange test 0 -1
获取从倒数第3个到倒数第2个的元素
lrange -3 -2
lpushx，表示键存在时才能插入
如果键不存在，命令将不会进行任何操作，其返回值为0
获取该键的List中的第一个元素
lrange test 0 0
lpop，取出链表头部的元素，该元素在链表中就已经不存在了 
llen，列表长度
lrem，从头部(left)向尾部(right)操作链表，删除2个值等于a的元素，返回值为实际删除的数量
lrem test 2 a
lindex，根据索引获取值
获取索引值为1(头部的第二个元素)的元素值
lindex test 1
lset
将索引值为1(头部的第二个元素)的元素值设置为新值w
lset test 1 w
ltrim
仅保留索引值0到2之间的3个元素，注意第0个和第2个元素均被保留
ltrim test 0 2 
linsert
在a的前面插入新元素a0
linsert test before a a0
在e的后面插入新元素e2，从返回结果看已经插入成功
linsert test after e e2
在不存在的元素之前或之后插入新元素，该命令操作失败，并返回­1
为不存在的Key插入新元素，该命令操作失败，返回0
rpush
从链表的尾部插入参数中给出的values，插入顺序是从右到左依次插入【看作是从右到左的栈】
rpush test a b c d e
rpushx
键已经存在并且包含5个元素，rpushx命令将执行成功，并将元素e插入到链表的尾部
rpush test e
rpop
从尾部(right)弹出元素，即取出元素
rpop test
rpoplpush
将test的尾部元素弹出，然后插入到test2的头部(原子性的完成这两步操作)
rpoplpush test test2
将source和destination设为同一键，将test中的尾部元素移到其头部
set
没有排序的字符集合，Set集合中不允许出现重复的元素，和List类型相比，Sets之间可以聚合计算操作，如unions并、intersections交和differences差。
sadd
由于该键test之前并不存在，因此参数中的三个成员都被正常插入
sadd test a b c
smembers
查看集合中的元素，从结果可以，输出的顺序和插入顺序无关(无序的)
由于参数中的a在test中已经存在，因此本次操作仅仅插入了d和e两个新成员（不允许重复）
sismember
判断a是否已经存在，返回值为1表示存在
判断w是否已经存在，返回值为0表示不存在
sismember test w
scard
获取集合中元素的数量
srandmember
随机返回一个成员，成员还在集合中
spop
取出一个成员，成员会从集合中删除
srem
从Set中移出b、d和w三个成员，其中f并不存在，因此只有b和d两个成员被移出，返回为2
smove
将a从test移到test2，从结果可以看出移动成功
smove test test2 a
sdiff
获取多个集合之间的不同成员，要注意匹配的规则
先将test和test2进行比较，a、b和d三个成员是两者之间的差异成员，然后再用这个结果继续和
test3进行差异比较，b和d是test3不存在的成员
sdiffstore
将3个集合的差异成员存储到与diffkey关联的Set中，并返回插入的成员数量
sdiffstore difftest test test1 test2
sinter
获取多个集合之间的交集，这三个Set的成员交集只有c
sinter test test1 test2
sinterstore
将3个集合中的交集成员存储到与intertest关联的Set中，并返回交集成员的数量
sinterstore intertest test1 test2 test3
sunion
获取多个集合之间的并集
sunion test1 test2 test3
sunionstore
将3个集合中成员的并集存储到uniontest关联的set中，并返回并集成员的数量
sunionstore uniontest test1 test2 test3
Sorted-Sets
也称为Zset，每一个成员都会有一个分数(score)与之关联，Redis正是通过分数来为集合中的成员进行从小到大的排序（默认）。尽管Sorted­Sets中的成员必须是唯一的，但是分数(score)却是可以重复的。
zadd
添加一个分数为10的成员
zadd test 10 aaa
添加两个分数分别是20和30的两个成员
zadd test 20 bbb 30 ccc
zrange
通过索引获取元素，0表示第一个成员，­1表示最后一个成员。WITHSCORES选项表示返回的结果中包含每个成员及其分数，否则只返回成员
zrange test 0 -1 withscores
zcard
获取test键中成员的数量
zcard test
zrank
获取成员在集合中的索引，索引从0开始
zcount
获取符合指定条件的成员数量，分数满足表达式10 <= score <= 20的成员的数量
zcount test 10 20 
zrem
删除成员aaa和bbb，返回实际删除成员的数量
zrem test aaa bbb
zscore
获取成员ccc的分数。返回值是字符串形式
zscore test ccc
zincrby
将成员ccc的分数增加10，并返回该成员更新后的分数
zincreby test 10 ccc
zrangebyscore
通过分数获取元素，获取分数满足表达式10 <= score <= 20的成员
zrangebyscore test 10 20
inf表示第一个成员，+inf表示最后一个成员，limit后面的参数用于限制返回成员的数量，
limit 2 3，2表示从位置索引(0­-based)等于2的成员开始，取后面3个成员，成员不足就有多少显示多少，类似于MySQL中的limit
zrangebyscore  test -inf +inf limit  2 2
zremrangebyscore
根据分数删除成员，删除分数满足表达式10 <= score <= 20的成员，并返回实际删除的数量
zremrangebyscore test 10 20
zremrangebyrank
根据索引删除成员，删除索引满足表达式0 <= rank <= 1的成员 
zremrangebyrank test 0 1
zrevrange
按索引从高到低的方式获取成员（获取top10：zrevrange test 0 9）
zrevrange test 0 -1 withscores
zrevrangebyscore
按索引从高到低的方式根据分数获取成员，分数满足表达式30 >= score >= 10的成员
zrevrangebyscore test 30 10
limit选项的含义等同于zrangebyscore中的该选项，只是在计算位置时按照相反的顺序计算和获取
zrevrangebyscore  test 40 10 limit 1 2
zrevrank
获取成员aaa在集合中的索引，由于是从高到低的排序，所以aaa的位置是3
zrevrank test aaa 
Hash
hset
给键为test的键设置字段为name，值为jack
hset test name jack
hget
获取键为test，字段为name的值
hget test name
hlen
获取test键的字段数量
hlen test
hexists
判断test键中是否存在字段名为city的字段，由于存在，返回值为1
hexists test city
hdel
删除test键中字段名为age的字段，删除成功返回1
hdel test age
hsetnx
通过hsetnx命令给test添加新字段age，其值为18，因为该字段已经被删除，所以该命令添加成功并返回1
hsetnx test age 18 
hincrby
给test的age字段的值加1，返回加后的结果
hincrby test age 1
hmset
为该键test，一次性设置多个字段，分别是：name=jack，age=18
hmset test  name jack age 18
hmget
获取test键的多个字段，其中city并不存在，因为在返回结果中与该字段对应的值为nil
 hmget test age name city
hgetall
返回test键的所有字段及其值，从结果中可以看出，他们是逐对列出的
hgetall test
hkeys
仅获取test键中所有字段的名字
hkeys test
hvals
仅获取test键中所有字段的值
hvals test
Key操作命令
keys
根据参数中的模式，获取当前数据库中符合该模式的所有key，从输出可以看出，该命令在执行时并不区分与Key关联的Value类型
del
删除一个或多个key
删除了两个Keys
批量删除，其余参数：-h redis所在服务器ip
exists
如果存在，返回整数类型1，否则返回0
查看刚刚删除的Key是否还存在，从返回结果看，name确实已经删除了
move
将当前数据库中的testset键移入到ID为1的数据库中
rename
修改键的名称，将name改名为username，然后获取值只能通过新的键
renamenx
当新名称不存在时才会执行。由于mycity已经存在，因此该命令未能成功执行
ttl
将该键的超时设置为1000秒
通过ttl命令查看还剩多少秒
persist
立刻执行persist命令，该存在超时的键变成持久化的键，即将该Key的超时去掉；-1表示该键已经没有超时了
expire
设置该键的超时被1000秒；用ttl命令看当前还剩下多少秒，从结果中可以看出还剩下991秒
expireat
以 UNIX 时间戳(unix timestamp)格式设置 key 的过期时间
type 查看数据的类型
randomkey
返回数据库中的任意键
flushdb
清空当前打开的数据库，不影响其它数据库
dbsize
返回当前数据库的key的数量
事务
Redis事务中如果有某一条命令执行失败，其后的命令仍然会被继续执行。
multi，标记事务的开始
exec，执行在一个事务内命令队列中的所有命令
discard，回滚事务队列中的所有命令，discard只能在exec前执行
在当前连接上启动一个新的事务















