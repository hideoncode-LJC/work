# SET 

> note that [`SET`](https://redis.io/commands/set) will replace any existing value already stored into the key, in the case that the key already exists, even if the key is associated with a non-string value. So [`SET`](https://redis.io/commands/set) performs an assignment.

注意，`SET command`会替换已经存在的`key-value`,

> Values can be strings (including binary data) of every kind, for instance you can store a jpeg image inside a value. A value can't be bigger than 512 MB.

字符串可以是任何字符串类型，包括二进制数据，字符串长度不能超过512MB。

## Syntax

```redis
SET key value 
[NX | XX] 
[GET] 
[EX seconds | PX milliseconds | EXAT unix-time-seconds | PXAT unix-time-milliseconds | KEEPTTL]
```

>Set `key` to hold the string `value`. If `key` already holds a value, it is overwritten, regardless of its type.

+ 设置`key`用来保存string类型。
+ 如果已经有`value`对应`Key`了，则会覆盖旧的值，无论该值是什么类型。

>Any previous time to live associated with the key is discarded on successful `SET` operation.

+ 当`SET`操作成功后，任何之前的与`key`一块生存的时间都会被丢弃。

### Options

**[nx | xx]**

+ nx，当`key`不存在时才设置`key`。
+ xx，当`key`已经存在时才设置`key`。

**[GET]**

+ 设置新值的同时返回旧值。
	1.  当`key`不存在时返回`nil`。
	2.  当`key`存在时且旧值为`string`类型时返回旧的`string`。
	3.  当`key`存在时且旧值不为`string`类型时返回错误并且终止`set`。

**[EX seconds | PX milliseconds |EXAT unix-time-seconds | PXAT unix-time-milliseconds | KEEPTTL]**

+ EX，设置精确的过期时间，以秒为单位。
+ PX，设置精确的过期时间，以毫秒为单位。
+ EXAT，设置精确的过期UNIX时间，以秒为单位。
+ PXAT，设置精确的过期UNIX时间，以毫秒为单位。
+ KEEPTTL，保留与该键相关的过期时间。

> Note: Since the `SET` command options can replace [`SETNX`](https://redis.io/commands/setnx), [`SETEX`](https://redis.io/commands/setex), [`PSETEX`](https://redis.io/commands/psetex), [`GETSET`](https://redis.io/commands/getset), it is possible that in future versions of Redis these commands will be deprecated and finally removed.

注意，这些选项和`SETNX` `SETEX` `PSETEX` `GETSET` 命令作用一样。

### Return

**不含GET选项**

+ 如果`SET`执行成功，会返回`OK`。
+ 如果`NX` `XX`不符合条件，会导致`SET`执行失败，返回`nil`。

**含有GET选项**

> 当`SET`命令含有`GET`选项时，返回值和`SET`是否执行成功无关。

+ 如果`key`存在，返回旧的`value`值。
+ 如果`key`不存在，返回`nil` 。