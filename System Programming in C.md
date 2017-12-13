

# Files and Operations on Files

Source: C Programming, a modern approach ch. 22

## Streams

The term stream means any source of input or destination for output.

**Input redirection**: when executing a program from command line, reads from a file instead of from keyboard. E.g. `test.exe <input.dat`

**Output redirection**: when executing a program from command line, writes to a file instead of to the console. E.g. `test.exe >ouput.dat`

### Text and Binary Files



## Functions

| Function | Syntax | Description |
| -------- | ------ | ----------- |
| [`fopen`](http://www.cplusplus.com/reference/cstdio/fopen/) | `FILE * fopen(const char filename, const char * mode)` | Opens the file whose name is specified in the parameter filename and associates it with a stream that can be identified in future operations by the FILE pointer returned |
| [`fclose`](http://www.cplusplus.com/reference/cstdio/fclose/) | `int fclose ( FILE * stream );` | Closes the file associated with the stream and disassociates it. Even if the call fails, the stream passed as parameter will no longer be associated with the file nor its buffers |
| [`remove`](http://www.cplusplus.com/reference/cstdio/remove/) | `int remove(const char *filename);` | Deletes the file whose name is specified in filename. If the file is successfully deleted, a zero value is returned |
| [`rename`](http://www.cplusplus.com/reference/cstdio/rename/) | `int rename(const char *oldname, const char *newname );` | Changes the name of the file or directory specified by oldname to newname. This is an operation performed directly on a file; no streams are involved in the operation. If oldname and newname specify different paths and this is supported by the system, the file is moved to the new location |
| [`feof`](http://www.cplusplus.com/reference/cstdio/feof/)     | `int feof ( FILE * stream );` | Checks whether the end-of-File indicator associated with stream is set, returning a value different from zero if it is. |
| [`ferror`](http://www.cplusplus.com/reference/cstdio/ferror/) | `int ferror ( FILE * stream );` | Checks if the error indicator associated with stream is set, returning a value different from zero if it is. |
| [`clearerr`](http://www.cplusplus.com/reference/cstdio/clearerr/) | `void clearerr ( FILE * stream );` | Resets both the error and the eof indicators of the stream. |
| [`fseek`](http://www.cplusplus.com/reference/cstdio/fseek/) | `int fseek ( FILE * stream, long int offset, int origin );` | Sets the position indicator associated with the stream to a new position. For streams open in binary mode, the new position is defined by adding offset to a reference position specified by origin. For streams open in text mode, offset shall either be zero or a value returned by a previous call to ftell, and origin shall necessarily be SEEK_SET. |
| [`ftell`](http://www.cplusplus.com/reference/cstdio/ftell/) | `long int ftell ( FILE * stream );` | Returns the current value of the position indicator of the stream. For binary streams, this is the number of bytes from the beginning of the file. |
| [`rewind`](http://www.cplusplus.com/reference/cstdio/rewind/) | `void rewind ( FILE * stream );` | Sets the position indicator associated with stream to the beginning of the file. The EOF and error internal indicators  are cleared. On streams open for update (read+write), switches between reading and writing. |
| [`fflush`](http://www.cplusplus.com/reference/cstdio/fflush/) | `int fflush ( FILE * stream );` | If the given stream was open for writing (or if it was open for updating and the last i/o operation was an output operation) any unwritten data in its output buffer is written to the file. |
| [`tempfile`](http://www.cplusplus.com/reference/cstdio/tmpfile/) |`FILE * tmpfile ( void );` | Creates a temporary binary file, open for update ("wb+" mode, see fopen for details) with a filename guaranteed to be different from any other existing file. The temporary file created is automatically deleted when the stream is closed (fclose) or when the program terminates normally.|

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

Returns NULL if the file is opened in read mode but it does not exist.

**`fseek`**

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
  
# Reading input

## Functions

| Function | Syntax | Description |
| -------- | ------ | ----------- |
| [`fgetc`](http://www.cplusplus.com/reference/cstdio/fgetc/) | `int fgetc ( FILE * stream );` | Returns the character currently pointed by the internal file position indicator of the specified stream. The internal file position indicator is then advanced to the next character. If the stream is at the end-of-file when called, the function returns EOF and sets the end-of-file indicator for the stream (feof). |
| [`fputc`](http://www.cplusplus.com/reference/cstdio/fputc/) | `int fputc ( int character, FILE * stream );` | Writes a character to the stream and advances the position indicator. |
| [`fgets`](http://www.cplusplus.com/reference/cstdio/fgets/) | `char * fgets ( char * str, int num, FILE * stream );` | Reads characters from stream and stores them as a C string into str until (num-1) characters have been read or either a newline or the end-of-file is reached, whichever happens first. A newline character makes fgets stop reading, but it is included in the string copied to str. |
| [`fputs`](http://www.cplusplus.com/reference/cstdio/fputs/) | `int fputs ( const char * str, FILE * stream );` | Writes the C string pointed by str to the stream. The function begins copying from the address specified (str) until it reaches the terminating null character ('\0'). This terminating null-character is not copied to the stream. |
| [`fread`](http://www.cplusplus.com/reference/cstdio/fread) |`size_t fread ( void * ptr, size_t size, size_t count, FILE * stream );` | Reads an array of count elements, each one with a size of size bytes, from the stream and stores them in the block of memory specified by ptr. The position indicator of the stream is advanced by the total amount of bytes read. | 
| [`fwrite`](http://www.cplusplus.com/reference/cstdio/fwrite/) | `size_t fwrite ( const void * ptr, size_t size, size_t count, FILE * stream );` | Writes an array of count elements, each one with a size of size bytes, from the block of memory pointed by ptr to the current position in the stream. The position indicator of the stream is advanced by the total number of bytes written. |

# I/O functions

| Function | Syntax | Description |
| -------- | ------ | ----------- |
| [`scanf`](http://www.cplusplus.com/reference/cstdio/scanf/) | `int scanf ( const char * format, ... );` |  Reads data from stdin and stores them according to the parameter format into the locations pointed by the additional arguments. The additional arguments should **point** to already allocated objects of the type specified by their corresponding format specifier within the format string.|
| [`printf`](http://www.cplusplus.com/reference/cstdio/printf/) | `int printf ( const char * format, ... );` | Writes the C string pointed by format to the standard output (stdout).|
| [`sscanf`](http://www.cplusplus.com/reference/cstdio/sscanf/) | `int sscanf ( const char * s, const char * format, ...);` | Reads data from s and stores them according to parameter format into the locations given by the additional arguments, as if scanf was used, but reading from s instead of the standard input (stdin). |
| [`sprintf`](http://www.cplusplus.com/reference/cstdio/sprintf/) | `int sprintf ( char * str, const char * format, ... );` | Composes a string with the same text that would be printed if format was used on printf, but instead of being printed, the content is stored as a C string in the buffer pointed by str. |
| [`fscanf`](http://www.cplusplus.com/reference/cstdio/fscanf/) | `int fscanf ( FILE * stream, const char * format, ... );`| Reads data from the stream and stores them according to the parameter format into the locations pointed by the additional arguments. |
| [`fprintf`](http://www.cplusplus.com/reference/cstdio/fprintf/) | `int fprintf ( FILE * stream, const char * format, ... );` | Writes a string pointed by format to the stream|

Format specifier: `%[*][width][length]specifier`

A numerical value can be formatted according to `%fm.pX`
- `m` indicates the minimum field width
- `p` indicates the precision
- `f` are the flags:
  - `-` to left-justify the value
  - `+` preceeds the value with the sign
  - `0` pads the width of the printed field with zeros

`fprintf` is a more general function that prints to any stream, compared with `printf` that prints only to `stdout`. Same for `scanf`

# Examples

**Read and write to console**
```c++
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_LENGTH 50
int main()
{
    char str[MAX_LENGTH];
    char strAge[MAX_LENGTH];
    char strHeight[MAX_LENGTH];
    int age;
    float height;
    printf("Hi, enter your name: ");
    // It is better to use fgets instead of scanf 
    // for user input to prevent buffer overflow
    fgets(str, MAX_LENGTH-1, stdin);
    str[strcspn(str, "\n")] = \0;   // Cleans \n at the end of the string
    printf("Hi %s, please enter your age: ", str);
    fgets(strAge, MAX_LENGTH, stdin);
    strAge[strcspn(strAge, "\n")] = 0;  // Cleans \n at the end of the string
    age = atoi(strAge);
    printf("Your age is: %d\n", age);
    printf("Please enter your height (mt): ");
    fgets(strHeight, MAX_LENGTH, stdin);
    strHeight[strcspn(strHeight, "\n")] = 0;
    height = atof(strHeight);
    printf("Your height is: %4.2f\n", height);
    return 0;
}
```

**Write and read line from file**
```c++
#include <stdio.h>
#define BUFF_SIZE 50
int main() 
{
FILE *fp;
fp = fopen("test.txt", "w+");
fprintf(fp, "This is the content of the file test.txt.\n");
fseek(fp, 0, SEEK_SET); //Sets the cursor at the beginning of the file
char str[BUFF_SIZE];
fscanf(fp, "%[^\n]", str);
printf("%s", str);
fclose(fp);
return 0;
}
```

**Write and read array to and from file**
```c++
#include <stdio.h>
int main() 
{
    int iArr[5] = {1, 2, 3, 4, 5};
    FILE *fp;
    fp = fopen("test.txt", "w+");
    fwrite(iArr, sizeof(iArr[0]), sizeof(iArr)/sizeof(iArr[0]), fp);
    rewind(fp);
    int oArr[5];
    fread(oArr, sizeof(oArr[0]), sizeof(oArr)/sizeof(oArr[0]), fp);
    int i;
    while (i != sizeof(oArr)/sizeof(oArr[0]))
        fprintf(stdout, "%d\n", oArr[i++]);
    fclose(fp);
return 0;
}
```

**Read and write an object to a file**
```c++
#include <stdio.h>

#define NAME_LENGTH 30

typedef struct {
    int id;
    char name[NAME_LENGTH];
} Student;

int main() 
{
    Student s = {7, "Marco"};
    FILE *fp;
    fp = fopen("test.txt", "w+");
    //fwrite needs a pointer to an array/struc, not a value!
    fwrite(&s, sizeof(s), 1, fp);   
    // Returns the cursor a the start of the filestream
    rewind(fp);
    Student s2;
    //fread needs a pointer to an array/struc, not a value!
    fread(&s2, sizeof(s), 1, fp);
    fprintf(stdout, "ID: %i\n", s2.id);
    fprintf(stdout, "Name: %s\n", s2.name);
    fclose(fp);
return 0;
}
```

**Write and read an array of objects to a file**
```c++
#include <stdio.h>

#define MAX_LENGTH 30

typedef struct {
    int id;
    char name[MAX_LENGTH];
    int age;
    char address[MAX_LENGTH];
} Person ;

int main(void){
    Person pW[2] = {
        {5, "marco", 27, "Milano (MI)"}
        , {7, "Ciccio", 30, "Parma (PR)"}
        };
    
    FILE *fp;
    fp = fopen("test.txt", "w+");
    fwrite(pW, sizeof(pW[0]), sizeof(pW)/sizeof(pW[0]), fp);
    rewind(fp);
    Person pR[2];
    fread(pW, sizeof(pW[0]), sizeof(pW)/sizeof(pW[0]), fp);
    printf("Valori oggetti:\n");
    for (int i = 0; i != sizeof(pW)/sizeof(pW[0]); ++i) {
        printf("P%d.id: %d\n", i, pW[i].id);
        printf("P%d.name: %s\n", i, pW[i].name);
        printf("P%d.age: %d\n", i, pW[i].age);
        printf("P%d.address: %s\n", i, pW[i].address);
    }
    return 0;
}
```

**Read multiple lines from file into an object**

```c++
#include <stdio.h>
#include <string.h>

const size_t MAX_LENGTH = 30;

typedef struct {
    int id;
    char name[30];
    int age;
    char address[30];
} Person ;

int main(void){
    FILE *fp;
    fp = fopen("test.txt", "w+");
    fputs("1,marco,27,Milano (MI)\n2,Ciccio,30,Parma (PR)", fp);
    rewind(fp);
    const int LENGTH = MAX_LENGTH-1;
    char line[MAX_LENGTH];
    Person p[2];
    int n = 0;
    printf("Righe lette:\n");
    while (feof(fp) == 0) {
        (fgets(line, MAX_LENGTH-1, fp));
        line[strcspn(line, "\n")] = 0;
        printf("%s\n", line);
        sscanf(line, "%d , %39[^,] , %d , %39[^,] ", &p[n].id, &p[n].name, &p[n].age, &p[n].address);
        ++n;
    }
    printf("\nValori oggetti:\n");
    for (int i = 0; i != n; ++i) {
        printf("P%d.id: %d\n", i, p[i].id);
        printf("P%d.name: %s\n", i, p[i].name);
        printf("P%d.age: %d\n", i, p[i].age);
        printf("P%d.address: %s\n", i, p[i].address);
    }   
    return 0;
}
```

[Convertire intero a stringa con il preprocessore](https://stackoverflow.com/questions/25410690/scanf-variable-length-specifier)



- Operazioni sui processi
  - Generare processi slave e master
  - Terminare processi
  - Sostituire il codice di un processo in esecuzion
  
