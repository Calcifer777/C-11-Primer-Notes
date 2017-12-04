# Recap of 'cin'

```c++
#include <iostream>
#include <string>
#include <limits>
using namespace std;

int main()
{
  // 1 caracter input
  char letter;
  cout << "Insert letter: ";
  // istream& get (char& c);
  cin.get (letter);
  cout << "letter: " << letter << endl;
  
  // cin reset
  cin.clear();
  cin.ignore(numeric_limits<streamsize>::max(), '\n');
  
  // sentence input 
  string sentence;
  cout << "Insert sentence: ";
  getline (cin, sentence);
  cout << "Sentence: " << sentence << endl;
  
  // Validating input
  int a;
  cout << "Enter an integer: ";
  while (!(cin >> a)) {
    cin.ignore();
    while (cin.get() != '\n') continue
    cout << "Invalid input. Enter an integer: ";
  }
}

```

## [`istream::get`](http://www.cplusplus.com/reference/istream/istream/get/) 

| Input Type | Command | Result |
| ---------- | ------- | ------ |
| single character (1)	| `int get();` | Extracts a single character from the stream and returns it as `int`|
| single character (1)	| `istream& get (char& c);` |  Extracts a single character from the stream and sets it as the value of the function argument |
| c-string (2)	        | `istream& get (char* s, streamsize n);` | Extracts characters from the stream and stores them in s as a c-string, until (n-1) characters have been extracted |
| c-string (2)	        | `istream& get (char* s, streamsize n, char delim);` | Extracts characters from the stream and stores them in s as a c-string, until  the delimiting character is encountered: the delimiting character being either the newline character ('\n') or delim (if this argument is specified).|
| stream buffer (3)	    | `istream& get (streambuf& sb);` | Extracts characters from the stream and inserts them into the output sequence controlled by the stream buffer object sb, stopping as soon as such an insertion fails |
| stream buffer (3)	    | `istream& get` (streambuf& sb, char delim); | Extracts characters from the stream and inserts them into the output sequence controlled by the stream buffer object sb, stopping as soon as the delimiting character is encountered in the input sequence (the delimiting character being either the newline character, '\n', or delim, if this argument is specified). |

## [`ios::clear`](http://en.cppreference.com/w/cpp/io/basic_ios/clear)
**`cin.clear()`**: helps in clearing the error flags which are set when std::cin fails to interpret the input.

The states of the input buffer are (a combination of) 
| Constant | Explanation |
| -------- | ----------- |
|goodbit	 | no error |
|badbit	   | irrecoverable stream error |
|failbit   |input/output operation failed (formatting or extraction error) |
|eofbit	   | associated input sequence has reached end-of-file |

## [`istream::ignore`](http://www.cplusplus.com/reference/istream/istream/ignore/)

**`cin.ignore()`** helps in removing the input contents that could caused the read failure. By default only 
clears one character (the first one). 
`cin.ignore(1000)` would mean the next 1000 characters in the read buffer shall be ignored. 
`cin.ignore(1000,'\n')` would mean either next 1000 characters or the characters until '\n' shall be ignored, whichever comes first.

# The IO classes

**IO Library Types and Headers**

| Header | Type |
| ------ | ---- |
| `iostream` | `istream`, `wistream` reads from a stream |
| `iostream` | `ostream`, `wostream` writes to a stream |
| `iostream` | `iostream`, `woistream` reads and writes a stream |
| `fstream` | `ifstream`, `wifstream` reads from a stream |
| `fstream` | `ofstream`, `wofstream` writes to a stream |
| `fstream` | `fstream`, `wfstream` reads and writes a stream |
| `sstream` | `istringstream`, `wistringstream` reads from a stream |
| `sstream` | `ostringstream`, `wostringstream` writes to a stream |
| `sstream` | `stringstream`, `wstringstream` reads and writes a stream |

**IO Library Condition State**

| State | Description |
| ----- | ----------- |
| `strm::iostate` | iostate is a machine-dependent integral type that represents the condition of a stream |
| `strm::badbit` | Indicates that the stream is corrupted |
| `strm::failbit` | Indicates that an IO operation failed |
| `strm::eofbit` | Indicates that a stream hit end-of-file |
| `strm::goodbit` | Indicates that a stream is not in an error state. Guaranteed to be 0 |
| `s.eof()` | true if eobit in the stream s is set |
| `s.fail()` | true if failbit in the stream s is set |
| `s.bad()` | true if badbit in the stream s is set |
| `s.clear()` | Resets all condition vales in the stream s to valid state |
| `s.cleaf(flags)` | Reset the condition of `s` to flags. Returns void |  
| `s.setstate(flags)` | Adds specified conditions to `s` |
| `s.rdstate()` | Returns current condition of `s` as a `strm::iostate` value |


