# Data Storage and Access
> [!concept]
> ![](File%20System%20Design.assets/image-20231212160824340.png)![](File%20System%20Design.assets/image-20231212160834739.png)


## readSector
> [!code]
> ![](File%20System%20Design.assets/image-20231212160931455.png)



## writeSector
> [!code]
> ![](File%20System%20Design.assets/image-20231212160938178.png)


# Sectors and Blocks
> [!concept]
> ![](File%20System%20Design.assets/image-20231212161031116.png)


# Unix File V6 System Organization
## Two types of Data
### File Payload Data
> [!concept]
> ![](File%20System%20Design.assets/image-20231212161209575.png)![](File%20System%20Design.assets/image-20231212161224554.png)



### File Metadata
> [!concept]
> ![](File%20System%20Design.assets/image-20231212161248059.png)


## File Metadata
> [!example]
> ![](File%20System%20Design.assets/image-20231212165720838.png)
> **Notes:**
> - The first block is the boot block, which typically contains information about the hard drive itself. It's so named because its contents are generally tapped when booting—i.e. restarting—the operating system. This sector is universal and essential for a computer to start or enter into BIOS.
> - The second block is the superblock, which contains information about the filesystem imposing itself onto the hardware. It's just how filesystem interacts with the operating system.
> - ==Metadata region only accounts for up to 10% of the entire drive==. Even if it appears large in the graph.


## File Contents
> [!concept]
> - File payloads are stored in chunks of 512 bytes (or whatever the block size is).
> - **When a file isn't a multiple of 512 bytes, then the final block is a partial.** The portion of that final block that contains meaningful payload is easily determined from the file size.
> - The diagram below includes illustrations for a 32 byte (blue) and a 1028 (or 2 * 512 + 4) (green) byte file (as well as a purple file, which does not have an associated outline below), so each enlists some block to store a partial.
>
> ![](File%20System%20Design.assets/image-20231212170207946.png)



## Inode 
### Concepts
> [!concept]
> ![](File%20System%20Design.assets/image-20231212161338757.png)

> [!concept]
> ![](File%20System%20Design.assets/image-20231212171859949.png)![](File%20System%20Design.assets/image-20231212170448208.png)We need to track which blocks are used to store the payload of a file.
> - The first inode is the root innode, it is the start of our file search process.
> - Note the `i_addr[8]` field, it stores up to 8 different number, each indicating a block number. **This means each file cannot exceed 512 x 8 = 4096 bytes and we will have to address this.**
> - Blocks 1025, 1027, and 1028 are part of the same file, but you only know visually because they're the same color in the diagram. 
> - Note that in `inode2`, the first three entries of `i_addr` is 1027, 1028, 1025, and they ==need to be ordered==.

> [!example] Partial Block
> ![](File%20System%20Design.assets/image-20231212172154715.png)


### Accessing Innode
> [!code]
> ![](File%20System%20Design.assets/image-20231212172248814.png)



### Large File Storation - Indirect Addressing
> [!motiv] Motivation
> ![](File%20System%20Design.assets/image-20231212172600270.png)

> [!concept] Indirect Addressing
> ![](File%20System%20Design.assets/image-20231212172657857.png)
> Even though indirect addressing is useful, but means that it takes more steps to get to the data, and we may use more blocks than we need, so:
> - We should not make all the block numbers in an innode use indirect addressing. Just some of them.
> - We should ==use indirect addressing only for large files==.





## File Directory
> [!concept]
> Note that ==each inode is only 32 bytes wide==(you can calculate it from the above struct). So if we want to store a filename into the innode, the filename cannot have more than 32 characters, which is ridiculous. Moreover, for file directory, if we want to store its system path as a field in the innode, the same tradedy will happen.
> 
> So we will have to introduce a new file type: directory.
> ![](File%20System%20Design.assets/image-20231212171638932.png)
> Have a look at the contents of block 1024, i.e. the contents of file with inumber 1, in the diagram below. This directory contains two files, so its total file size is 32; the first 16 bytes form the first row of the table (14 bytes for the filename, 2 for the inumber), and the second 16 bytes form the second row of the table. When we are looking for a file in the directory, we search this table for the corresponding inumber.
> On unix v6, filename length is limited to 14 bytes.



## File Lookup Process
> [!concept]






# Singly-Indirect Addressing
> [!concept]
> 