Introduction to Redis hashes

>


>Redis hashes are record types structured as collections of field-value pairs. You can use hashes to represent basic objects and to store groupings of counters, among other things.

+ `Redis hash type`是用来记录结构化类型(`field-value`对的集合)。
+ 可以用`hash`类型表示基础对象、计数器组等。

>While hashes are handy to represent _objects_, actually the number of fields you can put inside a hash has no practical limits (other than available memory), so you can use hashes in many different ways inside your application.

+ 因为`Hash`用来表示对象是有用的，实际上`field`的数量没有真是的限制。所以你可以在你的应用中多种方式使用`Hash`。

>It is worth noting that small hashes (i.e., a few elements with small values) are encoded in special way in memory that make them very memory efficient.

+ 值得注意的是一些小的`hash`被用一种特殊方式编码，可以使内存更有效。

>Every hash can store up to 4,294,967,295 (2^32 - 1) field-value pairs. In practice, your hashes are limited only by the overall memory on the VMs hosting your Redis deployment.

+ `field`的限制仅被`VM`总体内存限制。