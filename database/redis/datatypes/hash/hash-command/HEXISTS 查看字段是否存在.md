# Syntax

```shell
HEXISTS key field
```

+ O(1)

# Return

+ 返回整数
	+ 如果该字段存在，返回`1`
	+ 字段不存在或者`key`不存在，都会返回`0`