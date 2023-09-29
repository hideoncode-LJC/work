Introduction to Redis strings.

# strings 简介

>Redis字符串类型的介绍

Redis strings store sequences of bytes, including text, serialized objects, and binary arrays.

>Redis strings类型存储字节序列。包括文本、序列化对象(JSON)、二进制数组。

As such, strings are the simplest type of value you can associate with a Redis key.

>因此，redis字符串类型是最简单的可以和redis键联系起来的值类型。

They're often used for caching, but they support additional functionality that lets you implement counters and perform bitwise operations, too.

>它们经常被用于缓存，但是它们也支持额外的函数，可以让你实现计数器和运行二进制操作。

Since Redis keys are strings, when we use the string type as a value too, we are mapping a string to another string.

>因为redis键是字符串类型，所以当我们使用字符串作为值得时候，我们可以把一个字符串映射到另外一个字符串上。

The string data type is useful for a number of use cases, like caching HTML fragments or pages.

>redis字符串数据类型对大量的使用用例是有用的。比如缓存HTML片段或者页面。

As you can see using the [`SET`](https://redis.io/commands/set) and the [`GET`](https://redis.io/commands/get) commands are the way we set and retrieve a string value.

>正如你所看到的，使用SET、GET命令是我们设置和检索值的方式。

Note that [`SET`](https://redis.io/commands/set) will replace any existing value already stored into the key, in the case that the key already exists, even if the key is associated with a non-string value.So [`SET`](https://redis.io/commands/set) performs an assignment.

>注意，SET方法会替换已经存在的k-v对，即使key对应的value类型不是字符串类型。所以SET命令执行赋值操作。

Values can be strings (including binary data) of every kind, for instance you can store a jpeg image inside a value. A value can't be bigger than 512 MB.

>字符串值可以是任何类型的。例如你可以存储一个图片到字符串类型中，但是一个字符串的长度不能操作512MB。

The [`SET`](https://redis.io/commands/set) command has interesting options, that are provided as additional arguments.

>SET命令有选项可以被提供，当作额外的参数。

For example, I may ask [`SET`](https://redis.io/commands/set) to fail if the key already exists, or the opposite, that it only succeed if the key already exists:

>例如，当key已经存在时，可以让SET命令失败。或者只有当key存在时，set才会执行成功。

There are a number of other commands for operating on strings.

>有大量的其他命令可以用来操作string类型。

For example the [`GETSET`](https://redis.io/commands/getset) command sets a key to a new value, returning the old value as the result.

>例如，你可以使用GETSET命令设置一个新值并且返回旧值作为结果。

You can use this command, for example, if you have a system that increments a Redis key using [`INCR`](https://redis.io/commands/incr) every time your web site receives a new visitor.

>如果你有一个系统需要记录每次访问网站，你可以使用INCR命令。

You may want to collect this information once every hour, without losing a single increment.

>你可能想要每个小时收集一次信息，不丢失增量。

You can [`GETSET`](https://redis.io/commands/getset) the key, assigning it the new value of "0" and reading the old value back.

>你可以使用GETSET命令赋新的值，得到旧的值。

The ability to set or retrieve the value of multiple keys in a single command is also useful for reduced latency.

>在一条命令中设置或者检索多个k-v的能力也是有用的，对于减少延迟来说。


# strings 应用

## 计数器

Even if strings are the basic values of Redis, there are interesting operations you can perform with them.

>虽然字符串类型是redis中最基础的类型，但是有很多有趣的操作你可以使用string来实现。

The [`INCR`](https://redis.io/commands/incr) command parses the string value as an integer, increments it by one, and finally sets the obtained value as the new value.

>INCR命令解析字符串类型作为整数，对其增加一，并将获得的值作为新值。

There are other similar commands like [`INCRBY`](https://redis.io/commands/incrby), [`DECR`](https://redis.io/commands/decr) and [`DECRBY`](https://redis.io/commands/decrby). Internally it's always the same command, acting in a slightly different way.

>有很多类似的命令。它们在内部是相似的命令，执行方式稍微不同。

What does it mean that INCR is atomic? That even multiple clients issuing INCR against the same key will never enter into a race condition. For instance, it will never happen that client 1 reads "10", client 2 reads "10" at the same time, both increment to 11, and set the new value to 11. The final value will always be 12 and the read-increment-set operation is performed while all the other clients are not executing a command at the same time.

>INCR是原子的。


# Limits

By default, a single Redis string can be a maximum of 512 MB.

>默认情况下，一个单独的redis字符串类型的最大为512MB




# Bitwise operations

To perform bitwise operations on a string, see the [bitmaps data type](https://redis.io/docs/data-types/bitmaps) docs.

>在字符串上执行二进制操作时，看bitmap类型。


# Performance

Most string operations are O(1), which means they're highly efficient.

>大多数字符串命令是O(1)。意味着这些命令很高效。

However, be careful with the [`SUBSTR`](https://redis.io/commands/substr), [`GETRANGE`](https://redis.io/commands/getrange), and [`SETRANGE`](https://redis.io/commands/setrange) commands, which can be O(n).

>但是注意这些命令，它们的时间复杂度是O(n)

These random-access string commands may cause performance issues when dealing with large strings.

>随机访问kv对的命令在处理大量数据时可能会出现问题。


# Alternatives

If you're storing structured data as a serialized string, you may also want to consider Redis [hashes](https://redis.io/docs/data-types/hashes) or [JSON](https://redis.io/docs/stack/json).

>当你存储结构化数据作为一个序列化字符串时，你可以考虑hash或者JSON。

