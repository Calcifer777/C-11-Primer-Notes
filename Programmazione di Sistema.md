# Argomenti

- Gestione accessi ai file
  - Aprire un file
  - Leggere un file (carattere, stringa, blocco)
  - Scrivere un file
  - Chiudere un file
- Operazioni sulle directories
  - Spostare un file
  - Cambiare il nome di un file
  - Spostare o eliminare una directory
- Operazioni sui processi
  - Generare processi slave e master
  - Terminare processi
  - Sostituire il codice di un processo in esecuzion
  
# File

I file sono identificati da:
- Nome
- Directory
- Lunghezza (# byte)
- Data/ora creazione
- Data/ora ultima modifica
- Diritti di accesso (r, w, x)

## Functions

| Function | Syntax |
| -------- | --------- |
| [`fopen`](http://www.cplusplus.com/reference/cstdio/fopen/) | `FILE * fopen(const char filename, const char * mode)` |
| [`fclose`](http://www.cplusplus.com/reference/cstdio/fclose/) | `int fclose ( FILE * stream );` |
| [`remove`](http://www.cplusplus.com/reference/cstdio/remove/) | `int remove ( const char * filename );` | 
| [`rename`](http://www.cplusplus.com/reference/cstdio/rename/) | `int rename ( const char * oldname, const char * newname );` |
| [`feof`](http://www.cplusplus.com/reference/cstdio/feof/)     | `int feof ( FILE * stream );` |
| [`ferror`](http://www.cplusplus.com/reference/cstdio/ferror/) | `int ferror ( FILE * stream );` |
| [`clearerr`](http://www.cplusplus.com/reference/cstdio/clearerr/) | `void clearerr ( FILE * stream );` |
| [`fseek`](http://www.cplusplus.com/reference/cstdio/fseek/) | `int fseek ( FILE * stream, long int offset, int origin );` |
| [`ftell`](http://www.cplusplus.com/reference/cstdio/ftell/) | `long int ftell ( FILE * stream );` |
| [`rewind`](http://www.cplusplus.com/reference/cstdio/rewind/) | `int fseek ( FILE * stream, long int offset, int origin );` |


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

**`fclose`**

Closes the file associated with the stream and disassociates it. Returns `0` if the stream is successfully closed.

All internal buffers associated with the stream are disassociated from it and flushed: the content of any unwritten output buffer is written and the content of any unread input buffer is discarded.

Even if the call fails, the stream passed as parameter will no longer be associated with the file nor its buffers.

**`rename`**

Changes the name of the file or directory specified by oldname to newname.

This is an operation performed directly on a file; No streams are involved in the operation.

If oldname and newname specify different paths and this is supported by the system, the file is moved to the new location.

**`remove`**

Deletes the file whose name is specified in filename. If the file is successfully deleted, a zero value is returned. On failure, a nonzero value is returned. 

**`fseek`**

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
  
  
  
  
  
  
