
# Classes

## Basics

```c++
class Student {
  
  // Members
  string name;
  string surname;
  string address;
  
  // Constructors
  public: // Sets everything after this declaration as public; private does the same
  Student() = default;
  Student(const string &s1, const string &s2, const string &s3) :
    name(s1), surname(s2), address(s3) {}  // No semicolumn after this constructor!!!
  // Methods
  inline string const getName() {
    return this->name;
  }
  void setName(string newName) {
    (this)->name = newName;
  }
};
```
