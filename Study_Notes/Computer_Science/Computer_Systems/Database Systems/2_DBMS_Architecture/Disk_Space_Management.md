> Note 2 Discussion 2
# Resource Management
## Overview
> [!overview]
> ![](Disk_Space_Management.assets/image-20240123235623110.png)


## Disk
> [!concept]
> ![](Disk_Space_Management.assets/image-20240123235250232.png)![](Disk_Space_Management.assets/image-20240123235255755.png)


## Flash(SSD)
> [!concept]
> ![](Disk_Space_Management.assets/image-20240123235319356.png)![](Disk_Space_Management.assets/image-20240123235325218.png)
> **Key Takeaway: **For SSD, read is fast while write is relatively slow. The reason is that when writing to the SSD, we have to make sure that the same cell won't be erased too many times. So SSD manufacturers have come up with powerful algorithm to reallocate the data to prevent cell from fading away too quickly(wear leveling).

> [!quiz] True or False
> Writing to an SSD drive is more costly than reading from an SSD drive. 
> **True**, a write can involve reorganization to avoid uneven wear and tear (wear leveling).










## Block Level Storage
> [!concept]
> ![](Disk_Space_Management.assets/image-20240123235553087.png)![](Disk_Space_Management.assets/image-20240123235559082.png)

> [!quiz] True or False
> When querying for a 16 byte record, exactly 16 bytes of data is read from disk.
> 
> **False**, an entire page of data is read from disk.




# Cost Model
## I/O
> [!concept]
> There are two main types of files: Heap Files and Sorted Files. For each relation, the database chooses which file type to use based on the I/O cost of the relation’s access pattern. 
> 
> **1 I/O is equivalent to 1 page read from disk or 1 page write to disk**, and I/O calculations are made for each file type based on the insert, delete, and scan operations in its access pattern. 
> 
> The file type that incurs less I/O cost is chosen.


## Cost Model for Analysis
> [!concept]
> ![](Disk_Space_Management.assets/image-20240124084241558.png)![](Disk_Space_Management.assets/image-20240124084217095.png)![](Disk_Space_Management.assets/image-20240124084231686.png)

> [!important] Important Note
> When we want to write record to pages, we have to first read it to the main memory(RAM) so that the CPU can run the program and decide how to insert the record to the page. Then after insertion, we have to write the page back to the disk. Thus:
> 1. Check if the page has free space only involves read I/O.
> 2. Update records in a page involves both read and write I/O.


# Pages in Files - File Structures
## Overview
> [!overview]
> ![](Disk_Space_Management.assets/image-20240124091513228.png)![](Disk_Space_Management.assets/image-20240124091502996.png)





## Heap Files
> [!def]
> A heap file is a file type with no particular ordering of pages or of the records on pages and has two main implementations.
> ![](Disk_Space_Management.assets/image-20240124091443308.png)
> - In a heap file, new records are placed in the first available space in the file. This "first available space" could be an empty space left by a previously deleted record or at the end of the file if no such spaces are available.
> - This method is typically fast for insertions since it doesn't require the records to be ordered in any particular way.
> - Unlike indexed files or other organized storage methods (like clustered files), heap files do not store records based on any key or other criteria. There's no inherent sorting or ordering of the data by values.
> - Because of this, when records are retrieved (e.g., during a full table scan), they appear in the order they are found in the file, which corresponds to the order of insertion unless records have been deleted and their spaces reused.

> [!quiz] True or False
> In a heap file, all pages must be filled to capacity except the last page.
> 
> **False,** there is no such requirement.



### Ordering Myth
> [!important]
> It's a common misconception that heap files result in a "random" order of records each time they are read from disk. In reality, the order of records in a heap file remains consistent between reads unless:
> - New records are added.
> - Existing records are deleted, potentially causing new records to occupy these freed spaces.
> - The file is explicitly reorganized or compacted by the database system.
> 
> Suppose you have a heap-organized file storing customer records with attributes like CustomerID, Name, and Address. When new customer records are added:
> - They are placed in the next available space.
> - If a customer record is deleted, its space becomes available for future insertions.
> - When scanning the table to list all customers, the result will reflect the physical order in the file at the time of the scan, which might not match any logical or sorted order by CustomerID or Name.


### List Implementation
#### Memory Layout
> [!concept] Overview Layout
> ![](Disk_Space_Management.assets/image-20240124082059200.png)
> In this implementation, we have:
> 1. A header page that stores two pointers to two doubly linked list. One to the start of full-page list where all the pages are full(cannot hold more records).
> 2. A **full-page linked list**. All the pages here are full.
> 3. A **free-page linked list**. All the pages here have free space for more records.
> 4. Each page(except for header page) maintains:
> 	1. Two pointers, one to the previous, one to the next page. 
> 	2. Free space tracker, could be a private member field, indicating whether there is free space on the page(in bytes).
> 	3. Records.


