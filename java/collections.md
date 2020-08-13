# 集合

## LinkedHashMap

`LinkedHashMap` 继承了 `HashMap` 所有的方法，然后通过重写某些方法来实现自身的功能。在 `LinkedHashMap`  中，会将所有的点串联成一个链表，按插入顺序记录顺序记录每一个键值对，另外，`LinkedHashMap` 中也已经实现了LRU缓存的功能，其实现思路是，设置一个 `accessOrder` 的域，如果这个实例域设置为 `true` ，则会在每次访问 `LinkedHashMap` 或者向 `LinkedHashMap` 中插入键值对之后，会将这个键值对放到链表的末尾，如果此时 `LinkedHashMap` 中的键值对数量超过了缓存的阈值，则会将链表中的第一个键值对删除，这就是“最少最近原则”的应用。