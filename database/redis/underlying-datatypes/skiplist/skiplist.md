# zSkipList

## zSkipList结构

```go
type struct zset {
    // 哈希表
    dict *dict
    // 跳表 
    zsl *zskiplist
}
```

+ 哈希表可以实现高效的单点查询
+ 跳表可以实现高效的范围查询
+ zset更新数据时，哈希表和跳表都会更新。
+ 


## 跳表结构设计

```go
type zskipListLevel struct {
    // 前向指针
    forward *zskiplistNode
    // 该层次每个节点之间的跨度
    span uint64
}

type zskiplistNode struct {
    // Zset 对象的元素值
    // string 类型使用 sds存储
    ele sds
    // 元素的权重
    score float64
    // 后向指针 从尾部指向头部
    backward *zskiplistNode
    // level 数组
    level []zskiplistLevel
}

type zskiplist struct {
    // 头节点、尾节点
    header, tail *zskiplistNode
    // 跳表的长度
    length uint64
    // 层次
    level int
}
```

**跳表结构特点**

+ 跳表的头尾节点，可以在O(1)复杂度内访问跳表头节点、尾节点；
+ 跳表的长度，便于在O(1)复杂度获得跳表节点的数量；
+ 跳表的最大层数，便于在O(1)时间复杂度获取跳表中层高最大的那个节点的层数量；？？