#### Look up Free Page
> [!concept] Lookup Free Page
> Read the header page first, then traverse the free page list to find the desired page.
> 

> [!example] Sp18 Vitamin 2 Q2
> ![](Disk_Space_Management.assets/image-20240129092258215.png)



#### Insert Records
> [!concept] Insertion
> When we insert a new record, we will follow the procedures as follow: 
> 1. Since we don't have any ordering in our file structure(heap files), we have to traverse over the free-page **list** to find the first page with enough free space. This step involves **reading(I/O)** from the pages to get the free space information from page header/footer.
> 2. Once we find the appropriate page, **write(I/O)** the record to the page and update the free space information. Now we have two scenarios:
> 	1. If after insertion, the page is full, they are moved from the free space portion to the front of the full pages portion of the linked list. We move it to the front(**read and write I/O**), so we don’t have to traverse the entire full pages portion to append it. An alternative is to keep a pointer to the end of this list in the header page. The details of which implementation we use aren’t important for this course.
> 	2. If after insertion, the page still has free space, then we are done. 
> 3. If we cannot find a free page, we will have to ask for more from the disk and insert the allocated free page at the front of free-page list.


#### Delete Records
> [!concept] Deletion
> When we delete a new record, we will follow the procedures as follow:
> 1. Since we don't have any ordering in our file structure(heap files), we have to traverse over the free-page **list** to find the first page with enough free space. This step involves **reading(I/O)** from the pages to get the free space information from page header/footer.
> 2. Once we find the target page, **delete(I/O)** the record from the page and update the free space information. Now we have two scenarios:
> 	1. If the page is initially full, then after deletion(**write I/O**), the page has free space, so they are moved from the full space portion to the front of the free pages portion of the linked list. We move it to the front(**read and write I/O**), so we don’t have to traverse the entire full pages portion to append it. An alternative is to keep a pointer to the end of this list in the header page. The details of which implementation we use aren’t important for this course.
> 	2. If the page is initially at the free pages portion, then we don't have to move the page around, and we are done.
> 3. If we cannot find a free page, we will have to ask for more from the disk and insert the allocated free page at the front of free-page list.

> [!example] Fa20 Discussion2 P4
> ![](Disk_Space_Management.assets/image-20240124083103165.png)



