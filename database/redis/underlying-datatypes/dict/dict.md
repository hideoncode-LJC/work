# dict

## dict struct design

```go
type dictEntry struct {
    // key
    key *any

    // value
    union {
        val *any
        u64 uint64
        s64 int64
        d float64
    }
    // next dictEntry node
    next *dictEntry
}

type dictht struct {    
    // 哈希表数组
    table **dictEntry
    // 哈希表大小
    size uint64
    // 哈希码大小掩码，用于计算索引值
    sizemask uint64
    // 该哈希表已有的节点数量
    used uint64
}
```

## hash confusion

哈希桶？？？

## link hash

## rehash

## 渐进式rehash


## dict feature

