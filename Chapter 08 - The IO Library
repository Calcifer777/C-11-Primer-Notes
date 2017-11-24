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

## `get`

| Input Type | Command | Result |
| ---------- | ------- | ------ |
| single character (1)	| int get(); | |
| single character (1)	| istream& get (char& c); | |
| c-string (2)	        | istream& get (char* s, streamsize n); | |
| c-string (2)	        | istream& get (char* s, streamsize n, char delim); | |
| stream buffer (3)	    | istream& get (streambuf& sb); | |
| stream buffer (3)	    | istream& get (streambuf& sb, char delim); | |




## Clear
**`cin.clear()`**: helps in clearing the error flags which are set when std::cin fails to interpret the input.

**`cin.ignore()`**, on the other hand helps in removing the input contents that could caused the read failure. By default only 
clears one character (the first one). 
`cin.ignore(1000)` would mean the next 1000 characters in the read buffer shall be ignored. 
`cin.ignore(1000,'\n')` would mean either next 1000 characters or the characters until '\n' shall be ignored, whichever comes first.
