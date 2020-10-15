# File Access

Doing everything in the program's memory and talking only to the standard I/O is cool, but what if a user needs to save his task in a file or read / write from a preexisting file on the disk. 

We fulfil this need by creating programs that can access a file that is not already connected to the program. Such a program is capable of creating, reading, updating and deleting data on the disk.

## File Structure

File structure is the data representation of files in the secondary storage along with associated operations. It helps in organising the data to minimise access time and storage space.

A file structure allows applications to read, write and modify data efficiently. It might also support finding the data that matches some search criteria or reading through the data in some particular order.

## File Format / Type

A file format or file type is a standard way in which information is encoded for storage in a computer file. It specifies how bits are used to encode information in a digital storage medium. 

File formats may be either proprietary or free and may be either unpublished or open.

Some file formats are designed for very particular types of data: `.png` files, for example, store bit-mapped images using lossless data compression. 

Other file formats, however, are designed for storage of several different types of data: the `.ogg` format can act as a container for different types of multimedia including any combination of audio and video, with or without text (such as subtitles), and metadata. 

A text file can contain any stream of characters, including possible control characters, and is encoded in one of various character encoding schemes. Some file formats, such as HTML, scalable vector graphics, and the source code of computer software are text files with defined syntaxes that allow them to be used for specific purposes.

## Stream

A stream is basically a sequence of data. It's a logical entity through which all data we use in our program flows. 

A stream can be thought of as a channel connecting a processor/logic unit (where data is processed according to the instructions) and the file or device from which input/output is taking place.

