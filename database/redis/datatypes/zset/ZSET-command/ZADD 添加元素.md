# Syntax

```shell
ZADD key 
[NX | XX] 
[GT | LT] 
[CH] 
[INCR] 
score member [score member ...]
```

+ Time complexity，`O(log(N))`，对每个`score-member`字段来说，N是插入前`ZSET`中元素的个数。

>Adds all the specified members with the specified scores to the sorted set stored at `key`. It is possible to specify multiple score / member pairs. If a specified member is already a member of the sorted set, the score is updated and the element reinserted at the right position to ensure the correct ordering.

+ 插入一个或者多个`score-member`对。
+ 如果一个member已经存在，则会更新该member对应的score，并且会重新排序。

>If `key` does not exist, a new sorted set with the specified members as sole members is created, like if the sorted set was empty. If the key exists but does not hold a sorted set, an error is returned.

# ZADD options

>ZADD supports a list of options, specified after the name of the key and before the first score argument.  Options are:

+ **XX**，只更新存在的元素，不增加新的元素。
+ **NX**，只添加新的元素，不更新元素。
+ **LT**，当新的`score`小于当前的`score`，更新该元素。不阻止添加新的元素。
+ **GT**，当新的`score`大于当前的`score`，更新该元素。不阻止添加新的元素。
+ **CH**，


# Return

>

