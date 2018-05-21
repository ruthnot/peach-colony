+++
title =  "Module One: Pointers"
+++
#### **Pointers**

A pointer is simply a variable that holds the memory address of an object in C++. To create
 a pointer variable, use * plus the data type. such as:
```
int num = 3;
int* pNum = &num;
```
* Here, the ```&``` is the **address-of operator**. what we did is assigning the address of variable "num" to the 
pointer (pointer variable) pNum. 
* Notice that```int* pNum``` and ```int *pNum```is essentially the same. The
first one emphasize ```pNum```'s pointer type, the second one emphasize ```pNum``` is a pointer.
* The address of ```num``` is only good in current scope. In other words, each time we run this code,
the address will be different.
* When declaring a pointer, should you always initialize it to NULL, nullptr, 0 or with a memory address.
also, make sure the pointer type matches the variable type.


The asterisk symbol ```*``` has three usage: the multiplication operator, the ponter
symbol, and also the **Dereference Operator**. 
```
int num = 3;
int *pNum = &num;

*pNum =45;
```
* It is called **overloading** when use one symbol for **multiple dissimilar purposes**
* In the above example, we first use * to declare the pointer, then use * as dereference operator
to get the value of that variable.

#### **Reference Types**
* The ampersand symbol **&** is the address-of operator, and also the **reference** operator, we
are overloading again! 
* Reference is like an alias of a variable. When we pass a variable to a function, 
even if we use the same variable name, because what we did is pass a copy, instead of the variable itself, 
within the function's scope, nothing we affect the original variable. When the variable is large, and we want to 
modify it directly, we can pass an alias, this case the reference of that variable to the function. 
* Also, a reference must be initialized when first declared, same as pointers.

#### **Managing Memory in C++**
* Each time we instantiate an object, the system will allocate memory for it. We can also manually
using the ```new``` operator. For example,

```
int *pInt = new int; 
double * pDouble = new double;

*pInt = 3; 
*pDouble = 5.0;
```

* We need to assign the specific data type (int, double) when allocating the memory, so that
the system know how large the memory you need. For example, 4 bytes for int, and 8 bytes for double

* After we allocated the memory, don't forget to release the memory (deallocation) use **delete** operator:

```
delete pInt;
delete pDouble;

```
* Every **new** operator needs a **delete** operator at the end to prevent **memory leak**.