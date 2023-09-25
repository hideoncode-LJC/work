
# ZRANK

## Syntax

```shell
ZRANK key member [WITHSCORE]
```

+ **Time complexity**，O(log(N))

>Returns the rank of `member` in the sorted set stored at `key`, with the scores ordered from low to high.

+ 返回存储在Sorted Set中对应key的member的排序，按照分数从低到高进行排序。

>The rank (or index) is 0-based, which means that the member with the lowest score has rank 0.

+ 排名or索引是从0开始，分数最低的member的排名为0。

>The optional WITHSCORE argument supplements the command's reply with the score of the element returned.

+ 可供选择WITHSCORE参数补充了命令的回复用返回元素的分数。

## Return

**如果member存在**

+ 使用WITHSCORE参数，返回数组，包括member和score。
+ 不是用WITHSCORE参数，返回整数，member的排名。

**如果member不存在或者key不存在**

+ 使用WITHSCORE参数，返回数组，nil。
+ 不使用WITHSCORE参数，返回字符串，nil。

## go-redis调用

```go
func (c cmdable) ZRank(ctx context.Context, key, member string) *IntCmd {
    //声明一个cmd，用作传入参数和接收返回结果。
    cmd := NewIntCmd(ctx, "zrank", key, member)
    // 执行redis命令，将返回结果放入cmd
    _ = c(ctx, cmd)
    // 返回结果集
    return cmd
}

type IntCmd struct {
	baseCmd
    // val用作接受返回值，返回值为整型时使用该cmd。
	val int64
}

func (c cmdable) ZRankWithScore(ctx context.Context, key, member string) *RankWithScoreCmd {
	cmd := NewRankWithScoreCmd(ctx, "zrank", key, member, "withscore")
	_ = c(ctx, cmd)
	return cmd
}

type RankWithScoreCmd struct {
	baseCmd
	val RankScore
}

type RankScore struct {
	Rank  int64
	Score float64
}

```

# ZRERANK

