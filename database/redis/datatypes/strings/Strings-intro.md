> Redis strings introduction

# Strings intro

Redis存储了字节序列(sequences of bytes)，包括
+ 文本
+ 序列化对象 serialized objects
+ 二进制数组
`Strings`是最简单的可以和`redis key`联系起来的值类型(type of value)。它们通常被用于缓存`caching`，但是它们支持附加功能，比如实现计数功能、按位操作。

> Since Redis keys are strings, when we use the string type as a value too, we are mapping a string to another string.

由于 Redis 键是字符串，因此当我们也将字符串类型用作值时，我们将一个字符串映射到另一个字符串。???

Strings对许多用例(use case)都有用。例如
+ HTTP Fragment
+ HTTP page

# Strings Command

