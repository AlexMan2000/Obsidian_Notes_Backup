# Amdahl's Law
> 



# Flynn's Taxonomy
> ![image.png](Data-Level_Parallelism.assets/20231105_1747232396.png)
> ![image.png](Data-Level_Parallelism.assets/20231105_1747267622.png)
> ![image.png](Data-Level_Parallelism.assets/20231105_1747288891.png)
> SIMD 和 MIMD 是目前最常见的并行处理技术。最普遍的并行处理编程风格是SPMD，一个程序在MIMD的所有处理器上运行。通过条件表达式进行跨处理器的执行协调。
> SIMD是专门的硬件单元，用于处理数组计算，常应用于科学计算、机器学习、信号处理和多媒体处理。




# SIMD History
## SISD/SIMD/MIMD/MISD
> ![image.png](Data-Level_Parallelism.assets/20231105_1747304543.png)![image.png](Data-Level_Parallelism.assets/20231105_1747322705.png)![image.png](Data-Level_Parallelism.assets/20231105_1747353509.png)![image.png](Data-Level_Parallelism.assets/20231105_1747374292.png)




## SIMD Evolution
> ![image.png](Data-Level_Parallelism.assets/20231105_1747397933.png)



### MMX
> ![image.png](Data-Level_Parallelism.assets/20231105_1747416116.png)




### SSE
> ![image.png](Data-Level_Parallelism.assets/20231105_1747423153.png)



### AVX
> ![image.png](Data-Level_Parallelism.assets/20231105_1747446654.png)



## SIMD Architecture
### XMM Register in SSE
> 本质上说，`XMM Register`就是一个能够储存位宽为`128bit`的大号寄存器，一共有`16`个。
> ![image.png](Data-Level_Parallelism.assets/20231105_1747464789.png)![image.png](Data-Level_Parallelism.assets/20231105_1747492427.png)
> `Packed`的意思就是我们可以同时处理多个数据段。



### SIMD Register in AVX512
> ![image.png](Data-Level_Parallelism.assets/20231105_1747509247.png)![image.png](Data-Level_Parallelism.assets/20231105_1747523613.png)



### WSL Parameter(lscpu)
> ![image.png](Data-Level_Parallelism.assets/20231105_1747541883.png)



# SIMD Parallel Instructions
## SIMD Array Processing
> ![image.png](Data-Level_Parallelism.assets/20231105_1747567914.png)
> 我们可以发现`SIMD`可以极大程度上的缩减我们循环体执行的次数，每个循环体内做的事情会比`SISD`更多。
> ![image.png](Data-Level_Parallelism.assets/20231105_1747585944.png)



## SIMD Matrix Multiplication
> ![](Data-Level_Parallelism.assets/image-20231105204038302.png)




# Vector Sum Example
> [!lab] CS61C Sp23 Lab07 Ex1


## Naive sum
> [!example]
> 直接将所有的元素加起来，使用一个循环实现。
```c
    clock_t start = clock();

    long long int sum = 0;
    for(unsigned int w = 0; w < OUTER_ITERATIONS; w++) {
        for(unsigned int i = 0; i < NUM_ELEMS; i++) {
            if(vals[i] >= 128) {
                sum += vals[i];
            }
        }
    }
    clock_t end = clock();
    printf("Time taken: %Lf s\n", (long double)(end - start) / CLOCKS_PER_SEC);
    return sum;
}
```

## Sum Unrolled
> [!example]
> 使用`Loop Unrolling`技巧实现，减少循环次数，减少在循环上的额外开销。
```c
long long int sum_unrolled(int vals[NUM_ELEMS]) {
    clock_t start = clock();
    long long int sum = 0;

    for(unsigned int w = 0; w < OUTER_ITERATIONS; w++) {
        for(unsigned int i = 0; i < NUM_ELEMS / 4 * 4; i += 4) {
            if(vals[i] >= 128) sum += vals[i];
            if(vals[i + 1] >= 128) sum += vals[i + 1];
            if(vals[i + 2] >= 128) sum += vals[i + 2];
            if(vals[i + 3] >= 128) sum += vals[i + 3];
        }

        // TAIL CASE, for when NUM_ELEMS isn't a multiple of 4
        // NUM_ELEMS / 4 * 4 is the largest multiple of 4 less than NUM_ELEMS
        // Order is important, since (NUM_ELEMS / 4) effectively rounds down first
        for(unsigned int i = NUM_ELEMS / 4 * 4; i < NUM_ELEMS; i++) {
            if (vals[i] >= 128) {
                sum += vals[i];
            }
        }
    }
    clock_t end = clock();
    printf("Time taken: %Lf s\n", (long double)(end - start) / CLOCKS_PER_SEC);
    return sum;
}

```

