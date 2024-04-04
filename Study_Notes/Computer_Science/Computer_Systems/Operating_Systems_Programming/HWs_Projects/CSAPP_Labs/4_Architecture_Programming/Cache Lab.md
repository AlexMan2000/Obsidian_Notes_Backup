# Part A: Cache Simulator
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


# Part B: Matrix Transpose Function
