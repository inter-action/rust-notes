

* Map
    * collections::btree_map::BTreeMap
        基于BTree的Map，key是排序过的。
        Lookup-array structure, based on hashCode(), equals() implementations, O(1) runtime complexity for inserting and searching, unsorted

    * HashMap
        基于hash的，key没有顺序。
        TreeMap: Tree structure, based on compareTo() implementation, O(log(N)) runtime complexity for inserting and searching, sorted


* collections::vec_deque
    双向链表？