# Part A: Cache Simulator(Medium)
> [!overview]
> ![](Cache%20Lab.assets/image-20231207190005828.png)
```c
#include "cachelab.h"

int main()
{
    printSummary(0, 0, 0);
    return 0;
}
```


## Phase 1: Cache Data Structure
> [!task] Define Cache Data Structure
> ![](Cache%20Lab.assets/image-20231207190044680.png)![](Cache%20Lab.assets/image-20231207204512736.png)![](Cache%20Lab.assets/image-20240229185050688.png)

> [!code] Data Structure and Initialization
> Note that when we index into a 2d-array, we'd better use `cache_line[line_index][block_index]`, which is canonical way.
```c
// Start of a cache line, or cache block
typedef struct cache_line {
    int valid_bit;
    int tag;
    long lru_bit;
} cache_line_t;

// Cache data structure
typedef struct cache {
    int s; // Index bits
    int E; // Associativity bits
    int b; // Block size
    cache_line_t** cache;
} cache_t;

void init_cache(int s, int E, int b) {
    
    int S = 1 << s;

    // Malloc
    cache_o = (cache_t *) malloc(sizeof(cache_t));
    cache_o -> s = s;
    cache_o -> E = E;
    cache_o -> b = b;
    cache_o -> cache = (cache_line_t ** ) malloc(S * sizeof(cache_line_t*));
    if (cache_o -> cache == NULL) {
        fprintf(stderr, "Malloc Failed!");
        exit(1);
    }
    for (int i = 0; i < S; i++) {
        cache_line_t* line = (cache_line_t*) malloc(E * sizeof(cache_line_t));
        if (line == NULL) {
            fprintf(stderr, "Malloc Failed!");
            exit(1);
        }

        cache_o -> cache[i] = line;
        for (int j = 0; j < E; j++) {
            cache_o->cache[i][j].valid_bit = 0; //Empty data at the beginning
            cache_o->cache[i][j].tag = -1; // Nothing in the cache, so tag bits are all 0x11111111
            cache_o->cache[i][j].lru_bit = 0; // At the very beginning, all pages are equally least significantly used.
        }
    }

}
```

> [!bug] Caveats
> Note that the following way of implementing 2d indexing is faulty and could cause memory leak issues. The reason is that for `cache_line_t* line` pointer,  `&line[j * sizeof(cache_line_t)]` is equal to `line + j * sizeof(cache_line_t)` instead of `line + j`(which we want).
> 
> Here the pointer arithmetic is `line + j = addr(line) + j * sizeof(cache_line_t)`, but  `line + j * sizeof(cache_line_t) = addr(line) + (j * sizeof(cache_line_t)) * sizeof(cache_line_t)`.
> 
> The key reason is that for `type* obj`, if we use `obj + i`, we are moving the pointer by `i*sizeof(type)`. 
> ![](Cache%20Lab.assets/image-20240301120152396.png)





## Phase 2: Parse the command line arguments
> [!concept] getopt
> This function deserves some explanations. However, we could always refer to the man page of it.
> First, the function signature, `int getopt(int argc, char* const argv[], const char* optstring)`
> ![](Cache%20Lab.assets/image-20231207200856514.png)
> Here, `x:y:` means flag x and flag y requires argument, and the corresponding argument will be returned in a `optarg` variable for user to extract the cmd value.
```c
int opt;
    
int s = 0; 
int E = 0;
int b = 0;

// : indicates that we need input for this argument.
// Here we want -s 2 -E 4 -b 3 -t filepath
while (-1 != (opt = getopt(argc, argv, "hvs:E:b:t:"))) {
	switch(opt) {
		case 'h': // Print help or not
			print_help();
			exit(0); // We just want to print the help info.
		case 'v':  // Verbose
			v = 1;
			break;
		case 's':  // Index Bits, num_lines = 2^s
			s = atoi(optarg);
			break;
		case 'E':  // Blocks per set
			E = atoi(optarg);
			break;
		case 'b': // Block bits
			b = atoi(optarg);
			break;
		case 't': // Trace file path
			strcpy(t, optarg);
			break;
		default:
			// If any arguments that require input doesn't receive the input
			// We print the help info and exit the program.
			print_help();
			exit(-1);
	}
}

// Print Help Info
void print_help()
{
    printf("** A Cache Simulator by Deconx\n");
    printf("Usage: ./csim-ref [-hv] -s <num> -E <num> -b <num> -t <file>\n");
    printf("Options:\n");
    printf("-h         Print this help message.\n");
    printf("-v         Optional verbose flag.\n");
    printf("-s <num>   Number of set index bits.\n");
    printf("-E <num>   Number of lines per set.\n");
    printf("-b <num>   Number of block offset bits.\n");
    printf("-t <file>  Trace file.\n\n\n");
    printf("Examples:\n");
    printf("linux>  ./csim -s 4 -E 1 -b 4 -t traces/yi.trace\n");
    printf("linux>  ./csim -v -s 8 -E 2 -b 4 -t traces/yi.trace\n");
}
```


