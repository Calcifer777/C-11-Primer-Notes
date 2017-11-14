To be inserted at the BEGINNING of the paragraph:
When a member is omitted from the constructor initializer list, it is implicitly initialized using the same process as is used by the synthesized default constructor. In this case, those members are initialized by the in-class initializers. 


---------------------------
***************************
To be inserted in the constructors paragraph:

With respect to the  default initializer, the new parts in these definitions are the colon and the code between it and the
curly braces that define the (empty) function bodies. This new part is a constructor initializer list, which specifies initial values for one or more data members of the object being created. The constructor initializer is a list of member names, each of which is followed by that member’s initial value in parentheses (or inside curly braces). Multiple member initializations are separated by commas.

When a member is omitted from the constructor initializer list, it is implicitly initialized
using the same process as is used by the synthesized default constructor. In this
case, those members are initialized by the in-class initializers.

==========================

## Class Scope

**Scope and Members Defined outside the Class**

The fact that a class is a scope explains why we must provide the class name as well as the function name when we define a member function outside its class. Outside of the class, the names of the members are hidden. Once the class name is seen, the remainder of the definition—including the parameter list and the function body—is in the scope of the class. As a result, we can refer to other class members without qualification.

**Type Names Are Special**

Ordinarily, an inner scope can redefine a name from an outer scope even if that name has already been used in the inner scope. However, in a class, if a member uses a name from an outer scope and that name is a type, then the class may not subsequently redefine that name. *Definitions of type names usually should appear at the beginning of a class. That way any member that uses that type will be seen after the type name has already been defined*.

## Constructors revisited

Members that are const or references must be initialized. Similarly, members that are of a class type that does not define a default constructor also must be initialized. 





