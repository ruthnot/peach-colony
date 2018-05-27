+++
title =  "Module 3: More OOP in C++"
+++
### Inheritance

* Inheritance meaning one can write a new class that inherit the members of an existing class. The existing class is called **base** class, the new class is called **derived** class.
* There're three types of inheritance in C++, public, private and protected, below are the rules:
    * Public Inheritance:
        * public in base class remains public in derived class
        * protected in base class remains  protected in derived class
        * private in base class remains private in derived class
    * Protected Inheritance:
        * public and protected in base class becomes protected in derived class
        * private in base class remains private in derived class
    * Private Inheritance:
        * public and protected and private in base class all becomes  private in derived class
* Remember, no matter which type of inheritance you choose, derived class can never access base class' private members directly.
* Default inheritance is "private" if you're not using any access specifier. However, "private" and "protected" inheritance are rarely used. Hence, usually you need to add a "public" specifier when using inheritance, like this:

```
class Rectangle: public Shape{
};
```

### Encapsulation and Protected Access

#### Protected Class
* Protected class serves the purpose that you want to keep certain members of the base class private to the "outside world", but public to the drived class.

#### Friend Class
* The friend class can access all members (including private members) from the first class.
* A good way of explaining friend class is the so called "Handle-Body" idiom in C++. The idiom splits one class into two intimately related class: a "body" class that defines the private data, and a "handle" class that defines the public behavior. The body defines the handle class as a friend class, so that the handle class can access all the members in the body class
* Here is the implementation:

**Body.h**
```
class Handle;  // Forward reference of the "handle" class, so the compiler knows about it.

class Body
{
    friend class Handle;

    private:
        int someData;
        ...
};
```
**Handle.h**
```
#include "Body.h"

class Handle
{
private:
    Body* body; //The "handle" class typically maintains an internal instance of the "body" class.

public:
    Handle();
    ~Handle();

    void someOperationOnBody();
    ...
};
```
**Handle.cpp**
```
#include "Handle.h"

Handle::Handle()
{
    body = new Body; //Create the underlying "body" object.
}

Handle::someOperationOnBody()
{
    someData = 42; //Perform operations on the underlying "body" object.
}
```
**Main.cpp**
```
#include "Handle.h"

int main()
{
    Handle h;
    h.someOperationOnBody();

    return 0;
}
```

* this way, client code just works with the "handle" class, and has no knowledge of the underlying "body class". 
* The intent of this idiom is to shield client code from the details of the "body class", so that its implementation can vary dramatically without impacting the rest of the application
* In other words, the "handle" class serves a "interface" of the "body" class.

### Virtual Functions and Abstract Classes
* We use inheritance to reuse command code across a hierachy of related class, but sometimes, a derived class need somehow tweak some of the member from the base class to better perform, we call it **overriding**.
* To define overridable member function, we use the keyword **virtual** to create a virtual funciton.
* Pure Virtual function means that it won't be implemented at all at the base class, and the derived class has to override it.