## Phase 3: Read from trace file
> [!concept]
> ![](Cache%20Lab.assets/image-20231207204542926.png)
```c
FILE* infile = fopen(t, "r");

    FILE* outfile = fopen("./cache_status.txt", "a+");
    if (infile == NULL || outfile == NULL) {
        // fprintf(stderr, "File open failed!");
        exit(-1);
    }

    char identifer; // I, M, L, S
    unsigned address; // memory address
    int size; // size to read

    // Even if there is a whitespace in front of %c, we can still read in instruction line. So we use switch to filter them out.
    while(fscanf(infile, " %c %x,%d", &identifer, &address, &size) > 0) {
        message_t message_o;

        // message_o.buf = {'\0'}; // Cannot use this, can only be used at initialization.

        memset(message_o.buf, 0, sizeof(message_o.buf));

        switch(identifer) {
            case 'M':
                // Data Load
                lookup_cache(cache, address, &message_o);
                // Data Write
                lookup_cache(cache, address, &message_o);
                break;
            case 'L':
                // Data Load
                lookup_cache(cache, address, &message_o);
                break;
            case 'S':
                // Data Write
                lookup_cache(cache, address, &message_o);
                break;
        }
        // Verbose
        if (v == 1) {
            print_verbose_trace(identifer, address, size, &message_o, NULL);
        }
    }
    fclose(infile);
    fclose(outfile);
```


