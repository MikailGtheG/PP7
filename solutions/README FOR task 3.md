# Task 3: Modular Linking with `extern`

In this task, we create a simple modular program in C, using separate files for functions and `extern` to link them manually.  
We write the code in two files: `add.c` and `main.c`, then compile and link them step by step.

---

## Step 1: Write the Source Files

### `add.c`
```c
// add.c
int add(int a, int b) {
    return a + b;
}
```

This file contains the function definition.  
It will be compiled separately into an object file.

---

### `main.c`
```c
// main.c
#include <stdio.h>

// This tells the compiler the function exists in another file
extern int add(int, int);

int main(void) {
    int sum = add(5, 7);
    printf("5 + 7 = %d\n", sum);
    return 0;
}
```

Here, we use `extern` to declare the function `add()` from `add.c`.  
This allows the linker to find it during the linking stage.

---

## Step 2: Compile Each File Separately

```bash
gcc -c solutions/add.c -o solutions/add.o
gcc -c solutions/main.c -o solutions/main.o
```

What happens:
- `-c` tells gcc to compile only (no linking).
- Each `.c` file becomes an `.o` object file.
- This is useful in larger projects, as only changed files need to be recompiled.

---

## Step 3: Manual Linking

```bash
gcc solutions/add.o solutions/main.o -o solutions/add_example
```

What happens:
- We link the object files into a final executable.
- The linker connects the call to `add()` in `main.c` with its definition in `add.c`.

---

## Step 4: Run the Program

```bash
./solutions/add_example
```

Expected output:
```
5 + 7 = 12
```

---

## Notes

### The role of `extern`

- `extern` informs the compiler that a function exists in another file.
- It is necessary for modular programming and separate compilation.

### Why separate compilation?

- When only one source file changes, we can recompile only that file.
- This saves time in bigger codebases.

### Manual vs. automatic linking

| Type | Command | Description |
|------|---------|-------------|
| Manual | `gcc -c file.c -o file.o` + `gcc file.o ... -o exe` | More control, better for bigger projects |
| Automatic | `gcc file1.c file2.c -o exe` | Easier and faster for small programs |

---

## Terminal Workflow Example

```bash
mikailerarslan@mikailerarslan-HP-Z400-Workstation:~/PP7/solutions$ nano add.c
mikailerarslan@mikailerarslan-HP-Z400-Workstation:~/PP7/solutions$ nano main.c
mikailerarslan@mikailerarslan-HP-Z400-Workstation:~/PP7/solutions$ cd ..
mikailerarslan@mikailerarslan-HP-Z400-Workstation:~/PP7$ gcc -c solutions/add.c -o solutions/add.o
mikailerarslan@mikailerarslan-HP-Z400-Workstation:~/PP7$ gcc -c solutions/main.c -o solutions/main.o
mikailerarslan@mikailerarslan-HP-Z400-Workstation:~/PP7$ gcc solutions/add.o solutions/main.o -o solutions/add_example
mikailerarslan@mikailerarslan-HP-Z400-Workstation:~/PP7$ ./solutions/add_example
5 + 7 = 12
```

---