## Sum SIMD
> [!example]
> 使用`Data-Level Parallelism`实现一行指令多维数据处理。
```c
long long int sum_simd(int vals[NUM_ELEMS]) {
    clock_t start = clock();
    __m128i _127 = _mm_set1_epi32(127); // This is a vector with 127s in it... Why might you need this?
    long long int result = 0; // This is where you should put your final result!
    /* DO NOT MODIFY ANYTHING ABOVE THIS LINE (in this function) */

    for(unsigned int w = 0; w < OUTER_ITERATIONS; w++) {
        /* YOUR CODE GOES HERE */
        // Initialize
        __m128i sum_vec = _mm_setzero_si128();

        for (unsigned int i = 0; i < NUM_ELEMS / 4 * 4; i += 4) {
            // Load four from array
            __m128i tmp = _mm_loadu_si128((__m128i *) (vals + i));
            // Mask the element smaller than 128
            __m128i mask = _mm_cmpgt_epi32(tmp, _127);
            tmp = _mm_and_si128(tmp, mask);
            // Add the the sum vec
            sum_vec = _mm_add_epi32(sum_vec, tmp);
        }
        int tmp_val[4];
        _mm_storeu_si128((__m128i *) tmp_val, sum_vec);

        for (int i = 0; i < 4; i++) {
            result += tmp_val[i]; // This won't cause overflow because we are doing 
            // addition between long long int and int and store the result as a long long int,
            // where long long int result has enough bits to store the tmp_val.
        }
        // result = tmp_val[0] + tmp_val[1] + tmp_val[2] + tmp_val[3]; is not ok, because
        // tmp_val[i] is huge, and any addition operations like tmp_val[i] + tmp_val[j]
        // will cause an overflow(big int + big int), causing the actual result to be smaller than expected.

        /* Hint: you'll need a tail case. */
        for (unsigned int i = NUM_ELEMS / 4 * 4; i < NUM_ELEMS; i++){
            if (vals[i] >= 128) {
                result += vals[i];
            }
        }
    }

    /* DO NOT MODIFY ANYTHING BELOW THIS LINE (in this function) */
    clock_t end = clock();
    printf("Time taken: %Lf s\n", (long double)(end - start) / CLOCKS_PER_SEC);
    return result;
}
```


## Sum SIMD Unrolled
> [!example]
> 结合`SIMD`和`Loop Unrolling`技巧:
```c
long long int sum_simd_unrolled(int vals[NUM_ELEMS]) {
    clock_t start = clock();
    __m128i _127 = _mm_set1_epi32(127);
    long long int result = 0;
    /* DO NOT MODIFY ANYTHING ABOVE THIS LINE (in this function) */

    for(unsigned int w = 0; w < OUTER_ITERATIONS; w++) {
        /* YOUR CODE GOES HERE */
        /* Copy your sum_simd() implementation here, and unroll it */

        __m128i sum_vec = _mm_setzero_si128();

        for (unsigned int i = 0; i < NUM_ELEMS / 16; i++) {
            // Load four from array
            // Unroll 1
            __m128i tmp = _mm_loadu_si128((__m128i *) (vals + i * 16));
            // Mask the element smaller than 128
            __m128i mask = _mm_cmpgt_epi32(tmp, _127);
            tmp = _mm_and_si128(tmp, mask);
            // Add the the sum vec
            sum_vec = _mm_add_epi32(sum_vec, tmp);
            // Unroll 2
            tmp = _mm_loadu_si128((__m128i *) (vals + i * 16 + 4));
            // Mask the element smaller than 128
            mask = _mm_cmpgt_epi32(tmp, _127);
            tmp = _mm_and_si128(tmp, mask);
            // Add the the sum vec
            sum_vec = _mm_add_epi32(sum_vec, tmp);
            // Unroll 3
            tmp = _mm_loadu_si128((__m128i *) (vals + i * 16 + 8));
            // Mask the element smaller than 128
            mask = _mm_cmpgt_epi32(tmp, _127);
            tmp = _mm_and_si128(tmp, mask);
            // Add the the sum vec
            sum_vec = _mm_add_epi32(sum_vec, tmp);
            // Unroll 4
            tmp = _mm_loadu_si128((__m128i *) (vals + i * 16 + 12));
            // Mask the element smaller than 128
            mask = _mm_cmpgt_epi32(tmp, _127);
            tmp = _mm_and_si128(tmp, mask);
            // Add the the sum vec
            sum_vec = _mm_add_epi32(sum_vec, tmp);
        }
        int tmp_val[4];
        _mm_storeu_si128((__m128i *) tmp_val, sum_vec);

        for (int j = 0; j < 4; j++){
            result += tmp_val[j];
        }
        
        /* Hint: you'll need 1 or maybe 2 tail cases here. */
        for (unsigned int i = NUM_ELEMS / 16 * 16; i < NUM_ELEMS; i++){
            if (vals[i] >= 128) {
                result += vals[i];
            }
        }
    }

    /* DO NOT MODIFY ANYTHING BELOW THIS LINE (in this function) */
    clock_t end = clock();
    printf("Time taken: %Lf s\n", (long double)(end - start) / CLOCKS_PER_SEC);
    return result;
}

```

