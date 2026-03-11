# get_next_line

A C function that reads a file descriptor line by line.

## Description

`get_next_line` reads from a given file descriptor and returns the next line on each call. It uses a static variable to keep track of remaining data between calls, allowing sequential reading of lines from a file or standard input.

### Function Prototype

```c
char *get_next_line(int fd);
```

### Parameters

- `fd` — the file descriptor to read from.

### Return Value

- A pointer to the line that was read (including the terminating `\n` character, if present).
- `NULL` when there is nothing more to read or an error occurred.

> The caller is responsible for freeing the returned string.

## Files

| File | Description |
|------|-------------|
| `get_next_line.c` | Core `get_next_line` function |
| `get_next_line_utils.c` | Helper functions (`ft_strjoin`, `ft_substr`, `ft_strdup`, etc.) |
| `get_next_line.h` | Header file with function prototypes and `BUFFER_SIZE` definition |

### Bonus

The bonus version supports reading from **multiple file descriptors** simultaneously (up to 1024), so you can alternate between different files without losing track of each one's reading position.

| File | Description |
|------|-------------|
| `get_next_line_bonus.c` | Multi-fd version of `get_next_line` |
| `get_next_line_utils_bonus.c` | Helper functions (same as the regular version) |
| `get_next_line_bonus.h` | Header file for the bonus version |

## Usage

Include the header and compile the source files with your project:

```c
#include "get_next_line.h"

int main(void)
{
    int   fd;
    char  *line;

    fd = open("example.txt", O_RDONLY);
    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

### Compilation

```sh
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c main.c
```

You can set `BUFFER_SIZE` at compile time with the `-D` flag to control how many bytes are read per `read()` call. If omitted, it defaults to `3`.
