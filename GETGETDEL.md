# GET Syntax

```go
GET key
```

>Get the value of `key`. If the key does not exist the special value `nil` is returned. An error is returned if the value stored at `key` is not a string, because `GET` only handles string values.

+ 获取`value`。
+ 当`key`不存在时返回`nil`。
+ 当`key`存在时，为`string`类型则返回值，不为`string`类型返回`error`，`GET`只处理`string`类型的值。

# GETDEL



# GETEX


# GETRANGE

# GETSET

#