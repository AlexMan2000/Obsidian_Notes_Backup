> [[CS161 SP24] Lecture 2_ x86 Assembly and Call Stack]([CS161%20SP24]%20Lecture%202_%20x86%20Assembly%20and%20Call%20Stack.pdf)

# C Memory Layout
> [!important]
> Also see [C Memory Layout](../../../Computer_Systems/Machine_Structures/1_C_Language/Memory_Management.md#C%20Memory%20Layout)
> - Stack grows downwards from higher addresses to lower ones.
> - Heap/Static grows upwards from lower addresses to higher ones.
> 
> Consider the following code, where `x`, `y`, `z` are allocated on static memory, since it grows upwards, we have `addr(x) < addr(y) < add(z)`.
```c
int x;
char y[4];
int z;

int main() {
    return 0;
}
```
> [!important] Stack Memory
> Consider the following code, where `x`, `y`, `z` are allocated on stack memory, since it grows downwards, we have `addr(x) > addr(y) > add(z)`.
```c
int main() {
    int x;
    char y[4];
    int z;

    return 0;
}
```
> [!important] Struct
> A **struct** is always treated as a group of variables, no matter what part of memory it is in. Even though the struct here is on the **stack**, which grows downwards, within the struct, `x` has the lowest address, `y` has a higher address, and `z` has the highest address.
> 
> If another variable was declared after the line `struct s foo;`, that variable would be located below `x` on the stack.
```c
struct s {
    int x;        
    char y[4];
    int z;
};

int main() {
    struct s foo;
    
    return 0;
}
```


# X86 CALL Procedures
## Setup
> [!concept]
> There are 11 steps to calling an x86 function and returning. In this example, `main` is the caller function and `foo` is the callee function. In other words, `main` calls the `foo` function.
> 
> Here is the stack before the function is called. ebp and esp point to the top and bottom of the caller stack frame.
> ![](1_X86_Assembly_Call_Stack.assets/image-20240224150232423.png)

> [!code]
```c
int main(void) {
    foo(1, 2);
}

void foo(int a, int b) {
    int bar[4];
}

```

> [!code] Assembly
```assembly
main:
    # Step 1. Push arguments on the stack in reverse order
    push $2
    push $1

    # Steps 2-3. Save old eip (rip) on the stack and change eip
    call foo

    # Execution changes to foo now. After returning from foo:

    # Step 11: Remove arguments from stack
    add $8, %esp

foo:
    # Step 4. Push old ebp (sfp) on the stack
    push %ebp

    # Step 5. Move ebp down to esp
    mov %esp, %ebp

    # Step 6. Move esp down
    sub $16, %esp

    # Step 7. Execute the function (omitted here)

    # Step 8. Move esp
    mov %ebp, %esp

    # Step 9. Restore old ebp (sfp)
    pop %ebp

    # Step 10. Restore old eip (rip)
    pop %eip
```

> [!important]
> Steps 4-6 are sometimes called the _function prologue_, since they must appear at the start of the assembly code of any C function. Similarly, steps 8-10 are sometimes called the _function epilogue_.


## Step 1: Push arguments onto the stack
> [!example]
> **Push arguments onto the stack.** RISC-V passes arguments by storing them in registers, but x86 passes arguments by pushing them onto the stack. Note that esp is decremented as we push arguments onto the stack. Arguments are pushed onto the stack **in reverse order**.
> ![](1_X86_Assembly_Call_Stack.assets/image-20240224150226164.png)




## Step 2: Push Old EIP on Stack
> [!example]
> **Push the old eip (rip) on the stack.** We are about to change the value in the eip register, so we need to save its current value on the stack before we overwrite it with a new value. When we push this value on the stack, it is called the _old eip_ or the _rip_ (return instruction pointer).
> 
> In reality, the value we push on the stack is the current value in eip, incremented by 1 instruction. This is because after the function returns, we want to execute the instruction directly after the instruction eip is currently pointing to
> ![](1_X86_Assembly_Call_Stack.assets/image-20240224150352791.png)


## Step 3: Move EIP
> [!example]
> Now that we’ve saved the old value of eip, we can safely change eip to point to the instructions for the callee function.
> ![](1_X86_Assembly_Call_Stack.assets/image-20240224150433118.png)



## Step 4: Push Old EBP on Stack
> [!example]
> We are about to change the value in the ebp register, so we need to save its current value on the stack before we overwrite it with a new value. When we push this value on the stack, it is called the _old ebp_ or the _sfp_ (saved frame pointer). Note that esp has been decremented because we pushed a new value on the stack.![](1_X86_Assembly_Call_Stack.assets/image-20240224150608221.png)


## Step 5: Move EBP to ESP
> [!example]
> Now that we’ve saved the old value of ebp, we can safely change ebp to point to the top of the new stack frame. The top of the new stack frame is where esp is currently pointing, since we are about to allocate new space below esp for the new stack frame.![](1_X86_Assembly_Call_Stack.assets/image-20240224150640425.png)


## Step 6: Move ESP Down
> [!example]
> Now we can allocate new space for the new stack frame by decrementing esp. The compiler looks at the complexity of the function to determine how far esp should be decremented. For example, a function with only a few local variables doesn’t require too much space on the stack, so esp will only be decremented by a few bytes. On the other hand, if a function declares a large array as a local variable, esp will need to be decremented by a lot to fit the array on the stack.
> ![](1_X86_Assembly_Call_Stack.assets/image-20240224150714664.png)



## Step 7: Execute the function
> [!example]
> Local variables and any other necessary data can now be saved in the new stack frame. Additionally, since **ebp is always pointing at the top of the stack frame**, we can use it as **a point of reference** to find other variables on the stack. For example, the arguments will be located starting at the address stored in ebp, plus 8.
> ![](1_X86_Assembly_Call_Stack.assets/image-20240224150812302.png)


## Step 8: Move ESP To EBP
> [!example]
> Once the function is ready to return, **we increment esp to point to the top of the stack frame (ebp).** 
> 
> This effectively erases the stack frame, since the stack frame is now located below esp. (Anything on the stack below esp is undefined.)
> ![](1_X86_Assembly_Call_Stack.assets/image-20240224150848257.png)


## Step 9: Restore the old EBP
> [!example]
> The next value on the stack is the sfp, the old value of ebp before we started executing the function. We pop the sfp off the stack and store it back into the ebp register. This returns ebp to its old value before the function was called.![](1_X86_Assembly_Call_Stack.assets/image-20240224150924692.png)


## Step 10: Restore the old EIP
> [!example]
> The next value on the stack is the rip, the old value of eip before we started executing the function. We pop the rip off the stack and store it back into the eip register. This returns eip to its old value before the function was called.
> 
> In reality, eip is now pointing at the instruction directly after the old instruction it was pointing to. This lets us continue executing the caller function right after where we left off to call the function.![](1_X86_Assembly_Call_Stack.assets/image-20240224151021371.png)


## Step 11: Remove Arguments from the Stack
> [!example]
> Since the function call is over, we don’t need to store the arguments anymore. We can remove them by incrementing esp (recall that anything on the stack below esp is undefined).![](1_X86_Assembly_Call_Stack.assets/image-20240224151052532.png)


## Summary
> [!summary]
> ![](1_X86_Assembly_Call_Stack.assets/image-20240224153102860.png)


# Chapter Exercises
## Registers and Addresses (GDB)
> [!example] Win12 Homework 1
> ![](1_X86_Assembly_Call_Stack.assets/image-20240226111101528.png)![](1_X86_Assembly_Call_Stack.assets/image-20240226111109219.png)![](1_X86_Assembly_Call_Stack.assets/image-20240226111118098.png)![](1_X86_Assembly_Call_Stack.assets/image-20240226111124969.png)![](1_X86_Assembly_Call_Stack.assets/image-20240226111131938.png)![](1_X86_Assembly_Call_Stack.assets/image-20240226111246900.png)

















## Code Analysis
### Stack Diagram
> [!example] Sp24 Disc01 P2
> ![](1_X86_Assembly_Call_Stack.assets/image-20240225111524983.png)![](1_X86_Assembly_Call_Stack.assets/image-20240225111530993.png)![](1_X86_Assembly_Call_Stack.assets/image-20240225111535736.png)


### Printf Function
> [!example] Sp24 ExamPrep01 P3
> ![](1_X86_Assembly_Call_Stack.assets/image-20240225113904482.png)![](1_X86_Assembly_Call_Stack.assets/image-20240225113913706.png)





## Concept Check
> [!example] Sp24 Disc01 P3
> See [cheatsheet](cheatsheet.pdf) for references.
> ![](1_X86_Assembly_Call_Stack.assets/image-20240225112101802.png)![](1_X86_Assembly_Call_Stack.assets/image-20240225112109174.png)



