>decrement 

# Syntax

```shell
DECR key [number]
```

>Decrements the number stored at `key` by one. If the key does not exist, it is set to `0` before performing the operation. An error is returned if the key contains a value of the wrong type or contains a string that can not be represented as integer. This operation is limited to **64 bit signed integers**.

+ 将存储在`key`中的值加`1 or number`
+ 如果`key`不存在，则会把`value`在操作执行之前设置为0。`SET key 1 or number` 
+ 如果`value`中包含错误类型或者包含一个字符串不能被表示成整数，则会返回错误。
+ 这个操作仅限于64位有符号整数。

# Return

经过增长后的值

