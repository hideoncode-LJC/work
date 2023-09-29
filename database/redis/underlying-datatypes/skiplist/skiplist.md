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



**往跳表中插入元素**

```c
/* Insert a new node in the skiplist. Assumes the element does not already
 * exist (up to the caller to enforce that). The skiplist takes ownership
 * of the passed SDS string 'ele'. */
zskiplistNode *zslInsert(zskiplist *zsl, double score, sds ele) {
    // 得到插入的节点，便于断链接链
    zskiplistNode *update[ZSKIPLIST_MAXLEVEL], *x;
    // 便于更新span属性
    unsigned long rank[ZSKIPLIST_MAXLEVEL];
    int i, level;

    // c语言宏定义 判断score的类型 是否是 not a number
    serverAssert(!isnan(score));
    // 获取跳表的头节点
    x = zsl->header;
    // 从最上面一层开始遍历
    for (i = zsl->level-1; i >= 0; i--) {
        /* store rank that is crossed to reach the insert position */
        rank[i] = i == (zsl->level-1) ? 0 : rank[i+1];
        /*
        找到该score的位置
        */
        while (x->level[i].forward && (x->level[i].forward->score < score || (x->level[i].forward->score == score && sdscmp(x->level[i].forward->ele,ele) < 0)))
        {
            rank[i] += x->level[i].span;
            x = x->level[i].forward;
        }
        update[i] = x;
    }
    /* we assume the element is not already inside, since we allow duplicated
     * scores, reinserting the same element should never happen since the
     * caller of zslInsert() should test in the hash table if the element is
     * already inside or not. */

    // 随机数决定是否需要增加跳表的层数
    level = zslRandomLevel();
    if (level > zsl->level) {
        for (i = zsl->level; i < level; i++) { 
            rank[i] = 0;
            update[i] = zsl->header;
            update[i]->level[i].span = zsl->length;
        }
        zsl->level = level;
    }
    // 创建新节点
    x = zslCreateNode(level,score,ele);
    for (i = 0; i < level; i++) {
        x->level[i].forward = update[i]->level[i].forward;
        update[i]->level[i].forward = x;

        /* update span covered by update[i] as x is inserted here */
        x->level[i].span = update[i]->level[i].span - (rank[0] - rank[i]);
        update[i]->level[i].span = (rank[0] - rank[i]) + 1;
    }

    /* increment span for untouched levels */
    for (i = level; i < zsl->level; i++) {
        update[i]->level[i].span++;
    }

    x->backward = (update[0] == zsl->header) ? NULL : update[0];
    if (x->level[0].forward)
        x->level[0].forward->backward = x;
    else
        zsl->tail = x;
    zsl->length++;
    return x;
}

```