> **Rationale**
>
> The people designing C wanted a uniform way of interfacing with different sources of sequential data, like files, sockets, keyboards, USB ports, printers or whatever.
>
> So they designed one interface that could be applied to all of them. This interface uses properties that are common to all of them.
>
> To make it easier to talk about the things that could be used through the interface they gave the things a generic name, *streams*.
>
> The beauty of using the same interface is that the same code can be used to read from a file as from the keyboard or a socket.
>
> [- Klas Lindback, Stack Overflow](https://stackoverflow.com/a/38653267)

For historical reasons, the type of the C data structure that represents a stream is called `FILE` rather than “stream”. Since most of the library functions deal with objects of type `FILE *`, sometimes the term *file pointer* is also used to mean “stream”.

### FILE

The type `FILE`, defined in `<stdio.h>`, is used to connect to files on the storage for access.

A `FILE` object holds all of the internal information about the connection to the associated file, including such things as the location of a buffer, the current character position in the buffer, whether the file is being read or written, and whether errors or end-of-file have occurred.

`FILE` objects are allocated and managed internally by the file I/O library functions. Your programs should deal only with [*file pointers*](#file-pointer) (that is, `FILE *` values) rather than the `FILE` objects themselves.

#### File Pointer

A pointer to a `FILE` object is called a *file pointer*. This is how we declare it:

```c
FILE *fp;
```

### Types of streams

All input and output functions in standard C, operate on data streams.

Streams can be divided[^1] into **text** streams and **binary** streams.

When you open a stream, you can specify either a text stream or a binary stream. You indicate that you want a binary stream by specifying the 'b' modifier in the *opentype* argument to [`fopen`](). Without this option, `fopen` opens the file as a text stream.

#### Text Stream

- A text stream is an ordered sequence of characters composed into lines (that is, zero or more characters plus a terminating `'\n'`).
- On some systems, it might fail to handle lines more than 254 characters long (including the terminating newline character).
- A text stream on some systems can contain only printable characters, horizontal tab characters, and newlines, and so it may not support other characters.
- Space characters that are written immediately preceding a newline character in a text stream may disappear when the file is read in again.
- Whether the last line requires a terminating `'\n'` is implementation-defined.  Characters may have to be added, altered, or deleted on input and output to conform to the conventions for representing text in the OS (in particular, C streams on Windows OS convert `\n` to `\r\n` on output, and convert `\r\n` to `\n` on input).[^2]

#### Binary Stream

- A binary stream is an ordered sequence of characters that can transparently record internal data.
- The is no limitation on the number of characters in a binary stream. 
- Binary streams can handle any character value.
- Data read in from a binary stream always equals to the data that were earlier written out to that stream.
- Implementations are only allowed to append a number of null characters to the end of the stream.

## File Operations  and File Handling Functions

### Opening a File

Opening a file with the `fopen` function creates a new stream and establishes a connection between the stream and a file. This may involve creating a new file.

#### `fopen`

Declared in: `<stdio.h>`

Usage syntax: `fopen (filename, opentype);`

Prototype: `FILE* fopen (const char *filename, const char *opentype);`

The `fopen` function opens a stream for I/O to the file `filename`, and returns a pointer (`FILE*`) to the stream.

The `opentype` argument is a string that controls how the file is opened and specifies attributes of the resulting stream. It must begin with one of the following sequences of characters:

- ‘r’

  Open an existing file for reading only.

- ‘w’

  Open the file for writing only. If the file already exists, it is truncated to zero length. Otherwise a new file is created.

- ‘a’

  Open a file for append access; that is, writing at the end of file only. If the file already exists, its initial contents are unchanged and output to the stream is appended to the end of the file. Otherwise, a new, empty file is created.

- ‘r+’

  Open an existing file for both reading and writing. The initial contents of the file are unchanged and the initial file position is at the beginning of the file.

- ‘w+’

  Open a file for both reading and writing. If the file already exists, it is truncated to zero length. Otherwise, a new file is created.

- ‘a+’

  Open or create file for both reading and appending. If the file exists, its initial contents are unchanged. Otherwise, a new file is created. The initial file position for reading is at the beginning of the file, but output is always appended to the end of the file.

As you can see, ‘+’ requests a stream that can do both input and output. When using such a stream, you must call `fflush` or a file positioning function such as `fseek` when switching from reading to writing or vice versa. Otherwise, internal buffers might not be emptied properly.

### Closing a File

When a stream is closed with `fclose`, the connection between the stream and the file is cancelled. After you have closed a stream, you cannot perform any additional operations on it.

#### `fclose`

Declared in: `<stdio.h>`

Usage syntax: `fclose (stream);`

Prototype: `int fclose (FILE *stream);`

This function causes stream to be closed and the connection to the corresponding file to be broken. Any buffered output is written and any buffered input is discarded. 

The `fclose` function returns a value of `0` if the file was closed successfully, and `EOF` if an error was detected.

It is important to check for errors when you call `fclose` to close an output stream, because real, everyday errors can be detected at this time. For example, when `fclose` writes the remaining buffered output, it might get an error because the disk is full. Even if you know the buffer is empty, errors can still occur when closing a file if you are using NFS.

### Writing Output

Here are some functions for performing character and line oriented output.

#### `fputc`

Declared in: `<stdio.h>`

Usage syntax: `fputc (c, stream);`

Prototype:`int fputc (int c, FILE *stream);`

The `fputc` function converts the character `c` to type `unsigned char`, and writes it to the stream stream. `EOF` is returned if a write error occurs; otherwise the character `c` is returned.

#### `putc`

Declared in: `<stdio.h>`

Usage syntax: `putc (c, stream);`

Prototype: `int putc (int c, FILE *stream);`

This is just like `fputc`, except that most systems implement it as a macro, making it faster. One consequence is that it may evaluate the stream argument more than once, which is an exception to the general rule for macros. `putc` is usually the best function to use for writing a single character.

#### `fputs`

Declared in: `<stdio.h>`

Usage syntax: `fputs (s, stream);`

Prototype: `fputs (const char *s, FILE *stream);`

The function `fputs` writes the string s to the stream stream. The terminating null character is not written. This function does *not* add a newline character, either. It outputs only the characters in the string.

This function returns `EOF` if a write error occurs, and otherwise a non-negative value.

For example:

```c
fputs ("Are ", stdout);
fputs ("you ", stdout);
fputs ("hungry?\n", stdout);
```

outputs the text `Are you hungry?` followed by a newline.

### Reading a Character

Here are some functions for performing character-oriented input.

#### `fgetc`

Declared in: `<stdio.h>`

Usage syntax: `fgetc (stream);`

Prototype: `int fgetc (FILE *stream);`

This function reads the next character as an `unsigned char` from the stream stream and returns its value, converted to an `int`. If an end-of-file condition or read error occurs, `EOF` is returned instead.

#### `getc`

Declared in: `<stdio.h>`

Usage syntax: `getc (stream);`

Prototype: `int getc (FILE *stream);`

This is just like `fgetc`, except that it is permissible (and typical) for it to be implemented as a macro that evaluates the stream argument more than once. `getc` is often highly optimised, so it is usually the best function to use to read a single character.

### Reading a Line

Since many programs interpret input on the basis of lines, it is convenient to have functions to read a line of text from a stream.

#### `fgets`

Declared in: `<stdio.h>`

Usage syntax: `fgets (s, count, stream);`

Prototype: `char * fgets (char *s, int count, FILE *stream);`

The `fgets` function reads characters from the stream stream up to and including a newline character and stores them in the string s, adding a null character to mark the end of the string. You must supply count characters worth of space in s, but the number of characters read is at most count - 1. The extra character space is used to hold the null character at the end of the string.

If the system is already at end of file when you call `fgets`, then the contents of the array s are unchanged and a null pointer is returned. A null pointer is also returned if a read error occurs. Otherwise, the return value is the pointer s.

**Warning:** If the input data has a null character, you can’t tell. So don’t use `fgets` unless you know the data cannot contain a null. Don’t use it to read files edited by the user because, if the user inserts a null character, you should either handle it properly or print a clear error message. It is recommended to use `getline` instead of `fgets`.

#### `getline`

Note: This function is a GNU extension, but it is the recommended way to read lines from a stream. The alternative standard functions are unreliable.

Declared in: `<stdio.h>`.

Usage syntax: `getline (lineptr, n, stream);`

Prototype: `ssize_t getline (char **lineptr, size_t *n, FILE *stream);`

This function reads an entire line from stream, storing the text (including the newline and a terminating null character) in a buffer and storing the buffer address in `*lineptr`.

Before calling `getline`, you should place in `*lineptr` the address of a buffer `*n` bytes long, allocated with `malloc`. If this buffer is long enough to hold the line, `getline` stores the line in this buffer. Otherwise, `getline` makes the buffer bigger using `realloc`, storing the new buffer address back in `*lineptr` and the increased size back in `*n`.

If you set `*lineptr` to a null pointer, and `*n` to zero, before the call, then `getline` allocates the initial buffer for you by calling `malloc`. This buffer remains allocated even if `getline` encounters errors and is unable to read any bytes.

In either case, when `getline` returns, `*lineptr` is a `char *` which points to the text of the line.

When `getline` is successful, it returns the number of characters read (including the newline, but not including the terminating null). This value enables you to distinguish null characters that are part of the line from the null character inserted as a terminator.

If an error occurs or end of file is reached without any bytes read, `getline` returns `-1`.

### Others

Error and end-of-file status can be tested with the `ferror` and `feof` functions.



---



[^1]: GNU systems and other POSIX-compatible operating systems organise all files as uniform sequences of characters. However, some other systems make a distinction between files containing text and files containing binary data.
[^2]: `\r` - carriage return, `\n` - line feed

