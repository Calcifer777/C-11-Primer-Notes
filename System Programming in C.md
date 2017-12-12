
- Operazioni sui processi
  - Generare processi slave e master
  - Terminare processi
  - Sostituire il codice di un processo in esecuzion
  
# Files and Operations on Files

Files attributes:
- Name
- Directory
- Length (# byte)
- Date/hour created
- Date/hour last modified
- Access profiles (r, w, x)

## Functions

| Function | Syntax | Description |
| -------- | ------ | ----------- |
| [`fopen`](http://www.cplusplus.com/reference/cstdio/fopen/) | `FILE * fopen(const char filename, const char * mode)` | Opens the file whose name is specified in the parameter filename and associates it with a stream that can be identified in future operations by the FILE pointer returned |
| [`fclose`](http://www.cplusplus.com/reference/cstdio/fclose/) | `int fclose ( FILE * stream );` | Closes the file associated with the stream and disassociates it. Even if the call fails, the stream passed as parameter will no longer be associated with the file nor its buffers |
| [`remove`](http://www.cplusplus.com/reference/cstdio/remove/) | `int remove ( const char * filename );` | |
| [`rename`](http://www.cplusplus.com/reference/cstdio/rename/) | `int rename ( const char * oldname, const char * newname );` | |
| [`feof`](http://www.cplusplus.com/reference/cstdio/feof/)     | `int feof ( FILE * stream );` | |
| [`ferror`](http://www.cplusplus.com/reference/cstdio/ferror/) | `int ferror ( FILE * stream );` | |
| [`clearerr`](http://www.cplusplus.com/reference/cstdio/clearerr/) | `void clearerr ( FILE * stream );` | |
| [`fseek`](http://www.cplusplus.com/reference/cstdio/fseek/) | `int fseek ( FILE * stream, long int offset, int origin );` | |
| [`ftell`](http://www.cplusplus.com/reference/cstdio/ftell/) | `long int ftell ( FILE * stream );` | |
| [`rewind`](http://www.cplusplus.com/reference/cstdio/rewind/) | `void rewind ( FILE * stream );` | |
| [`fflush`](http://www.cplusplus.com/reference/cstdio/fflush/) | `int fflush ( FILE * stream );` | |

**`fopen`**

| Mode | Result |
| ---- | ------ |
| `"r"` | **read**: open file for input operations. The file must exist |
| `"w"` | **write**: create an empty file for output operations. If a file with the same name already exists, its contents are discarded and the file is treated as a new empty file | 
| `"a"` | **append**: open file for output at the end of a file. Output operations always write data at the end of the file, expanding it. Repositioning operations (fseek, fsetpos, rewind) are ignored. The file is created if it does not exist. |
| `"r+"` | **read/update**: open a file for update (both for input and output). The file must exist. |
| `"w+"` | **write/update**: create an empty file and open it for update (both for input and output). If a file with the same name already exists its contents are discarded and the file is treated as a new empty file. |
| `"a+"` | **append**: Open a file for update (both for input and output) with all output operations writing data at the end of the file. Repositioning operations (fseek, fsetpos, rewind) affects the next input operations, but output operations move the position back to the end of file. The file is created if it does not exist. |

Use `"b"` at the end of the `mode` options to open a file in binary mode.

Use `"x"` to force the function to fail if the file already exist, instead of overwriting it.

Returns NULL if the file does not exist.

### `rename`

Changes the name of the file or directory specified by oldname to newname.

This is an operation performed directly on a file; No streams are involved in the operation.

If oldname and newname specify different paths and this is supported by the system, the file is moved to the new location.

### `remove`

Deletes the file whose name is specified in filename. If the file is successfully deleted, a zero value is returned. On failure, a nonzero value is returned. 

### `fseek`

Sets the position indicator associated with the stream to a new position.

For streams open in binary mode, the new position is defined by adding offset to a reference position specified by origin.

For streams open in text mode, offset shall either be zero or a value returned by a previous call to ftell, and origin shall necessarily be SEEK_SET.

offset:
- Binary files: Number of bytes to offset from origin.
- Text files: Either zero, or a value returned by ftell.

origin:
- Position used as reference for the offset. It is specified by one of the following constants defined in <cstdio> exclusively to be used as arguments for this function:
  
|Constant	| Reference position |
| ------- | ------------------ |
| SEEK_SET | Beginning of file |
| SEEK_CUR | Current position of the file pointer |
| SEEK_END | End of file * |
  
### `ftell`

Returns the current value of the position indicator of the stream.

For binary streams, this is the number of bytes from the beginning of the file.

### `rewind`  
  
Sets the position indicator associated with stream to the beginning of the file.

The end-of-file and error internal indicators associated to the stream are cleared after a successful call to this function, and all effects from previous calls to ungetc on this stream are dropped.

On streams open for update (read+write), a call to rewind allows to switch between reading and writing.

### `fflush`  

If the given stream was open for writing (or if it was open for updating and the last i/o operation was an output operation) any unwritten data in its output buffer is written to the file.

If stream is a null pointer, all such streams are flushed.

# Reading input

## Functions

| Function | Syntax |
| -------- | --------- |
| [`fgetc`](http://www.cplusplus.com/reference/cstdio/fgetc/) | `int fgetc ( FILE * stream );` |
| [`fputc`](http://www.cplusplus.com/reference/cstdio/fputc/) | `int fputc ( int character, FILE * stream );` |
| [`fgets`](http://www.cplusplus.com/reference/cstdio/fgets/) | `char * fgets ( char * str, int num, FILE * stream );` |
| [`fputs`](http://www.cplusplus.com/reference/cstdio/fputs/) | `int fputs ( const char * str, FILE * stream );` |
| [`fread`](http://www.cplusplus.com/reference/cstdio/fread) |`size_t fread ( void * ptr, size_t size, size_t count, FILE * stream );` |
| [`fwrite`](http://www.cplusplus.com/reference/cstdio/fwrite/) | `size_t fwrite ( const void * ptr, size_t size, size_t count, FILE * stream );` |

## `fgetc`

Returns the character currently pointed by the internal file position indicator of the specified stream. The internal file position indicator is then advanced to the next character.

If the stream is at the end-of-file when called, the function returns EOF and sets the end-of-file indicator for the stream (feof).

If a read error occurs, the function returns EOF and sets the error indicator for the stream (ferror).

## `fputc`

Writes a character to the stream and advances the position indicator.

The character is written at the position indicated by the internal position indicator of the stream, which is then automatically advanced by one.

## `fgets`

Reads characters from stream and stores them as a C string into str until (num-1) characters have been read or either a newline or the end-of-file is reached, whichever happens first.

A newline character makes fgets stop reading, but it is considered a valid character by the function and included in the string copied to str.

## `fputs`

Writes the C string pointed by str to the stream.

The function begins copying from the address specified (str) until it reaches the terminating null character ('\0'). This terminating null-character is not copied to the stream.

## `fread`

Reads an array of count elements, each one with a size of size bytes, from the stream and stores them in the block of memory specified by ptr.

The position indicator of the stream is advanced by the total amount of bytes read.

## `fwrite`

Writes an array of count elements, each one with a size of size bytes, from the block of memory pointed by ptr to the current position in the stream.

The position indicator of the stream is advanced by the total number of bytes written.

Internally, the function interprets the block pointed by ptr as if it was an array of (size * count) elements of type unsigned char, and writes them sequentially to stream as if fputc was called for each byte

# I/O functions

| Function | Syntax | Description |
| -------- | ------ | ----------- |
| [`scanf`](http://www.cplusplus.com/reference/cstdio/scanf/) | `int scanf ( const char * format, ... );` | |
| [`printf`](http://www.cplusplus.com/reference/cstdio/printf/) | `int printf ( const char * format, ... );` | |
| [`sscanf`](http://www.cplusplus.com/reference/cstdio/sscanf/) | `int sscanf ( const char * s, const char * format, ...);` | |
| [`sprintf`](http://www.cplusplus.com/reference/cstdio/sprintf/) | `int sprintf ( char * str, const char * format, ... );` | |
| [`fscanf`](http://www.cplusplus.com/reference/cstdio/fscanf/) | `int fscanf ( FILE * stream, const char * format, ... );`| |
| [`fprintf`](http://www.cplusplus.com/reference/cstdio/fprintf/) | `int fprintf ( FILE * stream, const char * format, ... );` | Writes a string pointed by format to the stream|

Format specifier: `%[*][width][length]specifier`

Note: use always `fgets(string_to_fill, buffer_size, stdin)` instead of `scanf` to prevent bufferoverflow.

Examples:

```c++
FILE *fp;
fp = fopen("test.txt", "w+");
fputs("This is the content of the file test.txt.\n", fp);
fseek(fp, 0, SEEK_SET);
size_t BUFF_SIZE = 50;
char str[BUFF_SIZE];
printf("CURR_POS: %d\n", ftell(fp));
fscanf(fp, "%[^\n]", str);
printf("%s", str);
return 0;
```
