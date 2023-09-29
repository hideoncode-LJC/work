

Introduction to Redis lists

# list intro

>Redis list的介绍

Redis lists are linked lists of string values. Redis lists are frequently used to: Implement stacks and queues、Build queue management for background worker systems.

>redis列表是链接起来的字符串类型。redis列表经常被用来实现栈、队列，为后台用户系统构建队列管理系统。


# Examples

+ queue，`LPUSH` `RPOP`
+ stack，`LPUSH` `LPOP`
+ 查看列表的长度
+ 原子的拿到一个元素并且将它压入另外一个
+

To limit the length of a list you can call [`LTRIM`](https://redis.io/commands/ltrim):？？？？？？？？？？？？？？/

# What are Lists

To explain the List data type it's better to start with a little bit of theory, as the term _List_ is often used in an improper way by information technology folks.


为了更好的解释列表数据类型，最好从一点理论开始。因为List


But the properties of a List implemented using an Array are very different from the properties of a List implemented using a _Linked List_.

由数组实现的列表的属性和有链表实现的列表的属性完全不同。

Redis lists are implemented via Linked Lists. This means that even if you have millions of elements inside a list, the operation of adding a new element in the head or in the tail of the list is performed _in constant time_. The speed of adding a new element with the [`LPUSH`](https://redis.io/commands/lpush) command to the head of a list with ten elements is the same as adding an element to the head of list with 10 million elements.

redis列表是由链表实现的，因此，插入元素快。

What's the downside? Accessing an element _by index_ is very fast in lists implemented with an Array (constant time indexed access) and not so fast in lists implemented by linked lists (where the operation requires an amount of work proportional to the index of the accessed element).

缺点，按索引访问元素不够快。


Redis Lists are implemented with linked lists because for a database system it is crucial to be able to add elements to a very long list in a very fast way.

Redis列表是由链表实现的。对于一个数据库来说，能够快速将数据添加到一个长的列表中是很重要的。

Another strong advantage, as you'll see in a moment, is that Redis Lists can be taken at constant length in constant time.

另外一个存储优势，可以在常数时间取得一段长度的列表。？？



When fast access to the middle of a large collection of elements is important, there is a different data structure that can be used, called sorted sets.

当快速访问一个包含大量元素的集合的中间值是很重要的，有一个不同的数据结构可以被使用。ZSET。

Sorted sets are covered in the [Sorted sets](https://redis.io/docs/data-types/sorted-sets) tutorial page.

>有序集合



















Automatic creation and removal of keys

So far in our examples we never had to create empty lists before pushing elements, or removing empty lists when they no longer have elements inside.

>目前，在我们的样例中，我们不用在往列表添加元素之前创建空的列表。同样，当列表中不含有元素时，我们也不需要去删除这个列表。

It is Redis' responsibility to delete keys when lists are left empty, or to create an empty list if the key does not exist and we are trying to add elements to it

>这是Redis的责任，当列表中没有元素时删除key，当往空列表中加入元素时创建新的列表。

**自动创建的三条规则**

When we add an element to an aggregate data type, if the target key does not exist, an empty aggregate data type is created before adding the element.

>当我们向一个集成类型添加元素时，如果目标key不存在，则会先创建一个集合体类型，然后再添加元素。如果目标key的类型不为我们需要的类型，会报错。

When we remove elements from an aggregate data type, if the value remains empty, the key is automatically destroyed. The Stream data type is the only exception to this rule.

>当我们从一个集合体类型中移除一个元素时，如果该集合为空，则会销毁该集合。Stream类型不遵守这个规则。

Calling a read-only command such as [`LLEN`](https://redis.io/commands/llen) (which returns the length of the list), or a write command removing elements, with an empty key, always produces the same result as if the key is holding an empty aggregate type of the type the command expects to find.

>调用一个只读函数或者使用空键删除元素的写函数，总会产生相同的结果。就好像该键持有一个我们期望的聚合类型一样。？？？？？？？？？？？/




# First steps with Redis Lists



# Limits

The max length of a Redis list is 2^32 - 1 (4,294,967,295) elements.



# Performance

List operations that access its head or tail are O(1), which means they're highly efficient.

>处理列表头、尾的时间复杂度为O(1)，非常高效。

However, commands that manipulate elements within a list are usually O(n). Examples of these include [`LINDEX`](https://redis.io/commands/lindex), [`LINSERT`](https://redis.io/commands/linsert), and [`LSET`](https://redis.io/commands/lset).

>但是，操作一个列表中的元素的时间复杂度通常是O(n)

Exercise caution when running these commands, mainly when operating on large lists.

>执行O(n)命令时，对于大容量的list



# Alternatives

Consider [Redis streams](https://redis.io/docs/data-types/streams) as an alternative to lists when you need to store and process an indeterminate series of events.

>考虑redis stream类型是一个可供选择的方式当你需要存储或者处理一系列不确定性的事件。





