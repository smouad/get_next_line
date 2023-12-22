# Get_Next_Line Project

Welcome to my implementation of the Get_Next_Line (GNL) project for 42 School. The objective of this C programming project is to create a function that reads from a file descriptor and returns a line ending with a newline character.

## Description

`get_next_line` is an individual project at 42 that basically teaches you how to use static variables in C to read the contents of a file or stdin one line at a time, regardless of the length of the line.

## Features

- Handles reading from multiple file descriptors.
- Works with a variable buffer size.
- Handles reading from text files, standard input, or even redirection.

## Static Variables

In the context of `get_next_line`, a static variable plays a crucial role. Unlike regular local variables, which lose their data as soon as the function scope is exited, static variables preserve their values between multiple function calls. This characteristic is essential for managing the sporadic nature of line lengths and partially-read buffers.

Example of a static variable declaration in `get_next_line`:

```c
static char *remainder;
```

This static variable remainder can be used to store any characters that are read from the file descriptor but do not yet form a complete line.

## Installation

To compile the `get_next_line` library, clone the repo and run the appropriate commands:

```bash
git clone https://github.com/smouad/get_next_line
cd get_next_line
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=32 get_next_line.c get_next_line_utils.c
```

Note: You can adjust BUFFER_SIZE as you see fit.
Usage

Include the header get_next_line.h in your C project to use the function.

```c
#include "get_next_line.h"
```

## open(2)
The `open` function is a system call used to open a file descriptor for a file. Here’s how to use it with get_next_line

You provide the file path, and existing one or a a file youwilling to create, and the flags as parameters. The flag O_RDONLY opens the file descriptor for reading only O_CREATE creates a new file if it doesn't exist.

you can check man 2 open or visite this link [open(2)](https://man7.org/linux/man-pages/man2/open.2.html)

```c
#include <fcntl.h>
#include <stdio.h>

int main()
{
    /* you can either give the path to your existing file 
    or you can give a name of a new file to create 
    but make sure to add the O_CREATE flag*/
    int fd = open("path_to_your_file", O_RDONLY);
    char *line = get_next_line(fd);

    while (line) {
        // Use the line for something
        // exmpl print the line
        printf("%s", line);
        free(line);
        line = get_next_line(fd);
    }

    close(fd);
}
```

Testing

You can write your own main function or use the provided test files to check the functionality of get_next_line.
Contributing

Useful Resources

- [Input-output system calls in C](https://www.geeksforgeeks.org/input-output-system-calls-c-create-open-close-read-write/)
- [Static Variables in C](https://www.geeksforgeeks.org/static-variables-in-c/)
- [C Static Variables - When and How to Use]()
