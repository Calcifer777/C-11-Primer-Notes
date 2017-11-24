# Recap of the 'cin' use

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
}

```

## [`get`](http://www.cplusplus.com/reference/istream/istream/get/) 

| Input Type | Command | Result |
| ---------- | ------- | ------ |
| single character (1)	| int get(); | Extracts a single character from the stream and returns it as `int`|
| single character (1)	| istream& get (char& c); |  Extracts a single character from the stream and sets it as the value of the function argument |
| c-string (2)	        | istream& get (char* s, streamsize n); | Extracts characters from the stream and stores them in s as a c-string, until (n-1) characters have been extracted |
| c-string (2)	        | istream& get (char* s, streamsize n, char delim); | Extracts characters from the stream and stores them in s as a c-string, until  the delimiting character is encountered: the delimiting character being either the newline character ('\n') or delim (if this argument is specified).|
| stream buffer (3)	    | istream& get (streambuf& sb); | |
| stream buffer (3)	    | istream& get (streambuf& sb, char delim); | |




## Clear
**`cin.clear()`**: helps in clearing the error flags which are set when std::cin fails to interpret the input.

**`cin.ignore()`**, on the other hand helps in removing the input contents that could caused the read failure. By default only 
clears one character (the first one). 
`cin.ignore(1000)` would mean the next 1000 characters in the read buffer shall be ignored. 
`cin.ignore(1000,'\n')` would mean either next 1000 characters or the characters until '\n' shall be ignored, whichever comes first.
