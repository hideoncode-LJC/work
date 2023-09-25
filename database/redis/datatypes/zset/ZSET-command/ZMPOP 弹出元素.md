
> 弹出元素

+ ZMPOP
+ BZPOP
+ ZMPOPMIN
+ BZPOPMIN
+ ZMPOPMAX
+ BZPOPMAX

# ZMPOP

>Zset multiply pop 

## Syntax

```shell
ZMPOP numkeys key [key ...] 
<MIN | MAX> 
[COUNT count]
```

+ **Time complexity**，where K is the number of provided keys, N being the number of elements in the sorted set, and M being the number of elements popped.

>Pops one or more elements, that are member-score pairs, from the first non-empty sorted set in the provided list of key names.

+ 从第一个非空Zset中弹出一个或者若干个member-score对。

## Return

>Array reply:
>A `nil` when no element could be popped.
>A two-element array with the first element being the name of the key from which elements were popped, and the second element is an array of the popped elements. Every entry in the elements array is also an array that contains the member and its score.

**返回类型为数组类型**

+ 当Zset中没元素时返回nil