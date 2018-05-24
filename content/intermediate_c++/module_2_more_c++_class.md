+++
title =  "Module 2: More C++ Class"
+++
#### **Splitting Classes**
* In C++, the common practice is to create your classes as two separate files. The header files, with a
.h extension on the filename, is used to contain the declarations found in the class file. 
* Header file is more like a "manual" to the user, so that user only needs to know how to use this class, ignoring how
methods are actually implemented. 
* Declarations in the header file includes function prototypes
and class constructors typically. 
* The actual implementation of the class are in a .cpp or .c file.

Next, lets take a look at an example header file: Math.h
```
    // Math.h
    // Header file for the Math class

    #pragma once

    // Math class definition
    static class Math
    {
        public:

        // given base and exponent, calculate value
        static int pow(int base, int exp);

    };
```
* ```#pragma once``` is a preprocessor directive(like ```#include```) that tells the compiler
to only include this header once, regardless of how many times it has been imported in the program
* The ```static``` keyword meaning we don't need to instantiate this class before using. Otherwise, we
need to do:

```
    Math math = new Math();
    math.pow(2, 8);
```

this is helpful for a utility class such as this math class. Notice that the static class is only supported
by Visual Studio, most the cases, people only use static member function instead of class.

Next, let's take a look at the implementation of this class, the .cpp file:

```
    #include "stdafx.h"
    #include "Math.h"

    int Math::pow(int base, int exp)
    {
        int result = 1;

        for (int i = 0; i < exp; i++)
        {
            result = result * base;
        }

        return result;
    }
```

* In the actual function implementation, we use Math::pow instead of just Math. The **::**
is a **scope resolution operator**. In this case, it is used to call static members of the class.

#### **Constructors and Destructors**
* A constructor is used to initialize data members of a class
* Each class will have only one default constructor. If you don't manually create one, the compiler
will create one automatically. 
* The default constructor initialize member variables to default values

Let's take a look at the below example:

**Person.h**
```
    #pragma once
    
    #include <string>
    
    class Person
    {
    
    private:
        std::string firstName;
        std::string lastName;
    
        int age;
    
    public:
        Person();
    
        Person(std::string fName, std::string lName);
    
        Person(std::string fName, std::string lName, int age);
    
        ~Person();

        void SayHello();
    };
```

**Person.cpp**
```
    #include "stdafx.h"
    #include "Person.h"
    #include <iostream>
    
    Person::Person()
    {
    
    }
    
    Person::Person(std::string fName, std::string lName)
    {
        this -> firstName = fName;
        this -> lastName = lName;
    }
    
    Person::Person(std::string fName, std::string lName, int age)
    {
        this -> firstName = fName;
        this -> lastName = lName;
    
        this -> age = age;
    }
    
    
    Person::~Person()
    {
    }
```

* The first constructor is the default constructor. It has no parameters and because we have not initialized our private 
member variables, this constructor will do so with the default values for data types of those member variables.
* The second constructor takes two arguments and uses those to initialize the first and last name member 
variables in the class.  Notice, we don't have age in the arguments, it may or may not get initialized depends on the compiler.



#### **Scope in Classes**
The way that we declare our objects is important for determining how we call the member functions or access the public member variables.

```
Person *pOne = new Person();
Person p;
Person &Ref = p;

pOne->SayHello();
p.SayHello();
pRef.SayHello();
```

* Like the example shown above, if we dynamically allocate memory for a new Person object, we use the **arrow member selection operator ->**
to gain access.
* In contrast, if we create a new Person object without using a pointer or the new keyword, we use a **dot operator** to access
the member function. Notice, the reference is the same
* Finally, if the member function is a static function , we would use **Person::SayHello()** without instantiate an object of the Person class

----

The definition of **encapsulation** in C++ has two layers:

* First is "Inclusion", meaning user can take all of member functions and member variables and enclose it within a class
* Second is "Data Restriction", meaning the outside user cannot direclty change the data of the class, only through constructors or
member functions. This helps the class to reject invalid input

----

A **namespace** is a "scope container" where you can place your classes, variables, or other identifiers to prevent name conflicts. For ecample,
"std" is a namespace when you use "std::cout" Again, the "::" symbol is called **scope resolution operator** that allows user
gain access to certain function in certain namespace
