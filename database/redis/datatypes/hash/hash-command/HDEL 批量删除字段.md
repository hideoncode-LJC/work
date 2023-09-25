# Syntax

```shell
HDEL key field [field ...]
```

>Removes the specified fields from the hash stored at `key`. Specified fields that do not exist within this hash are ignored. If `key` does not exist, it is treated as an empty hash and this command returns `0`.

+ 移除存储在`hash`中指定`key`特定的字段。
+ 如果字段不存在，则会忽略该字段。
+ 如果key不存在，则会返回0。

# Return

+ 返回成功删除的字段