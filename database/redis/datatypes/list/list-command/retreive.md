+ LINDEX









# LINDEX

## syntax

```shell
LINDEX key index
```

+ O(N) 
+ N 取决于 Index的大小
+ 访问头元素或者尾元素 O(1)

## return

+ 返回字符串
+ value the key hold is not list, return error，其他情况返回字符串。

# LLEN

## syntax

```shell
LLen key
```

+ O(1)

## return

+ 返回整数
+ key不存在返回0
+ key存在但是不是list 返回 error
+ 其他情况返回list中元素的个数

# LPOS