## Phase 4: Replacement Policy
> [!important]
> See [TLB Access Pattern](../../../../Machine_Structures/7_OS_Memory_Optimization/OS_VM_I_O.md#TLB%20Access%20Pattern)

### Method 1: LRU
> [!concept]
> **Main Idea:**
> 
> The idea is simple, we just find the non-empty block with the biggest `lru_bit` field and return that block's index to the calling function.

> [!code]
```c
int get_eviction(cache_t* cache_o, int set_index) {
    int E = cache_o -> E;
    int max_LRU = -1;
    int max_LRU_index = -1;
    for (int j = 0; j < E; j++) {
        int lru_bit = (cache_o -> cache[set_index][j]).lru_bit;
        if (lru_bit > max_LRU) {
            max_LRU_index = j;
            max_LRU = lru_bit;
        }  
    }
    return max_LRU_index;
}

```



### Method 2: LFU
> [!concept]
> 


> [!code]



### Method 3: MRU
> [!concept]
> 

> [!code]



## Phase 5: Cache Update Rules
### Using LRU
> [!concept]
> **Main idea is that:**
> 1. We should set the `lru_bit` of the newly updated block to `0`.
> 2. We should increment the `lru_bit` of the all the other blocks by `1`.
> 	1. Implementation 1 increment all the other valid blocks by 1.
> 	2. Implementaion 2 increments all the other blocks (no matter valid or not) by 1.
> 	3. Both implementations are fine.
> 3. We should set the `tag` of the newly updated block to the new tag.
> 4. We should set the `valid_bit` of the newly updated block to `1`.

> [!code] Implementation 1
```c
void lru_update_cache(cache_t* cache_o, int set_index, int block_index, unsigned tag) {
    int E = cache_o -> E;
    cache_o->cache[set_index][block_index].valid_bit = 1;
    cache_o->cache[set_index][block_index].tag = tag;
    for (int j = 0; j < E; j++) {
        int valid_bit = cache_o -> cache[set_index][j].valid_bit;
        if (valid_bit == 1) {
            cache_o->cache[set_index][j].lru_bit ++;
        }
    }
    cache_o->cache[set_index][block_index].lru_bit = 0;
}
```

> [!code] Implementation 2
> 
```c
void lru_update_cache(cache_t* cache_o, int set_index, int block_index, unsigned tag) {
    int E = cache_o -> E;
    for (int j = 0; j < E; j++) {
        if (j != block_index) {
            cache_o->cache[set_index][j].lru_bit ++;
        } else {
            cache_o->cache[set_index][j].valid_bit = 1;
            cache_o->cache[set_index][j].lru_bit = 0;
            cache_o->cache[set_index][j].tag = tag;
        }
    }
}
```


### Using LFU



### Using MRU





## Phase 6: Cache Lookup
> [!important]
> To look up or write to the cache at `address`, we have to perform the following steps:
> 1. Perform `TIO` breakdown on the `address` based on the cache parameter `s, b`. We will use bitwise operations to extract the corresponding bits from `address`.
> 	- Note that `address` needs to be declared as `unsigned` type since we don't want the arithmetic shift to cause more trouble.
> 2. Indexing into the cache data structure using `cache[I]` and find the block.
> 	- Find if there is any matching block with the same `tag` field as `T`. If there is matching, it is a cache hit events, then we follow the updating rules in phase 5. If there is not, it is a cache miss events.
> 	- For cache miss, if there is empty block with the line `cache[I]`(having `valid_bit == 0`), then put the new block at such empty blocks with the lowest index.
> 	- If there is no empty blocks with the line, then it is a `eviction` event, we will following the replacement rules specified in phase 4 to find a page to evict and then update the cache following the phase 5.
> 3. Print the verbose message if `-v` flag is present in phase 2.

> [!code] Cache Lookup Implementation
```c
void lookup_cache(cache_t* cache_o, unsigned address, message_t* message_o) {
    // 1. Perform TIO breakdown
    unsigned T, I;

    int s = cache_o -> s;
    int b = cache_o -> b;

    T = address >> (s + b);
    I = (address << (address_bit - s - b)) >> (address_bit - s);

    // 2. Look up the corresponding line in the cache while checking for empty lines
    int found_index = get_match_tag(cache_o, I, T);
    if (found_index != -1) {
        // Cache Hit
        hits++;
        lru_update_cache(cache_o, I, found_index, T);
        update_message(message_o, "hit ");
        return;
    }

    // Cache Miss
    int found_empty_index = get_free_block(cache_o, I);
    if (found_empty_index == -1) {
        // Replacement Policy
        int eviction_index = get_eviction(cache_o, I);
        update_message(message_o, "miss ");
        update_message(message_o, "eviction ");
        lru_update_cache(cache_o, I, eviction_index, T);
        misses++;
        evictions++;
    } else {
        // Placement Policy
        update_message(message_o, "miss ");
        lru_update_cache(cache_o, I, found_empty_index, T);
        misses++;
    }
}
```

> [!code] Print Verbose Information
```c
void print_verbose_trace(char type, unsigned address, int size, message_t* message_o, FILE* outfile) {
    if (type != 'I') {
        if (outfile == NULL) {
            printf("%c %9x,%d %s\n", type, address, size, message_o->buf);
        } else {
            fprintf(outfile, "%c %9x,%d %s\n", type, address, size, message_o->buf);
        }
    }
}

```


## Phase 6: Main Program
> [!important]
> Main Idea, the whole C program(300+ lines) has the following logics:
> 1. Read the arguments from the user.
> 2. Initialize the cache.
> 3. Simulate the cache behavior with `trace` file.
> 4. Print the summary statistics.
> 5. Free up the cache.

```c
#include "cachelab.h"
#include <unistd.h>
#include <getopt.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>
#include <stdio.h>

typedef struct cache_line {
    int valid_bit;
    int tag;
    long lru_bit;
} cache_line_t;


typedef struct cache {
    int s; // Index bits
    int E; // Associativity bits
    int b; // Block size
    cache_line_t** cache;
} cache_t;


// The maximum length of message is just 17 bytes. (miss eviction hit)
typedef struct message {
    char buf[2048];
} message_t;

// 1. Initialize the cache data structure on the static segment but the pointer
// points to the heap memory
cache_t* cache_o = NULL;

// 2. Accumulator on the static
int hits = 0;
int misses = 0;
int evictions = 0;

// 3. Virtual Memory Stat
int address_bit = 64;

// 4. Verbose Flag
int v = 0;
// Path to the trace file.
char t[1000]; 

void init_cache(int s, int E, int b) {
    
    int S = 1 << s;

    // Malloc
    cache_o = (cache_t *) malloc(sizeof(cache_t));
    cache_o -> s = s;
    cache_o -> E = E;
    cache_o -> b = b;
    cache_o -> cache = (cache_line_t ** ) malloc(S * sizeof(cache_line_t*));
    if (cache_o -> cache == NULL) {
        fprintf(stderr, "Malloc Failed!");
        exit(1);
    }
    for (int i = 0; i < S; i++) {
        cache_line_t* line = (cache_line_t*) malloc(E * sizeof(cache_line_t));
        if (line == NULL) {
            fprintf(stderr, "Malloc Failed!");
            exit(1);
        }

        cache_o -> cache[i] = line;
        for (int j = 0; j < E; j++) {
            cache_o->cache[i][j].valid_bit = 0; //Empty data at the beginning
            cache_o->cache[i][j].tag = -1; // Nothing in the cache, so tag bits are all 0x11111111
            cache_o->cache[i][j].lru_bit = 0; // At the very beginning, all pages are equally least significantly used.
        }
    }

}


void clear_cache(cache_t* cache_o) {
    int s = cache_o -> s;
 
    int num_lines = 1 << s;
    for (int i = 0; i < num_lines; i++) {
        free((cache_o -> cache)[i]);
    }
    free(cache_o -> cache);
    free(cache_o);
}

void update_message(message_t* message_o, char* message) {
    char* buf = message_o -> buf;
    int message_length = strlen(buf);
    strncpy(buf + message_length, message, strlen(message));
}


void lru_update_cache(cache_t* cache_o, int set_index, int block_index, unsigned tag) {
    int E = cache_o -> E;
    for (int j = 0; j < E; j++) {
        if (j != block_index) {
            cache_o->cache[set_index][j].lru_bit ++;
        } else {
            cache_o->cache[set_index][j].valid_bit = 1;
            cache_o->cache[set_index][j].lru_bit = 0;
            cache_o->cache[set_index][j].tag = tag;
        }
    }
}


int get_match_tag(cache_t* cache_o, int set_index, unsigned T) {
    int E = cache_o -> E;
    for (int j = 0; j < E; j++) {
        int valid_bit = (cache_o -> cache[set_index][j]).valid_bit;
        unsigned tag = (cache_o -> cache[set_index][j]).tag;
        if (tag == T && valid_bit == 1) {
            // Cache Hit
            return j;
        }
    }
    return -1;
}

int get_eviction(cache_t* cache_o, int set_index) {
    int E = cache_o -> E;
    int max_LRU = -1;
    int max_LRU_index = -1;
    for (int j = 0; j < E; j++) {
        int lru_bit = (cache_o -> cache[set_index][j]).lru_bit;
        if (lru_bit > max_LRU) {
            max_LRU_index = j;
            max_LRU = lru_bit;
        }  
    }
    return max_LRU_index;
}


int get_free_block(cache_t* cache_o, int set_index) {
    int E = cache_o -> E;
    for (int j = 0; j < E; j++) {
        int valid_bit = (cache_o -> cache[set_index][j]).valid_bit;
        if (valid_bit == 0) {
            // Cache Hit
            return j;
        }
    }
    return -1;
}


void lookup_cache(cache_t* cache_o, unsigned address, message_t* message_o) {
    // 1. Perform TIO breakdown
    unsigned T, I;

    int s = cache_o -> s;
    int b = cache_o -> b;

    T = address >> (s + b);
    I = (address << (address_bit - s - b)) >> (address_bit - s);

    // 2. Look up the corresponding line in the cache while checking for empty lines
    
    int found_index = get_match_tag(cache_o, I, T);
    if (found_index != -1) {
        // Cache Hit
        hits++;
        lru_update_cache(cache_o, I, found_index, T);
        update_message(message_o, "hit ");
        return;
    }

    // Cache Miss
    int found_empty_index = get_free_block(cache_o, I);
    if (found_empty_index == -1) {
        // Replacement Policy
        int eviction_index = get_eviction(cache_o, I);
        update_message(message_o, "miss ");
        update_message(message_o, "eviction ");
        lru_update_cache(cache_o, I, eviction_index, T);
        misses++;
        evictions++;
    } else {
        // Placement Policy
        update_message(message_o, "miss ");
        lru_update_cache(cache_o, I, found_empty_index, T);
        misses++;
    }
}


void print_cache(cache_t* cache_o, FILE* outfile) {
    int s = cache_o -> s;
    int E = cache_o -> E;

    int num_lines = 1 << s;

    // Malloc
    for (int i = 0; i < num_lines; i++) {
        for (int j = 0; j < E; j++) {
            cache_line_t block = (cache_o -> cache)[i][j];
            if (outfile == NULL) {
                printf("Index: %d, block: %d, valid_bit: %d, lru_bit: %lu\n", i, j, block.valid_bit, block.lru_bit);
            } else {
                fprintf(outfile, "Index: %d, block: %d, valid_bit: %d, lru_bit: %lu\n", i, j, block.valid_bit, block.lru_bit);
            }
            
        }
    }
}



void print_verbose_trace(char type, unsigned address, int size, message_t* message_o, FILE* outfile) {
    if (type != 'I') {
        if (outfile == NULL) {
            printf("%c %9x,%d %s\n", type, address, size, message_o->buf);
        } else {
            fprintf(outfile, "%c %9x,%d %s\n", type, address, size, message_o->buf);
        }
    }
}


void simulate_cache(cache_t* cache) {

    FILE* infile = fopen(t, "r");

    FILE* outfile = fopen("./cache_status.txt", "a+");
    if (infile == NULL || outfile == NULL) {
        // fprintf(stderr, "File open failed!");
        exit(-1);
    }

    char identifer; // I, M, L, S
    unsigned address; // memory address
    int size; // size to read

    // Only read the lines that starts with a whitespace(not the instruction)
    while(fscanf(infile, " %c %x,%d", &identifer, &address, &size) > 0) {
        message_t message_o;
        // message_o.buf = {'\0'}; // Cannot use this, can only be used at initialization.

        memset(message_o.buf, 0, sizeof(message_o.buf));

        switch(identifer) {
            case 'M':
                // Data Load
                lookup_cache(cache, address, &message_o);
                // Data Write
                lookup_cache(cache, address, &message_o);
                break;
            case 'L':
                // Data Load
                lookup_cache(cache, address, &message_o);
                break;
            case 'S':
                // Data Write
                lookup_cache(cache, address, &message_o);
                break;
        }
        // Verbose
        if (v == 1) {
            print_verbose_trace(identifer, address, size, &message_o, NULL);
        }
    }
    fclose(infile);
    fclose(outfile);
}

// Print Help Info
void print_help()
{
    printf("** A Cache Simulator by Deconx\n");
    printf("Usage: ./csim-ref [-hv] -s <num> -E <num> -b <num> -t <file>\n");
    printf("Options:\n");
    printf("-h         Print this help message.\n");
    printf("-v         Optional verbose flag.\n");
    printf("-s <num>   Number of set index bits.\n");
    printf("-E <num>   Number of lines per set.\n");
    printf("-b <num>   Number of block offset bits.\n");
    printf("-t <file>  Trace file.\n\n\n");
    printf("Examples:\n");
    printf("linux>  ./csim -s 4 -E 1 -b 4 -t traces/yi.trace\n");
    printf("linux>  ./csim -v -s 8 -E 2 -b 4 -t traces/yi.trace\n");
}



int main(int argc, char** argv)
{
    int opt;
    
    int s = 0; 
    int E = 0;
    int b = 0;

    // : indicates that we need input for this argument.
    while (-1 != (opt = getopt(argc, argv, "hvs:E:b:t:"))) {
        switch(opt) {
            case 'h':
                print_help();
                exit(0); // We just want to print the help info.
            case 'v':
                v = 1;
                break;
            case 's':
                s = atoi(optarg);
                break;
            case 'E':
                E = atoi(optarg);
                break;
            case 'b':
                b = atoi(optarg);
                break;
            case 't':
                strcpy(t, optarg);
                break;
            default:
                // If any arguments that require input doesn't receive the input
                // We print the help info and exit the program.
                print_help();
                exit(-1);
        }
    }

    // 1. Initialize the cache
    if (s == 0 || E == 0 || b == 0) {
        fprintf(stderr, "Missing arguments for cache parameters");
        exit(1);
    }

    init_cache(s, E, b);

    // 2. Simulate Cache Behaviors by reading the trace
    simulate_cache(cache_o);

    // 3. Print the simulation results
    printSummary(hits, misses, evictions);

    // 4. Free the cache
    clear_cache(cache_o);
    return 0;
}


```


# Part B: Matrix Transpose Function(Hard)
## Testing Specs
> [!important]
> ![](Cache%20Lab.assets/image-20240512103458552.png)![](Cache%20Lab.assets/image-20240512115206271.png)



## Design Ideas
> [!algo] Idea
> See [Cache Blocking in Matrix Multiplication](../../../../Machine_Structures/7_OS_Memory_Optimization/Caches_Optimization.md#With%20Blocking) (原理笔记)
> 
> Another fantastic video https://www.youtube.com/watch?v=huz6hJPl_cU （原理解释）



## 32 x 32 Matrix(Medium)
### Naive Approach
> [!algo]
```c
void trans_submit(int M, int N, int A[N][M], int B[M][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            int tmp = A[i][j];
            B[j][i] = tmp;
        }
    }
}
```
> [!important] Analysis
> ![](Cache%20Lab.assets/image-20240513203809336.png)![](Cache%20Lab.assets/image-20240513203817121.png)




### Blocked Approach(8 x 8 Matrix Block)
> [!algo]
```c
int i, j, i1, j1;
int gap = 8;
for (i = 0; i < N; i += gap) {
	for (j = 0; j < M; j += gap) {
		for (i1 = i; i1 < i + gap && i1 < N; i1++) {
			for (j1 = j; j1 < j + gap && j1 < M; j1++) {
				B[j1][i1] = A[i1][j1];
			}
		}
	}
}
```

> [!important] Analysis
> ![](Cache%20Lab.assets/image-20240512143503862.png)
> Suppose the starting address of matrix A is `0xA+0000` and matrix B is `0x A+1000`.
> - Determine optimal matrix block size. 
> 	- Principle: Minimize the portion of cache miss.
> 	- Method: Find how many continuous blocks of data can fit into the entire cache without conflict for direct mapped cache.
> 	- Ex: The cache is 1KiB = 1024B, since each line of the matrix contains 32 ints(128 bytes), the cache can hold 8 lines without conflict. So our block size would better be 8 x 8.
> - Analyze the **non-diagonal** cache miss rate:
> 	- For non-diagonal blocks, they belong to different cache index. In the graph above, the first block column would go to cache index with 1 mod 4, while the second block column would go to cache index with 2 mod 4, so these two columns won't conflict. In other words, there won't be any conflict miss.
> 	- ![](Cache%20Lab.assets/image-20240512144450587.png)
> 	- The cache miss rate would be 1 / 8 of the operations. Here since there is 64 ints in a matrix block, the number of cache miss per block should be 64 / 8 = 8 times. So in total, there should be 12 x 8 x 2 = 192 misses.
> - Analyze the **diagonal** cache miss rate:
> 	- Since for diagonal blocks, they belong to the same cache index group(1 mod 4 for the first block column, 2 mod 4 for the second block column), there will be more conflict misses. Roughly each time A read a line, there will be a conflict miss and will evict the same line in B, which later on cause a conflict miss. And initially B will read all rows in, which counts for another 8 misses. So in total for each block pair(A, B), there will be 4 x 8 = 32 misses. There are 4 blocks so there should be around 32 x 4 = 128 misses.
> 	- In total, there should be around 320 misses.
> 
> ![](Cache%20Lab.assets/image-20240512153714248.png)

> [!bug] Caveat
> 上述方法存在很明显的性能问题，因为在每一个对角块中，对角线元素会导致额外的冲突，形成一种:
> - A先读取，把B踢掉。
> - B写入时候不命中，然后把A踢掉
> - A再读取的时候不命中，又要把B踢掉
> 
> 的不搞笑的缓存访问方式。




### Improved Blocked Approach(Hard)
> [!important]
> 一种改进的方式就是我们不要在每次读取完A的一个元素后就立即在B的相应位置写入元素，而是可以等待A的某一行都读取完了以后再全部写入B中，这样可以使得Conflict Miss极大幅度的减小。
```c
void transpose_32x32_submit(int M, int N, int A[N][M], int B[M][N])
{
    for(int i = 0; i < 32; i += 8)
        for(int j = 0; j < 32; j += 8)
            for (int k = i; k < i + 8; k++)
            {
                int a_0 = A[k][j];
                int a_1 = A[k][j+1];
                int a_2 = A[k][j+2];
                int a_3 = A[k][j+3];
                int a_4 = A[k][j+4];
                int a_5 = A[k][j+5];
                int a_6 = A[k][j+6];
                int a_7 = A[k][j+7];
                B[j][k] = a_0;
                B[j+1][k] = a_1;
                B[j+2][k] = a_2;
                B[j+3][k] = a_3;
                B[j+4][k] = a_4;
                B[j+5][k] = a_5;
                B[j+6][k] = a_6;
                B[j+7][k] = a_7;
            }         
}
```
> [!exp] Analysis
> 非对角线的Miss 数量不变，为192次。
> 对角线的Miss数量计算如下:
> - 对于每个Block而言，A每次读取一行的时候都会造成冷不命中，一共8次。
> - B在第一次读取的时候一共有8次MISS.
> - 之后每当A读取到第i个对角线元素时，都会将cache中对应第i行的B踢掉，后续写入B的某一列时，会触发一次B的第i行的额外的conflict miss.
> - 对于每个Block对(A, B)来说，一共有 8 + 8 + 8 = 24 次 miss, 一共有4组，所有一共是24 x 4 =96 misses
> - 加起来一共288 misses.
> 
> ![](Cache%20Lab.assets/image-20240512155643898.png)




## 64 x 64 Matrix(Very Hard)
### Naive Approach
> [!test]
> ![](Cache%20Lab.assets/image-20240512161353006.png)



### Blocked Approach with 4 x 4
> [!code]
> 因为每 4 行就会占满一个缓存，先考虑 4 × 4 分块，结果如下：
> ![](Cache%20Lab.assets/image-20240512161501763.png)



### Blocked Approach with 8 x 8
> [!code]
```c


```

> [!important]
> See https://zhuanlan.zhihu.com/p/387662272 (cachelab 最优解)on how to optimize 64 x 64 matrix using proper blocking techniques within 1024 misses!





## 61 x 67 Matrix(Easy)
> [!important]
> 使用16 x 16 的分块就能拿满分了。
```c
char transpose_61x67_submit_desc[] = "61 x 67 Input";
void transpose_61x67_submit(int M, int N, int A[N][M], int B[M][N])
{
    int i, j, i1, j1;
    int gap = 16;
    for (i = 0; i < N; i += gap) {
        for (j = 0; j < M; j += gap) {
            for (i1 = i; i1 < i + gap && i1 < N; i1++) {
                for (j1 = j; j1 < j + gap && j1 < M; j1++) {
                    B[j1][i1] = A[i1][j1];
                }
            }
        }
    }     
}
```



## Testing Results
> [!test]