### Page Directory Implementation
> [!concept] Page Directory Layout
> ![](Disk_Space_Management.assets/image-20240124085458218.png)
> **In this implementation, we have:**
> 1. A header page that stores entries. Each entry contains a pointer(4 bytes on 32-bit machine) to the data page and the amount of free space(4 bytes int), so 8 bytes each entry.
> 2. The header page also maintains a pointer to the next header page. So it is a singly linked list.
> 
> We have the following operations:
> 1. **Find free page:** Look up all the page entries(including those pointing to the full page, since we don't have ordering) in the header page. Runtime is just $O(\#~header~pages)$.
> 2. **Insert a record:** First find a free page(read I/O at header page), then read the data page(read I/O), write the record, and write back to disk(write I/O).
> 3. **Delete a record:** First find the record(read I/O at header page+read I/O at data page), then write the record, and write back to disk(write I/O).

> [!example] Fa20 Note02 Practice Q1
> ![](Disk_Space_Management.assets/image-20240124095502941.png)![](Disk_Space_Management.assets/image-20240124095630698.png)

> [!example] Fa20 Discussion2 P5
> ![](Disk_Space_Management.assets/image-20240124083202582.png)

> [!example] Sp18 Vitamin 2 Q2
> ![](Disk_Space_Management.assets/image-20240129092827370.png)

> [!example] Concept Check
> ![](Disk_Space_Management.assets/image-20240128165556545.png)
> It requies $O(\#header ~pages)$ to look up.



## Sorted Files
> [!def]
> A sorted file is a file type where pages are ordered and records within each page are sorted by key(s).
> ![](Disk_Space_Management.assets/image-20240124090222408.png)




## Efficiency Analysis
### Assumptions
> [!warning] 
> For analysis, we will use the following assumptions:
> - We are mostly concerned about the **average** case.
> - The workload is **uniform random.**
> - Inserts and deletes operate on **single records.**
> - Equality selections will have **exactly one match.**
> - Heap files always **insert to the end of the file.**
> - Sorted files are always sorted according to search key.
> - Packed files are compacted after deletions.


### Scan all records
> [!concept]
> ![](Disk_Space_Management.assets/image-20240124090301288.png)![](Disk_Space_Management.assets/image-20240124090308813.png)
> Scanning records doesn't require writing operation, only read and check.


### Equality Search - Find
> [!concept] Heap File
> ![](Disk_Space_Management.assets/image-20240124090352792.png)
> Here we compute the expected number of the pages touched under probabilistic framework:
> We define the number of pages touched to be a random variable $X$, suppose it only takes value $1,2,3,4$:
> $$\begin{aligned}E[X]&=1*P(X=1)+2*P(X=2)+3*P(X=3)+4*P(X=4)\\&(1+2+3+4)*\frac{1}{B}\\&=\frac{10}{B}\end{aligned}$$
> Here $P(X=i), i=1,2,3,4$ is the probablity that the record is in the page i, which is $\frac{1}{B}$.
> 

> [!concept] Sorted File
> ![](Disk_Space_Management.assets/image-20240124090731692.png)![](Disk_Space_Management.assets/image-20240124090752990.png)![](Disk_Space_Management.assets/image-20240124090757921.png)
> Here $P(X=i)$ is the probability that the record appears in the level-(i-1) pages, which is $\frac{2^{i-1}}{B}$.
> 
> ![](Disk_Space_Management.assets/image-20240124090933948.png)



### Range Search
> [!concept]
> ![](Disk_Space_Management.assets/image-20240124091001199.png)
> For heap file, range search will always touch all pages.
> For sorted file, we first find the page using binary search, then scan to the right.
> 
> ![](Disk_Space_Management.assets/image-20240124091048352.png)
> Here `pages` indicates the number of pages that is traversed after we pinpoint the left end of the range until the right end of the range.


### Insertion - When no free pages
> [!concept]
> Inserted record could potentially cause all later records to be pushed back by one. On average, N / 2 pages will need to be pushed back, and this involves a read and a write IO for each of those pages, which results in the N I/Os term.
> ![](Disk_Space_Management.assets/image-20240124095227122.png)![](Disk_Space_Management.assets/image-20240124091648198.png)
> **Note:** Here we assume that we all the pages are full, so we will have to allocate a new page adn insert the record in it, which involves a simple insertion at the front of free-page list.
> 
> 2 means one read and one write. One read indicates that we have to read the page into the main memory and let CPU decide how the record should be placed inside the page. One write is that the page should be updated to the disk.
> ![](Disk_Space_Management.assets/image-20240124094544858.png)![](Disk_Space_Management.assets/image-20240124094553147.png)


### Deletion
> [!concept]
> **Deletion involves:**
> 1. Find the record. (Read I/O, average B/2 read)
> 2. Modify the page. (CPU)
> 3. Write the page back to disk. (Write I/O, reason for +1)
> 
> ![](Disk_Space_Management.assets/image-20240124094611048.png)![](Disk_Space_Management.assets/image-20240124094617080.png)
> For heap file, since we don't need to sort the file, upon deletion we don't have to rearrage the file records.
> 
> So deletion costs less than sorted files(under our assumptions).



### Summary
> [!summary]
> Under our assumptions:
> - We are mostly concerned about the **average** case.
> - The workload is **uniform random.**
> - Inserts and deletes operate on **single records.**
> - Equality selections will have **exactly one match.**
> - Heap files always **insert to the end of the file.**
> - Sorted files are always sorted according to search key.
> - Packed files are compacted after deletions.
> 
> We have the following runtime table.
> ![](Disk_Space_Management.assets/image-20240129093000613.png)
> The entry may change if we drop some of the assumptions.

> [!example] When to use which?
> ![](Disk_Space_Management.assets/image-20240129094319500.png)![](Disk_Space_Management.assets/image-20240129094326338.png)











# Records in Pages - Page Layout
## Overview
> [!overview]
> ![](Disk_Space_Management.assets/image-20240124100124336.png)![](Disk_Space_Management.assets/image-20240124100130153.png)



## Fixed Length Records - Page Header
### Packed Layout - Offset
> [!concept]
> ![](Disk_Space_Management.assets/image-20240124100353546.png)
> If the page is packed, there are no gaps between records.
> 
> The page header just need to store `num_of_records`(4 bytes). 
> 
> We define the following operations on the page:
> 1. **Find the n-th record**: Since each record's length is fixed, we could compute the offset of the n-th record to be `offset = header_size + (record_size) * (n-1)` 
> 2. **Insert a record**: Since the page is packed, we just insert at the end by first compute the address `start = header_size + (record_size) * n` and insert at here. After that we have to increment the `num_of_records` by 1.
> 3. **Delete a record**: Upon deletion, we have to rearrange the records to the packed layout and update the index of each record after the deleted one. The 5-th record now becomes the 4-th record. Moreover, we have to decrement the `num_of_records` by 1.
> 
> ![](Disk_Space_Management.assets/image-20240124100924781.png)![](Disk_Space_Management.assets/image-20240124100935095.png)



### Unpacked Layout - Bitmap
> [!concept]
> ![](Disk_Space_Management.assets/image-20240124100952197.png)
> In the unpacked layout, records can have gap in between.
> 
> The page header just have to store an **additional bitmap** on top of `num_of_bytes`. So the page header in both cases are at least 4 bytes.
> 
> We define the following procedures:
> 1. Find a record: Same as paceked layout.
> 2. Insert a record:
> 	1. Find the first slot that has bit 0(guaranteed to have enough space for the record, since fixed length)
> 	2. If found, flip the bit.
> 	3. If not, add a new slot and set the bit to 1.
> 3. Delete a record:
> 	1. Find the record.
> 	2. Delete the record.
> 	3. Flip the bit.
> 	4. The index of each record doesn't change.
>
>![](Disk_Space_Management.assets/image-20240124101617574.png)

> [!quiz] Concept Check
> **We usually use bitmaps for pages with fixed-length records. Why not just use a slotted page for pages with fixed-length records?**
> 
> Bitmaps have better space complexity since slotted pages use pointers which are addresses.

## Variable Length Records - Slotted Layout
### Page Footer
> [!concept]
> ![](Disk_Space_Management.assets/image-20240124101656958.png)![](Disk_Space_Management.assets/image-20240124101707576.png)
> **Note:** The reason is that the slot directory grows from the end to start and the records grow grom start to end. When they meet, we say that further insertion is denied and the page is full. 



### Slotted Directory
> [!concept]
> ![](Disk_Space_Management.assets/image-20240124101816679.png)
> To work around this, each page uses a **page footer** that maintains a slot directory tracking **slot count**, **a free space pointer**, **and entries**. 
> 
> 
> 1. The **slot count** tracks the **total number of slots**. This **includes both filled and empty slots.** 
> 2. The **free space pointer** points to the next free position within the page. 
> 3. **Each entry** in the slot directory consists of a [record pointer, record length] pair.
> 
> The footer starts from the bottom of the page rather than the top so that the slot directory has room to grow when records are inserted. 

> [!summary]
> The maximum number of records that can be stored in a page is equal to the page size divided by the minimum record size, rounded down to the nearest integer.
> 
> For slotted page, it would be the floor of **(page size - page footer size) / (min record size + 8 bytes)** due to the additional metadata needed.
> 
> - Here the **min record size + 8 bytes** is the minimum size a record may take up within the page, including 8 bytes in the slot directory entry and the record size with variable length field set to NULL(0 bytes).
> - **page size** need to minus page footer size, since page footer are not used to store records. Typically, the size is 8 bytes since we have to store the free record pointer(4 bytes) and slot directory size(4-byte-int).

> [!quiz] True or False
> Assuming integers take 4 bytes and pointers take 4 bytes, a slot directory that is 512 bytes can address 64 records in a page.
> 
> **False**, we have the free space pointer, which doesn’t fit after 64 * (4 + 4) = 512 bytes of per-record data in the slot directory.
> 
> Actually, we are only able to address $\frac{512 - 4 - 4}{4 + 4} = 63$ slots.

> [!example] Sp18 Vitamin 2 Q4
> ![](Disk_Space_Management.assets/image-20240129095137484.png)

> [!example] Fa20 Note02 Practices Q3
> ![](Disk_Space_Management.assets/image-20240124103132175.png)![](Disk_Space_Management.assets/image-20240124103151867.png)

### Packed Layout
> [!important] Deletion Operation
> Deletion involves removing the record’s entry within the slot directory. 
> 
> Additionally, records after the deleted record must be moved towards the top of the page by one position and the corresponding slot directory entries shifted towards the bottom of the page by one position.
> ![](Disk_Space_Management.assets/image-20240124101903562.png)![](Disk_Space_Management.assets/image-20240124101910310.png)

> [!important] Insertion Operation
> For insertion, the record is inserted at the free space pointer and a new entry is added every time if all slots are full.
> 
> Then we reorganize the records to remain packed state.
> ![](Disk_Space_Management.assets/image-20240124101947724.png)![](Disk_Space_Management.assets/image-20240124101953298.png)![](Disk_Space_Management.assets/image-20240124102000292.png)![](Disk_Space_Management.assets/image-20240124102005770.png)![](Disk_Space_Management.assets/image-20240124102011415.png)



### Unpacked Layout
> [!important] Deletion Operation
> Deletion involves finding the record’s entry within the slot directory and setting both the record pointer and record length to null.


> [!important] Insertion Operation
> For future insertions, the record is inserted into the page at the free space pointer and a new [pointer, length] pair is set in any available null entry. 
> 
> 


### Growing Slots
> [!important] Growing - In both layout
> In the case where there are no null entries, a new entry is added to the slot directory for that record. The **slot count** is used to determine which offset the new slot entry should be added at, and then the slot count is incremented. Periodically, records will be reorganized into a packed state where deleted records are removed to make space for future insertions.
> ![](Disk_Space_Management.assets/image-20240124102704955.png)![](Disk_Space_Management.assets/image-20240124102709781.png)![](Disk_Space_Management.assets/image-20240124102721684.png)


### Summary
> [!summary]
> ![](Disk_Space_Management.assets/image-20240124102737482.png)











# Entries in Records - Record Layout
> [!important]
> Regardless of the format, every record can be uniquely identified by its record id - **[page #, record # on page]**.

## Fixed Length Record
> [!concept]
> FLRs only contain fixed length fields (integer, boolean, date, etc.), and FLRs with the same schema consist of the same number of bytes
> ![](Disk_Space_Management.assets/image-20240124102843455.png)

> [!quiz] True or False
> In a page containing fixed-length records with no nullable fields, the size of the bitmap never changes. 
> 
> **True**, the size of the records is fixed, so the number we can fit on a page is fixed.

> [!example] Fa20 Note02 Practices Q2
> ![](Disk_Space_Management.assets/image-20240124103052450.png)![](Disk_Space_Management.assets/image-20240124103112340.png)





## Variable Length Record
> [!concept]
> VLRs contain both fixed length and variable length fields (varchar), resulting in each VLR of the same schema having a potentially different number of bytes. VLRs store all fixed length fields before variable length fields and use a record header that contains pointers to the end of the variable length fields.
> ![](Disk_Space_Management.assets/image-20240124102852246.png)![](Disk_Space_Management.assets/image-20240124102900174.png)![](Disk_Space_Management.assets/image-20240129090841342.png)
> **Summary on variable length record:**
> 1. Each record contains a record header
> 2. Variable length fields are placed after fixed length fields
> 3. Record header stores field offset indicating where each variable length field ends
> 4. Record headers contain pointers to the end of variable length fields
> 5. Moving variable length fields to the end of a record is a useful optimization.
> 
> **An aside: this is not actually sufficient for storing NULLs**
> - Cannot distinguish between empty string (“”) and NULL
> - Need some extra metadata (e.g. bitmap in record header or special char in field), which varies widely between different DBMS

> [!quiz] True or False
> Is fragmentation an issue with variable length records on a slotted page?
> 
> **Yes.** Even if we periodically pack up the records. We cannot guarantee the packed state upon each deletion.
> 

> [!quiz] Concept Check
> ![](Disk_Space_Management.assets/image-20240124103405056.png)![](Disk_Space_Management.assets/image-20240124103412803.png)

> [!example] Fa20 Discussion2 P3
> ![](Disk_Space_Management.assets/image-20240124083133406.png)

> [!example] Sp18 Vitamin 2 Q4
> ![](Disk_Space_Management.assets/image-20240129100003566.png)![](Disk_Space_Management.assets/image-20240129095955318.png)
> Note that here record header is disjoint with the variable length field pointer.



# Conclusion
> [!summary]
> ![](Disk_Space_Management.assets/image-20240124102913113.png)![](Disk_Space_Management.assets/image-20240124102924262.png)

> [!example] Sp18 Vitamin 2 Q5
> ![](Disk_Space_Management.assets/image-20240129101027343.png)![](Disk_Space_Management.assets/image-20240129101032551.png)
> For heap file, insertions requires the least I/Os, just write to the end of the free data page. One read I/O and one write I/O. Select requires reading all the data pages.
> Delete requires first reading all the data pages to find the record then delete the records and write to the disk.
> 
> ![](Disk_Space_Management.assets/image-20240129101327273.png)
> For sorted file, deletion and insertion requires the same amount of time due to rearrangement(more than full scan). Select requires just a full scan.
> 
> ![](Disk_Space_Management.assets/image-20240129101436614.png)
> When using fixed length records, VARCHAR(20) should be modified as CHAR(20), which always take up 20 bytes no matter how long the actual data is. So the answer is just 4 bytes $\times$ 3 + 20 bytes $\times$ 2 = 52 bytes.










