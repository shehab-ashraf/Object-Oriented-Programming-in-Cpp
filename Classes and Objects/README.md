# **`What are Classes and Objects?`**

Classes are used to create user-defined data types. The predefined data types in C++ are classes themselves.
We can use these basic data types to create our own class.
The cool part is that our class can contain multiple variables, pointers, and functions which would be available to us whenever a class object is created.

 An object can be created from class. An object is an instance of a class. we can create many many objects each has own identity,
 each can use the defined class methods
 
 In general, there are categories are present in all classes.
 >Data Members
 >>These are also known as the member variables of a class. This is because they contain the information relevant to the object of the class.
 
 >Member Functions
 >>This category of attributes enables the class object to perform operations using the member variables.

**Class Definition**

Similar to functions, classes need to be created outside the main().
The written code of a class and its attributes are known as the definition or implementation of the class.
```c++
class className {
  
  /* All member variables
  and member functions*/

}; //The semi-colon operator ends the class
```

**Creating a Class Object** 

The className will be used to create an instance of the class in our main program.
We can create an object just like we create objects of other data types:
```c++
class className {
  ...
};

int main() {
  int i; //integer object
  className c; // className object
  }
```


# Access Modifiers

*Private*
>A private member cannot be accessed directly from outside the class. The aim is to keep it hidden from the users and other classes.
It is a popular practice to keep the data members private since we do not want anyone manipulating our data directly. By default, all declared members are private in C++.
However, we can also make members private using the private: heading.

```c++
class Class1 {
  int num; // This is, by default, a private data member
  ...
};

class Class2 {
  private: // We have explicitly defined that the variable is private
  int num;
  ...
};
```

*Public*
>This tag indicates that the members can be directly accessed by anything which is in the same scope as the class object.
Member functions are usually public as they provide the interface through which the application can communicate with our private members.

```c++
class myClass {
  int num; // Private variable
  
  public: // Attributes in this list are public
  void setNum(){
    // The private variable is directly accessible over here!
  }
};
```
Public members of a class can be accessed by a class object using the(.)operator.
For example, if we have an object_c_of type myClass, we could access setNum() like this:
```c++
myClass c; // Object created
c.setNum(); // Can manipulate the value of num
c.num = 20; // This would cause an error since num is private
```
*Protected*

>The protected category is unique. The access level to the protected members lies somewhere between private and public.
 The primary use of the protected tag is to implement **inheritance**, which is the process of creating classes out of classes.


# Class Data Members
 the data members contain all the information we store in a class. All the data members have to be defined at compile time.
 It is a very safe practice to make our member variables private.
 Making them public could possibly crash the application because any external force could manipulate them in any way.
 
*Data Types of Member Variables*
>C++ gives us a lot of freedom in selecting the data type of a data member.
 We can choose any of the in-built types such as int, double etc. Arrays, vectors, and pointers can also be used.
 
 Here’s an example of a Student class and its data members:
 ```c++
#include<iostream>
using namespace std;

class myClass {
  // All private members
  string name;
  int age;
  string *address;
  char grades [10]; // A student can have a maximum of 10 grades
};
```
We should always be careful with arrays inside classes. We should have appropriate checks in place to make sure our program never goes out of bounds due to an array.
A good practice is to store the size of the array in a variable. This way, we’ll always remember the maximum capacity.
 

**Class Data Member Initialization**
>Class data members can be initialized in the class declaration. 
 ```c++
 #include <iostream>
#define PI 3.1416
using namespace std;

class Circle {
  private: 
    int radius = 1;
  
  public:
    void setRadius(int r) {
      if ( r >= 0 ) {
        radius = r;
      }
    }

    int getRadius() {
      return radius;
    }

    double getArea() {
      return PI * radius * radius;
    }
};

int main() {
  Circle c;
  cout << "The area of a circle of radius " << c.getRadius() << " is " << c.getArea() << endl;
  return 0;
}
```
Another way to initialize class data members is using **constructors**.

# Class Member Functions
**The Purpose of Member Functions**
>Member functions act as the interface between a program and the data members of a class in the program.
 These functions can either change the content of the data variables or use their values to perform a certain computation.
 All the useful member functions should be public, although, some functions which do not need to be accessed from the outside could be kept private.
 
**Declaration and Definition**
>Like all functions, member functions can either be defined straightaway, or they could be declared first and defined later.
```c++
class Rectangle {
  int length;
  int width;

  public:
  void setLength(int l){ // This function changes the value of length
    length = l;
  }
  
  int area(){
    return length * width; // Only the values of the data members are
                           // accessed and used to calculate the area
  }
};
```
**Scope Resolution Operator**
>The scope resolution operator (::) allows us to simply declare the member functions in the class and define them elsewhere in the code.
 To use the scope resolution operator, we follow a certain syntax:
 ```c++
 returnType className::function()
 ```
 Now, we’ll use the scope resolution operator on our Rectangle class.
 ```c++
 class Rectangle {
  int length;
  int width;

  public:
  
  // We only write the declaration here
  void setLength(int l);
  int area();
};

// Somewhere else in the code
void Rectangle::setLength(int l){ // Using the scope resolution operator
  length = l;
}

int Rectangle::area(){
  return length * width; 
}
 ```
 The :: operator tells the compiler that the particular function belongs to the class preceding it.
 
