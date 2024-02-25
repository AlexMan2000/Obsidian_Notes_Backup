# Serialization
> [!concept]
> This project serialize the records to bytes in memory instead of serializing to file in file system, like in [P2102__Gitlet](../../../Data_Structures_Algorithms/Data_Structures/CS61B/16_Software_Projects/P2102__Gitlet.md).
> ![](Project2_B+_Tree(sp24).assets/image-20240212101728640.png)




# Task 1: LeafNode::fromBytes
> [!important]
> This deserializing method depends on how the LeafNode is serialized, so we have to take a look at `LeafNode::toBytes()`

> [!code]
```java
/**  
 * Loads a leaf node from page `pageNum`.
 */
public static LeafNode fromBytes(BPlusTreeMetadata metadata, BufferManager bufferManager,  LockContext treeContext, long pageNum) { 

    Page page = bufferManager.fetchPage(treeContext, pageNum);  
    Buffer buf = page.getBuffer();  
  
    byte nodeType = buf.get();  
    // 1 is leafnode, 0 is innernode
    assert(nodeType == (byte) 1);  
  
  
    // This is a factory creator method.  
    Optional<Long> rightSiblingPointer = Optional.of(buf.getLong());  
  
    List<DataBox> keys = new ArrayList<>();  
    List<RecordId> rids = new ArrayList<>();  
  
  
    int size = buf.getInt();  
    for (int i = 0; i < size; ++i) {  
        keys.add(DataBox.fromBytes(buf, metadata.getKeySchema()));  
        rids.add(RecordId.fromBytes(buf));  
    }  
    return new LeafNode(metadata, bufferManager, page, keys, rids, rightSiblingPointer, treeContext);  
}
```



# Task 2: get, getLeftmostLeaf, put, remove
> [!task]
> ![](Project2_B+_Tree(sp24).assets/image-20240225090438770.png)
> Since B+ Tree is a recursive data structure, the method in different class should be different.





> [!concept]
> 



# Task 3: Scans




# Task 4: Bulk Load



