
# ZRANGE

## Syntax

```shell
ZRANGE key start stop 
[BYSCORE | BYLEX] 
[REV] 
[LIMIT offset count]
[WITHSCORES]
```

+ **Time complexity**

>Returns the specified range of elements in the sorted set stored at `<key>`.

+ 返回 key 对应的已排序集合中在确定范围内的元素。

>`ZRANGE` can perform different types of range queries: by index (rank), by the score, or by lexicographical order.

+ 可以根据rank、score、字典序进行不同范围的类型查询。

## Common behavior and options

>The order of elements is from the lowest to the highest score. Elements with the same score are ordered lexicographically.

+ 元素的顺序是根据分数从低到高。
+ 相同分数的元素是根据字典序排序。

>The optional `REV` argument reverses the ordering, so elements are ordered from highest to lowest score, and score ties are resolved by reverse lexicographical ordering.

+ 分数从高到低，字段序也是反的。

>The optional `LIMIT` argument can be used to obtain a sub-range from the matching elements (similar to _SELECT LIMIT offset, count_ in SQL). A negative `<count>` returns all elements from the `<offset>`. Keep in mind that if `<offset>` is large, the sorted set needs to be traversed for `<offset>` elements before getting to the elements to return, which can add up to O(N) time complexity.

+ 可供选择的`LIMIT`参数可以被用来获得一个子序列从相匹配的元素中。类似与`SQL`语句`SELECT LIMIT offset, count in SQL`
+ 