**Get and Set Functions**
>These two types of functions are very popular in OOP. A get function retrieves the value of a particular data member, whereas a set function sets its value.
It is a common convention to write the name of the corresponding member variable with the get or set command. We have already seen an example of a set function in the code above.
setLength(int l) is a perfect example.

Let’s write get and set functions for the length and width in our Rectangle class:
```c++
class Rectangle {
  int length;
  int width;

  public:
  
  // get and set for length
  void setLength(int l);
  int getLength();
  
  // get and set for width
  void setWidth(int w);
  int getwidth();
  
  int area();
};


void Rectangle::setLength(int l){ 
  length = l;
}
int Rectangle::getLength(){ 
  return length;
}

void Rectangle::setWidth(int w){ 
  width = w;
}
int Rectangle::getWidth(){ 
  return width;
}

int Rectangle::area(){
  return length * width; 
}
```
**Overloading**
>Member functions can be overloaded just like any other function.
 This means that multiple member functions can exist with the same name on the same scope, but must have different arguments.
 
 
 # Constructors
 
 **What is a Constructor?**
 >As the name suggests, the constructor is used to construct the object of a class.
 >A constructor’s name must be exactly the same as the name of its class.
 >The constructor is a special function because it does not have a return type.
 > We do not even need to write void as the return type. It is a good practice to declare/define it as the first member function.


**Default Constructor**
>In a default constructor, we define the default values for the data members of the class.
> Hence, the constructor creates an object in which the data members are initialized to their default values.
```c++
#include <iostream>
#include <string>
using namespace std;

class Date {
  int day;
  int month;
  int year;

  public:
  // Default constructor
  Date(){
    // We must define the default values for day, month, and year
    day = 0;
    month = 0;
    year = 0;
  }

  // A simple print function
  void printDate(){ 
    cout << "Date: " << day << "/" << month << "/" << year << endl;
  }
};

int main(){
  // Call the Date constructor to create its object;
  
  Date d; // Object created with default values!
  d.printDate();
}
  
```
Notice that when we created a Date object, we don’t treat the constructor as a function and write this:
```c++
d.Date()
```
We create the object just like we create an integer or string object. It’s that easy!
The default constructor does not need to be explicitly defined. Even if we don’t create it,
the C++ compiler will call a default constructor and set data members to some junk values.

# Parameterized Constructor
>The default constructor isn’t all that impressive. Sure, we could use set functions to set the values for day, month and year ourselves, but this step can be avoided using a parameterized constructor.
In a parameterized constructor, we pass arguments to the constructor and set them as the values of our data members.

**We are basically overriding the default constructor to put our preferred values for the data members.**
```c++
#include <iostream>
#include <string>
using namespace std;

class Date {
  int day;
  int month;
  int year;

  public:
  // Default constructor
  Date(){
    // We must define the default values for day, month, and year
    day = 0;
    month = 0;
    year = 0;
  }
  
  // Parameterized constructor
  Date(int d, int m, int y){
    // The arguments are used as values
    day = d;
    month = m;
    year = y;
  }

  // A simple print function
  void printDate(){ 
    cout << "Date: " << day << "/" << month << "/" << year << endl;
  }
};

int main(){
  // Call the Date constructor to create its object;
  
  Date d(1, 8, 2018); // Object created with specified values!
  d.printDate();
}
```
```
Output : Date: 1/8/2021
```

# this Pointer
>The this pointer exists for every class. It points to the class object itself.
We use the pointer when we have an argument which has the same name as a data member.
Since this is a pointer, we use the -> operator to access members instead of(.)
```c++
#include <iostream>
#include <string>
using namespace std;

class Date {
  int day;
  int month;
  int year;

  public:
  // Default constructor
  Date(){
    // We must define the default values for day, month, and year
    day = 0;
    month = 0;
    year = 0;
  }
  
  // Parameterized constructor
  Date(int day, int month, int year){
    // Using this pointer
    this->day = day;
    this->month = month;
    this->year = year;
  }

  // A simple print function
  void printDate(){ 
    cout << "Date: " << day << "/" << month << "/" << year << endl;
  }
};

int main(){
  // Call the Date constructor to create its object;
  
  Date d(1, 8, 2018); // Object created with specified values!
  d.printDate();
}
  
```
