

# riscv.h
## Useful Macro
> [!code]
> ![](XV6-Memory.assets/image-20240814163424543.png)
```c
#define PGROUNDUP(sz)  (((sz)+PGSIZE-1) & ~(PGSIZE-1))
#define PGROUNDDOWN(a) (((a)) & ~(PGSIZE-1))
```
