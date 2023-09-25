
>A Redis sorted set is a collection of unique strings (members) ordered by an associated score.

+ 一个`ZSET`是一个根据相关分数排序的唯一字段的集合。

>When more than one string has the same score, the strings are ordered lexicographically.

+ 当有两个字段拥有同样的score时，字段会按照字典序排序。

>Leaderboards. For example, you can use sorted sets to easily maintain ordered lists of the highest scores in a massive online game.

+ 游戏排行榜

>- Rate limiters. In particular, you can use a sorted set to build a sliding-window rate limiter to prevent excessive API requests.

+ 速率限制器。构建滑动窗口来避免过多的`API`请求。

>You can think of sorted sets as a mix between a Set and a Hash. Like sets, sorted sets are composed of unique, non-repeating string elements, so in some sense a sorted set is a set as well.

+ 你可以认为`ZSET`是一个`SET`和`HASH`之间的混合。
+ `ZSET`是由唯一的、不重复的字符串元素组成，所以在某种意义上，`ZSET`也是`SET`。

>However while elements inside sets are not ordered, every element in a sorted set is associated with a floating point value, called the score (this is why the type is also similar to a hash, since every element is mapped to a value).

+ 然而，虽然集合中的元素不是有序的，但是每一个在`ZSET`集合中的元素都和一个浮点数分数值有关系，这个值叫做`SCORE`。这也是为什么`ZSET`像`Hash`，每一个元素都根据分数映射到值上。

>Moreover, elements in a sorted set are _taken in order_ (so they are not ordered on request, order is a peculiarity of the data structure used to represent sorted sets). They are ordered according to the following rule:

- If B and A are two elements with a different score, then A > B if A.score is > B.score.
- If B and A have exactly the same score, then A > B if the A string is lexicographically greater than the B string. B and A strings can't be equal since sorted sets only have unique elements.