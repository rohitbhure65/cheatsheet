# 🔷 Object-Oriented Programming in C++
### The Complete Handbook — Beginner to Advanced

> *"C++ is a language that combines the power of assembly language with the readability of assembly language."* — (and now, with OOP, it becomes truly powerful 😄)

![C++](https://img.shields.io/badge/C++-17%2F20-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![OOP](https://img.shields.io/badge/Paradigm-Object--Oriented-orange?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Advanced-green?style=for-the-badge)

---

## 🤔 What is Object-Oriented Programming?

**Object-Oriented Programming (OOP)** is a programming paradigm that organizes code around **objects** — real-world entities that have:
- **Attributes** (data/properties) → what it *has*
- **Behaviors** (methods/functions) → what it *does*

Instead of writing long procedural code (list of instructions), OOP groups related data and functions together into **classes**, making code modular, reusable, and easy to maintain.

> 📦 Think of a **class** as a blueprint (like architectural drawings of a house).
> Think of an **object** as the actual built house using that blueprint.

---

## 🚀 Why OOP in C++?

| Feature | Benefit |
|---|---|
| **Encapsulation** | Data hiding — protects data from misuse |
| **Inheritance** | Code reuse — don't repeat yourself |
| **Polymorphism** | Flexibility — one interface, many implementations |
| **Abstraction** | Simplicity — hide complex details, show essentials |
| **Modularity** | Large projects become manageable |
| **Maintainability** | Easy to modify, extend, and debug |

---

## ⚡ OOP vs Procedural Programming

| Feature | Procedural | OOP |
|---|---|---|
| Focus | Functions & procedures | Objects & classes |
| Data | Global or passed around | Encapsulated in objects |
| Reuse | Function reuse | Inheritance & composition |
| Access Control | None | public / private / protected |
| Real-world modeling | Difficult | Natural |
| Examples | C, Pascal | C++, Java, Python |

---

## 📚 Table of Contents

1. [C++ Basics Refresher](#1-c-basics-refresher)
2. [Classes & Objects](#2-classes--objects)
3. [Constructors & Destructors](#3-constructors--destructors)
4. [Access Modifiers](#4-access-modifiers)
5. [Encapsulation](#5-encapsulation)
6. [Getters & Setters](#6-getters--setters)
7. [Static Members](#7-static-members)
8. [this Pointer](#8-this-pointer)
9. [Friend Functions & Classes](#9-friend-functions--classes)
10. [Inheritance](#10-inheritance)
11. [Types of Inheritance](#11-types-of-inheritance)
12. [Polymorphism](#12-polymorphism)
13. [Function Overloading](#13-function-overloading)
14. [Operator Overloading](#14-operator-overloading)
15. [Virtual Functions & Runtime Polymorphism](#15-virtual-functions--runtime-polymorphism)
16. [Abstract Classes & Pure Virtual Functions](#16-abstract-classes--pure-virtual-functions)
17. [Abstraction](#17-abstraction)
18. [Interfaces in C++](#18-interfaces-in-c)
19. [Templates (Generic Programming)](#19-templates-generic-programming)
20. [Exception Handling](#20-exception-handling)
21. [File Handling with OOP](#21-file-handling-with-oop)
22. [Smart Pointers & OOP](#22-smart-pointers--oop)
23. [Advanced OOP Concepts](#23-advanced-oop-concepts)
24. [Design Patterns](#24-design-patterns)
25. [Best Practices](#25-best-practices)
26. [Exercises & Challenges](#26-exercises--challenges)
27. [Conclusion & Resources](#27-conclusion--resources)

---

# 1. C++ Basics Refresher

Before diving into OOP, here's a quick recap of C++ essentials.

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main() {
    // Variables & Data Types
    int age = 25;
    double salary = 75000.50;
    char grade = 'A';
    bool isActive = true;
    string name = "Rohit";

    // Input / Output
    cout << "Name: " << name << endl;
    cout << "Age: " << age << "\n";
    cin >> age;   // read input

    // References & Pointers
    int x = 10;
    int& ref = x;      // reference — alias for x
    int* ptr = &x;     // pointer — stores address of x

    ref = 20;          // changes x to 20
    *ptr = 30;         // changes x to 30 (dereference)

    cout << "Address of x: " << ptr << endl;
    cout << "Value at ptr: " << *ptr << endl;

    // Arrays & Vectors
    int arr[5] = {1, 2, 3, 4, 5};
    vector<int> nums = {10, 20, 30, 40};
    nums.push_back(50);

    return 0;
}
```

### Compile & Run

```bash
# Compile
g++ -std=c++17 -o program main.cpp

# Run
./program          # Linux/Mac
program.exe        # Windows

# Compile with warnings
g++ -std=c++17 -Wall -Wextra -o program main.cpp
```

---

# 2. Classes & Objects

## Definition

A **class** is a user-defined data type that bundles **data (attributes)** and **functions (methods)** together.

An **object** is an instance of a class — a real entity created from the blueprint.

## Syntax

```cpp
class ClassName {
    // access specifier (private by default)
    dataType attribute1;
    dataType attribute2;

public:
    // public members accessible outside
    returnType methodName(parameters);
};
```

## Example

```cpp
#include <iostream>
#include <string>
using namespace std;

// Class definition — the blueprint
class Car {
    // Private by default
    string brand;
    string model;
    int year;
    double price;

public:
    // Method to set data
    void setDetails(string b, string m, int y, double p) {
        brand = b;
        model = m;
        year  = y;
        price = p;
    }

    // Method to display data
    void display() {
        cout << "Brand : " << brand  << endl;
        cout << "Model : " << model  << endl;
        cout << "Year  : " << year   << endl;
        cout << "Price : ₹" << price << endl;
    }

    // Method that returns a value
    double getPrice() {
        return price;
    }

    bool isExpensive() {
        return price > 1000000;
    }
};

int main() {
    // Creating objects (instances)
    Car car1;                       // object on stack
    Car* car2 = new Car();          // object on heap (dynamic)

    // Using the object
    car1.setDetails("Tata", "Nexon EV", 2024, 1500000);
    car1.display();

    cout << "Is expensive? " << (car1.isExpensive() ? "Yes" : "No") << endl;

    car2->setDetails("Maruti", "Swift", 2023, 700000);
    car2->display();               // use -> for pointer to object

    delete car2;                   // free heap memory

    return 0;
}
```

### Output
```
Brand : Tata
Model : Nexon EV
Year  : 2024
Price : ₹1500000
Is expensive? Yes
```

---

## Separating Declaration & Definition

In real projects, class declaration goes in a **header file** (`.h`) and definition in a **source file** (`.cpp`).

```cpp
// ── Student.h ── (Declaration)
#ifndef STUDENT_H
#define STUDENT_H

#include <string>
using namespace std;

class Student {
    string name;
    int rollNo;
    float cgpa;

public:
    void setData(string n, int r, float c);
    void display();
    float getCGPA();
};

#endif

// ── Student.cpp ── (Definition)
#include "Student.h"
#include <iostream>

// :: is the scope resolution operator
void Student::setData(string n, int r, float c) {
    name   = n;
    rollNo = r;
    cgpa   = c;
}

void Student::display() {
    cout << "Name   : " << name   << endl;
    cout << "Roll No: " << rollNo << endl;
    cout << "CGPA   : " << cgpa   << endl;
}

float Student::getCGPA() {
    return cgpa;
}

// ── main.cpp ──
#include "Student.h"

int main() {
    Student s;
    s.setData("Rohit", 101, 9.2f);
    s.display();
    return 0;
}
```

> 💡 **Important Points:**
> - `class` members are **private by default**
> - `struct` members are **public by default** (only difference from class)
> - Use `::` (scope resolution operator) to define methods outside the class
> - Always use `#ifndef` guards in header files to prevent double inclusion

---

## 📝 Exercises — Section 2

1. Create a `Book` class with title, author, price, and pages. Add methods to display info and check if it's a bestseller (price > 500).
2. Create a `Rectangle` class with width and height. Add methods for area, perimeter, and isSquare().

---

# 3. Constructors & Destructors

## Constructor

A **constructor** is a special member function that is **automatically called when an object is created**. It initializes the object's data.

**Rules:**
- Same name as the class
- No return type (not even `void`)
- Can be overloaded
- Called automatically — you don't call it explicitly

```cpp
#include <iostream>
#include <string>
using namespace std;

class BankAccount {
    string owner;
    string accountNo;
    double balance;

public:
    // 1. Default Constructor (no parameters)
    BankAccount() {
        owner     = "Unknown";
        accountNo = "N/A";
        balance   = 0.0;
        cout << "Default constructor called\n";
    }

    // 2. Parameterized Constructor
    BankAccount(string o, string acc, double bal) {
        owner     = o;
        accountNo = acc;
        balance   = bal;
        cout << "Parameterized constructor called for: " << owner << "\n";
    }

    // 3. Constructor with Initializer List (preferred — more efficient)
    // BankAccount(string o, string acc, double bal)
    //     : owner(o), accountNo(acc), balance(bal) {
    //     cout << "Initialized: " << owner << "\n";
    // }

    // 4. Copy Constructor
    BankAccount(const BankAccount& other) {
        owner     = other.owner;
        accountNo = other.accountNo;
        balance   = other.balance;
        cout << "Copy constructor called\n";
    }

    void deposit(double amount) {
        if (amount > 0) balance += amount;
    }

    void display() {
        cout << "Account: " << accountNo
             << " | Owner: " << owner
             << " | Balance: ₹" << balance << endl;
    }

    // Destructor
    ~BankAccount() {
        cout << "Destructor called for account: " << accountNo << "\n";
    }
};

int main() {
    BankAccount acc1;                              // default constructor
    BankAccount acc2("Rohit", "SB001234", 50000); // parameterized
    BankAccount acc3 = acc2;                       // copy constructor
    BankAccount acc4(acc2);                        // copy constructor (explicit)

    acc2.deposit(10000);
    acc2.display();

    // acc1, acc2, acc3, acc4 — destructors called automatically when they go out of scope
    return 0;
}
```

---

## Initializer List

Preferred over assignment in constructor body — more efficient, and **required** for `const` members and references.

```cpp
class Employee {
    const int id;     // const — MUST use initializer list
    string name;
    double salary;
    int& refValue;    // reference — MUST use initializer list

public:
    // Initializer list syntax
    Employee(int i, string n, double s, int& r)
        : id(i), name(n), salary(s), refValue(r) {
        // constructor body — runs after initialization
        cout << "Employee " << name << " created\n";
    }

    void display() {
        cout << "ID: " << id << " | Name: " << name
             << " | Salary: " << salary << endl;
    }
};

int main() {
    int x = 100;
    Employee e(1, "Rohit", 75000.0, x);
    e.display();
    return 0;
}
```

---

## Destructor

A **destructor** is called automatically when an object goes out of scope or is explicitly deleted. Used to release resources (memory, file handles, network connections).

```cpp
class FileManager {
    string filename;
    // Imagine we hold a file handle here

public:
    FileManager(string f) : filename(f) {
        cout << "Opening file: " << filename << "\n";
        // open file...
    }

    ~FileManager() {
        cout << "Closing file: " << filename << "\n";
        // close file, release memory...
    }
};

int main() {
    {
        FileManager fm("data.txt");  // constructor called
        // work with file...
    }  // ← destructor called here automatically (end of scope)

    FileManager* fm2 = new FileManager("log.txt");
    delete fm2;   // ← destructor called explicitly

    return 0;
}
```

### Constructor Types Summary

| Type | Syntax | When Used |
|---|---|---|
| Default | `ClassName()` | No args needed |
| Parameterized | `ClassName(args)` | Initialize with values |
| Copy | `ClassName(const ClassName& obj)` | Copy one object to another |
| Move (C++11) | `ClassName(ClassName&& obj)` | Transfer ownership |
| Delegating (C++11) | Calls another constructor | Avoid code duplication |

> ⚠️ **Rule of Three / Rule of Five:** If you define a custom destructor, copy constructor, or copy assignment operator — you likely need to define all three (or five in C++11 with move semantics).

---

## 📝 Exercises — Section 3

1. Create a `Matrix` class with rows and columns. Write a constructor that allocates memory and a destructor that frees it.
2. Create a `String` class (like std::string) with a copy constructor that does a deep copy.
3. Demonstrate the difference between shallow copy and deep copy.

---

# 4. Access Modifiers

Access modifiers control **who can access** class members.

| Modifier | Same Class | Derived Class | Outside Class |
|---|---|---|---|
| `private` | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ |

```cpp
#include <iostream>
#include <string>
using namespace std;

class Person {
private:
    // Only accessible within this class
    string password;
    int ssn;                         // Social Security Number

protected:
    // Accessible in this class AND derived classes
    string name;
    int age;
    string email;

public:
    // Accessible everywhere
    Person(string n, int a, string e, string pwd)
        : name(n), age(a), email(e), password(pwd), ssn(123456789) {}

    void greet() {
        cout << "Hi, I'm " << name << ", age " << age << endl;
        // Can access private here — we're inside the class
        cout << "Password (internally): " << password << endl;
    }

    string getName() { return name; }
    string getEmail() { return email; }
};

class Student : public Person {
    int rollNo;
    float gpa;

public:
    Student(string n, int a, string e, string pwd, int r, float g)
        : Person(n, a, e, pwd), rollNo(r), gpa(g) {}

    void displayStudentInfo() {
        // ✅ Can access protected members from base class
        cout << "Name : " << name  << endl;
        cout << "Age  : " << age   << endl;
        cout << "Email: " << email << endl;

        // ❌ Cannot access private members of base class
        // cout << password;  // Error!
        // cout << ssn;       // Error!

        cout << "Roll : " << rollNo << endl;
        cout << "GPA  : " << gpa    << endl;
    }
};

int main() {
    Person p("Rohit", 25, "rohit@dev.com", "secret123");

    // ✅ Public access
    p.greet();
    cout << p.getName() << endl;

    // ❌ Private/Protected access from outside — errors
    // cout << p.password; // Error!
    // cout << p.name;     // Error! (protected)

    Student s("Priya", 20, "priya@college.com", "pass456", 101, 9.2f);
    s.displayStudentInfo();

    return 0;
}
```

> 💡 **Memory Trick:**
> - `private` → Mine alone 🔒
> - `protected` → Mine + my children's 🔒👨‍👧
> - `public` → Everyone's 🌍

---

# 5. Encapsulation

## Definition

**Encapsulation** is the bundling of data and the methods that operate on that data within a single unit (class), while **restricting direct access** to some of the object's components.

It's the principle of **data hiding** — protecting internal state from unintended modification.

## Real-World Analogy

A **medicine capsule** 💊 — you take the medicine without seeing what's inside. The pill works but the internal composition is hidden.

A **car engine** 🚗 — you use the steering wheel and pedals without knowing how the engine works internally.

## Example

```cpp
#include <iostream>
#include <string>
#include <stdexcept>
using namespace std;

class BankAccount {
private:
    // Encapsulated (hidden) data
    string accountNumber;
    string ownerName;
    double balance;
    int pin;
    int failedAttempts;
    bool isLocked;

    // Private helper method
    bool validatePin(int enteredPin) {
        return enteredPin == pin;
    }

public:
    BankAccount(string accNo, string owner, double initialBalance, int p)
        : accountNumber(accNo), ownerName(owner), balance(initialBalance),
          pin(p), failedAttempts(0), isLocked(false) {}

    // Controlled access to balance — validation happens here
    bool deposit(double amount) {
        if (isLocked) {
            cout << "Account is locked! Contact support.\n";
            return false;
        }
        if (amount <= 0) {
            throw invalid_argument("Deposit amount must be positive");
        }
        balance += amount;
        cout << "Deposited ₹" << amount << " | New balance: ₹" << balance << "\n";
        return true;
    }

    bool withdraw(double amount, int enteredPin) {
        if (isLocked) {
            cout << "Account is locked!\n";
            return false;
        }
        if (!validatePin(enteredPin)) {
            failedAttempts++;
            cout << "Wrong PIN! Attempts: " << failedAttempts << "/3\n";
            if (failedAttempts >= 3) {
                isLocked = true;
                cout << "Account LOCKED due to too many wrong attempts!\n";
            }
            return false;
        }
        if (amount > balance) {
            cout << "Insufficient balance!\n";
            return false;
        }
        failedAttempts = 0; // reset on success
        balance -= amount;
        cout << "Withdrawn ₹" << amount << " | Remaining: ₹" << balance << "\n";
        return true;
    }

    // Read-only access — can't set balance directly!
    double getBalance(int enteredPin) {
        if (!validatePin(enteredPin)) return -1;
        return balance;
    }

    string getAccountNumber() const { return accountNumber; }
    string getOwnerName()     const { return ownerName; }
    bool   getIsLocked()      const { return isLocked; }
};

int main() {
    BankAccount acc("SB001234", "Rohit", 50000, 1234);

    acc.deposit(10000);
    acc.withdraw(5000, 1234);      // correct pin
    acc.withdraw(5000, 9999);      // wrong pin
    acc.withdraw(5000, 9999);
    acc.withdraw(5000, 9999);      // account locked now

    // ❌ Cannot directly access or modify balance
    // acc.balance = 9999999;  // Compilation Error!

    return 0;
}
```

> ✅ **Benefits of Encapsulation:**
> - Data validation on every write operation
> - Internal implementation can change without affecting external code
> - Prevents invalid states (e.g., negative balance)
> - Easier debugging — data can only change through known methods

---

# 6. Getters & Setters

Getters and setters provide **controlled read/write access** to private data.

```cpp
#include <iostream>
#include <string>
#include <stdexcept>
using namespace std;

class Student {
private:
    string name;
    int    rollNo;
    float  cgpa;
    int    age;

public:
    Student() : name("Unknown"), rollNo(0), cgpa(0.0f), age(0) {}

    Student(string n, int r, float c, int a)
        : name(n), rollNo(r), cgpa(c), age(a) {}

    // ── Getters (accessors) ──
    string getName()   const { return name; }
    int    getRollNo() const { return rollNo; }
    float  getCGPA()   const { return cgpa; }
    int    getAge()    const { return age; }

    // ── Setters (mutators) with validation ──
    void setName(const string& n) {
        if (n.empty()) throw invalid_argument("Name cannot be empty");
        name = n;
    }

    void setRollNo(int r) {
        if (r <= 0) throw invalid_argument("Roll number must be positive");
        rollNo = r;
    }

    void setCGPA(float c) {
        if (c < 0.0f || c > 10.0f)
            throw out_of_range("CGPA must be between 0.0 and 10.0");
        cgpa = c;
    }

    void setAge(int a) {
        if (a < 15 || a > 100)
            throw out_of_range("Age must be between 15 and 100");
        age = a;
    }

    // Computed property — no setter needed
    string getLetterGrade() const {
        if (cgpa >= 9.0f) return "O (Outstanding)";
        if (cgpa >= 8.0f) return "A+";
        if (cgpa >= 7.0f) return "A";
        if (cgpa >= 6.0f) return "B+";
        if (cgpa >= 5.0f) return "B";
        return "F";
    }

    void display() const {
        cout << "Name    : " << name         << endl;
        cout << "Roll No : " << rollNo       << endl;
        cout << "CGPA    : " << cgpa         << endl;
        cout << "Grade   : " << getLetterGrade() << endl;
        cout << "Age     : " << age          << endl;
    }
};

int main() {
    Student s("Rohit", 101, 9.2f, 21);
    s.display();

    cout << "\n--- Updating CGPA ---\n";
    s.setCGPA(8.5f);
    cout << "New Grade: " << s.getLetterGrade() << endl;

    cout << "\n--- Trying invalid CGPA ---\n";
    try {
        s.setCGPA(15.0f);  // throws exception
    } catch (const out_of_range& e) {
        cout << "Error: " << e.what() << endl;
    }

    return 0;
}
```

> 💡 **Best Practice:** Make setters return `*this` (or a bool/reference) to support **method chaining**:

```cpp
class Builder {
    string name;
    int age;

public:
    Builder& setName(string n) { name = n; return *this; }
    Builder& setAge(int a)     { age = a;  return *this; }
    void build() { cout << name << " | " << age << endl; }
};

// Usage
Builder().setName("Rohit").setAge(25).build(); // Method chaining!
```

---

# 7. Static Members

**Static members** belong to the **class itself**, not to any individual object. They're shared across all instances.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Employee {
    string name;
    double salary;
    int    empId;

    // Static data members — shared among all objects
    static int     totalEmployees;
    static double  totalSalaryBudget;
    static int     nextId;

public:
    Employee(string n, double s)
        : name(n), salary(s) {
        empId = nextId++;             // auto-assign ID
        totalEmployees++;
        totalSalaryBudget += salary;
        cout << "Employee #" << empId << " (" << name << ") created\n";
    }

    ~Employee() {
        totalEmployees--;
        totalSalaryBudget -= salary;
        cout << "Employee #" << empId << " (" << name << ") left\n";
    }

    // Static member functions — can only access static members
    static int    getTotalEmployees()    { return totalEmployees; }
    static double getTotalSalaryBudget() { return totalSalaryBudget; }
    static double getAverageSalary() {
        if (totalEmployees == 0) return 0;
        return totalSalaryBudget / totalEmployees;
    }

    // Non-static function — can access both static & non-static
    void display() const {
        cout << "ID: " << empId
             << " | Name: " << name
             << " | Salary: ₹" << salary << endl;
    }

    // Static constant
    static const string COMPANY_NAME;
};

// Define static members outside the class
int    Employee::totalEmployees    = 0;
double Employee::totalSalaryBudget = 0.0;
int    Employee::nextId            = 1001;
const string Employee::COMPANY_NAME = "TechCorp India";

int main() {
    cout << "Company: " << Employee::COMPANY_NAME << endl;
    cout << "Initial employees: " << Employee::getTotalEmployees() << "\n\n";

    Employee e1("Rohit",   75000);
    Employee e2("Priya",   90000);
    Employee e3("Aditya", 110000);

    cout << "\n--- Company Stats ---\n";
    cout << "Total Employees  : " << Employee::getTotalEmployees()    << endl;
    cout << "Total Budget     : ₹" << Employee::getTotalSalaryBudget() << endl;
    cout << "Average Salary   : ₹" << Employee::getAverageSalary()    << "\n\n";

    {
        Employee temp("Temp Worker", 30000);
        cout << "Employees now: " << Employee::getTotalEmployees() << "\n";
    }  // temp destroyed here

    cout << "Employees after: " << Employee::getTotalEmployees() << "\n";

    return 0;
}
```

### Static vs Non-Static

| Feature | Static Member | Non-Static Member |
|---|---|---|
| Belongs to | Class | Object (instance) |
| Memory | One copy for all objects | Separate copy per object |
| Access | `ClassName::member` | `object.member` |
| Accessed by | Static & non-static functions | Only non-static functions |
| Exists when | Program loads | Object is created |

---

# 8. this Pointer

The **`this` pointer** is an implicit pointer available inside every non-static member function. It points to the **current object** that called the method.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Rectangle {
    double width;
    double height;
    string color;

public:
    Rectangle(double w, double h, string c)
        : width(w), height(h), color(c) {}

    // 'this' resolves naming conflicts
    void setDimensions(double width, double height) {
        this->width  = width;  // this->width = member, width = parameter
        this->height = height;
    }

    // 'this' enables method chaining (fluent interface)
    Rectangle& setColor(string c) {
        color = c;
        return *this;   // return reference to current object
    }

    Rectangle& scale(double factor) {
        width  *= factor;
        height *= factor;
        return *this;
    }

    Rectangle& setWidth(double w) {
        width = w;
        return *this;
    }

    // Compare with another object using 'this'
    bool isLargerThan(const Rectangle& other) const {
        return (this->width * this->height) > (other.width * other.height);
    }

    void display() const {
        cout << "Rectangle [" << width << " x " << height
             << "] | Color: " << color
             << " | Area: " << (width * height) << endl;
    }
};

int main() {
    Rectangle r1(10, 5, "Red");
    r1.display();

    // Method chaining using 'this'
    r1.setColor("Blue").scale(2.0).setWidth(25);
    r1.display();

    Rectangle r2(20, 8, "Green");
    r2.display();

    cout << "r1 larger than r2? "
         << (r1.isLargerThan(r2) ? "Yes" : "No") << endl;

    return 0;
}
```

---

# 9. Friend Functions & Classes

A **friend function** or **friend class** can access the **private and protected** members of a class — breaking normal access control deliberately.

```cpp
#include <iostream>
#include <cmath>
using namespace std;

class Point {
    double x, y;   // private

public:
    Point(double x, double y) : x(x), y(y) {}

    void display() const {
        cout << "(" << x << ", " << y << ")";
    }

    // Declare friend function
    friend double distance(const Point& p1, const Point& p2);

    // Declare friend class
    friend class PointAnalyzer;
};

// Friend function — not a member, but has private access
double distance(const Point& p1, const Point& p2) {
    double dx = p1.x - p2.x;   // Can access p1.x (private)
    double dy = p1.y - p2.y;   // Can access p1.y (private)
    return sqrt(dx*dx + dy*dy);
}

// Friend class — all its methods have private access
class PointAnalyzer {
public:
    void analyze(const Point& p) {
        // Can access private x and y
        cout << "Analyzing point (" << p.x << ", " << p.y << ")\n";
        cout << "  Quadrant   : " << getQuadrant(p)         << endl;
        cout << "  Distance from origin: " << distFromOrigin(p) << endl;
    }

private:
    int getQuadrant(const Point& p) {
        if (p.x > 0 && p.y > 0) return 1;
        if (p.x < 0 && p.y > 0) return 2;
        if (p.x < 0 && p.y < 0) return 3;
        return 4;
    }

    double distFromOrigin(const Point& p) {
        return sqrt(p.x * p.x + p.y * p.y);
    }
};

int main() {
    Point p1(3.0, 4.0);
    Point p2(0.0, 0.0);

    cout << "Distance between ";
    p1.display();
    cout << " and ";
    p2.display();
    cout << " = " << distance(p1, p2) << endl;

    PointAnalyzer analyzer;
    analyzer.analyze(p1);

    return 0;
}
```

> ⚠️ **Use friends sparingly.** They break encapsulation. Common valid uses:
> - Overloading `<<` and `>>` operators
> - Mathematical operations between two classes
> - Unit testing frameworks (accessing internals for tests)

---

# 10. Inheritance

## Definition

**Inheritance** allows a class (derived/child) to **acquire properties and behaviors** of another class (base/parent). It promotes **code reuse** and establishes a natural hierarchy.

> 🧬 Think of it as a child inheriting traits from parents — but the child can also have their own unique traits and can modify inherited ones.

## Syntax

```cpp
class DerivedClass : accessSpecifier BaseClass {
    // additional members
};
```

## Example

```cpp
#include <iostream>
#include <string>
using namespace std;

// ── Base Class (Parent) ──
class Animal {
protected:
    string name;
    int    age;
    string sound;

public:
    Animal(string n, int a, string s)
        : name(n), age(a), sound(s) {
        cout << "Animal created: " << name << endl;
    }

    virtual ~Animal() {    // virtual destructor — very important!
        cout << "Animal destroyed: " << name << endl;
    }

    void eat()   { cout << name << " is eating 🍖\n"; }
    void sleep() { cout << name << " is sleeping 💤\n"; }

    virtual void makeSound() {
        cout << name << " says: " << sound << endl;
    }

    void displayBasicInfo() {
        cout << "Name: " << name << " | Age: " << age << " years\n";
    }
};

// ── Derived Class (Child) ──
class Dog : public Animal {
    string breed;
    string owner;

public:
    Dog(string n, int a, string b, string o)
        : Animal(n, a, "Woof!"),   // call base constructor
          breed(b), owner(o) {
        cout << "Dog created: " << name << "\n";
    }

    ~Dog() {
        cout << "Dog destroyed: " << name << "\n";
    }

    // Own method (not in base)
    void fetch(string item) {
        cout << name << " fetches the " << item << "! 🎾\n";
    }

    // Override base method
    void makeSound() override {
        cout << name << " barks loudly: WOOF WOOF! 🐕\n";
    }

    void displayInfo() {
        displayBasicInfo();    // inherited method
        cout << "Breed : " << breed << endl;
        cout << "Owner : " << owner << endl;
    }
};

class Cat : public Animal {
    bool isIndoor;

public:
    Cat(string n, int a, bool indoor)
        : Animal(n, a, "Meow~"), isIndoor(indoor) {}

    void makeSound() override {
        cout << name << " says: Purrrr... Meow~ 🐱\n";
    }

    void purr() { cout << name << " is purring... 😻\n"; }
};

int main() {
    Dog dog("Buddy",  3, "Golden Retriever", "Rohit");
    Cat cat("Whiskers", 2, true);

    cout << "\n--- Dog ---\n";
    dog.displayInfo();
    dog.eat();           // inherited from Animal
    dog.makeSound();     // overridden in Dog
    dog.fetch("ball");   // Dog-specific method

    cout << "\n--- Cat ---\n";
    cat.displayBasicInfo();  // inherited
    cat.makeSound();         // overridden
    cat.purr();              // Cat-specific

    return 0;
}
```

---

# 11. Types of Inheritance

C++ supports **5 types** of inheritance:

```
1. Single        A → B
2. Multiple      A, B → C
3. Multilevel    A → B → C
4. Hierarchical  A → B, A → C
5. Hybrid        Combination of above
```

## 1. Single Inheritance

```cpp
class Vehicle {
protected:
    string brand;
    int    speed;
public:
    Vehicle(string b, int s) : brand(b), speed(s) {}
    void displayVehicle() {
        cout << "Brand: " << brand << " | Speed: " << speed << " km/h\n";
    }
};

class Car : public Vehicle {   // Single inheritance
    int doors;
public:
    Car(string b, int s, int d) : Vehicle(b, s), doors(d) {}
    void displayCar() {
        displayVehicle();
        cout << "Doors: " << doors << endl;
    }
};
```

## 2. Multiple Inheritance

```cpp
class Flyable {
public:
    void fly() { cout << "Flying! ✈️\n"; }
};

class Swimmable {
public:
    void swim() { cout << "Swimming! 🏊\n"; }
};

// Inherits from TWO base classes
class Duck : public Flyable, public Swimmable {
    string name;
public:
    Duck(string n) : name(n) {}
    void quack() { cout << name << " says: Quack! 🦆\n"; }
};

int main() {
    Duck duck("Donald");
    duck.fly();     // from Flyable
    duck.swim();    // from Swimmable
    duck.quack();   // own method
}
```

## 3. Multilevel Inheritance

```cpp
class LivingBeing {
public:
    void breathe() { cout << "Breathing...\n"; }
};

class Animal2 : public LivingBeing {
public:
    void eat() { cout << "Eating...\n"; }
};

class Dog2 : public Animal2 {   // multilevel
public:
    void bark() { cout << "Barking! 🐕\n"; }
};

int main() {
    Dog2 dog;
    dog.breathe();   // from LivingBeing (grandparent)
    dog.eat();       // from Animal2 (parent)
    dog.bark();      // own method
}
```

## 4. Hierarchical Inheritance

```cpp
class Shape {
protected:
    string color;
public:
    Shape(string c) : color(c) {}
    void displayColor() { cout << "Color: " << color << endl; }
};

class Circle2 : public Shape {
    double radius;
public:
    Circle2(string c, double r) : Shape(c), radius(r) {}
    double area() { return 3.14159 * radius * radius; }
};

class Square : public Shape {
    double side;
public:
    Square(string c, double s) : Shape(c), side(s) {}
    double area() { return side * side; }
};

// Both Circle2 and Square inherit from Shape
```

## 5. Diamond Problem & Virtual Inheritance

```cpp
// Without virtual — ambiguity!
class A {
public:
    void show() { cout << "A::show()\n"; }
};

class B : virtual public A { };   // virtual inheritance
class C : virtual public A { };   // virtual inheritance

class D : public B, public C {    // only ONE copy of A
public:
    void test() { show(); }       // no ambiguity now!
};

int main() {
    D obj;
    obj.show();   // ✅ Works — virtual inheritance resolved diamond problem
}
```

### Inheritance Access Modes

| Base Access | public inheritance | protected inheritance | private inheritance |
|---|---|---|---|
| `public` | `public` | `protected` | `private` |
| `protected` | `protected` | `protected` | `private` |
| `private` | ❌ Not inherited | ❌ Not inherited | ❌ Not inherited |

---

## 📝 Exercises — Section 10 & 11

1. Create a hierarchy: `Person → Student → GraduateStudent`. Add unique attributes at each level.
2. Implement multiple inheritance: `FlyingVehicle`, `WaterVehicle` → `Seaplane`.
3. Demonstrate the diamond problem and fix it with virtual inheritance.

---

# 12. Polymorphism

## Definition

**Polymorphism** means *"many forms"*. The same function/operator behaves differently based on the context — same interface, different implementations.

**Two types:**
- **Compile-time polymorphism** (Static) → Function overloading, Operator overloading
- **Runtime polymorphism** (Dynamic) → Virtual functions, Function overriding

> 🎭 Think of a person who is a **Developer** at work, a **Son** at home, and a **Friend** with friends — same person, different behavior in different contexts.

---

# 13. Function Overloading

**Function overloading** = same function name, different parameters (type, count, or order). Resolved at **compile time**.

```cpp
#include <iostream>
#include <string>
using namespace std;

class MathUtils {
public:
    // Overloaded add() functions
    int add(int a, int b) {
        cout << "(int + int): ";
        return a + b;
    }

    double add(double a, double b) {
        cout << "(double + double): ";
        return a + b;
    }

    int add(int a, int b, int c) {
        cout << "(int + int + int): ";
        return a + b + c;
    }

    string add(string a, string b) {
        cout << "(string + string): ";
        return a + b;
    }

    double add(int a, double b) {   // different parameter types
        cout << "(int + double): ";
        return a + b;
    }
};

class Printer {
public:
    void print(int n)    { cout << "Integer: " << n    << endl; }
    void print(double d) { cout << "Double : " << d    << endl; }
    void print(string s) { cout << "String : " << s    << endl; }
    void print(char c)   { cout << "Char   : " << c    << endl; }
    void print(bool b)   { cout << "Bool   : " << boolalpha << b << endl; }
};

int main() {
    MathUtils math;
    cout << math.add(3, 4)           << endl;  // 7
    cout << math.add(3.5, 4.5)       << endl;  // 8.0
    cout << math.add(1, 2, 3)        << endl;  // 6
    cout << math.add("Hello", " C++") << endl; // Hello C++
    cout << math.add(5, 2.5)         << endl;  // 7.5

    cout << "\n";
    Printer p;
    p.print(42);
    p.print(3.14);
    p.print("Rohit");
    p.print('A');
    p.print(true);

    return 0;
}
```

> ⚠️ **Cannot overload by return type alone!**
> `int foo()` and `double foo()` — this is NOT valid overloading.

---

# 14. Operator Overloading

**Operator overloading** lets you define how operators (+, -, *, ==, <<, etc.) work with your custom classes.

```cpp
#include <iostream>
#include <string>
#include <cmath>
using namespace std;

class Vector2D {
    double x, y;

public:
    Vector2D(double x = 0, double y = 0) : x(x), y(y) {}

    // + operator (v1 + v2)
    Vector2D operator+(const Vector2D& other) const {
        return Vector2D(x + other.x, y + other.y);
    }

    // - operator (v1 - v2)
    Vector2D operator-(const Vector2D& other) const {
        return Vector2D(x - other.x, y - other.y);
    }

    // * operator (vector * scalar)
    Vector2D operator*(double scalar) const {
        return Vector2D(x * scalar, y * scalar);
    }

    // == operator (v1 == v2)
    bool operator==(const Vector2D& other) const {
        return (x == other.x && y == other.y);
    }

    // != operator
    bool operator!=(const Vector2D& other) const {
        return !(*this == other);
    }

    // += operator
    Vector2D& operator+=(const Vector2D& other) {
        x += other.x;
        y += other.y;
        return *this;
    }

    // Unary - operator (-v)
    Vector2D operator-() const {
        return Vector2D(-x, -y);
    }

    // [] operator (index access)
    double operator[](int index) const {
        if (index == 0) return x;
        if (index == 1) return y;
        throw out_of_range("Index must be 0 or 1");
    }

    // Magnitude
    double magnitude() const {
        return sqrt(x*x + y*y);
    }

    // << operator (friend — for output)
    friend ostream& operator<<(ostream& os, const Vector2D& v) {
        os << "(" << v.x << ", " << v.y << ")";
        return os;
    }

    // >> operator (friend — for input)
    friend istream& operator>>(istream& is, Vector2D& v) {
        is >> v.x >> v.y;
        return is;
    }
};

int main() {
    Vector2D v1(3, 4);
    Vector2D v2(1, 2);

    cout << "v1 = " << v1 << endl;
    cout << "v2 = " << v2 << endl;

    Vector2D sum  = v1 + v2;   cout << "v1 + v2 = " << sum  << endl;
    Vector2D diff = v1 - v2;   cout << "v1 - v2 = " << diff << endl;
    Vector2D scaled = v1 * 3;  cout << "v1 * 3  = " << scaled << endl;
    Vector2D neg = -v1;        cout << "-v1     = " << neg  << endl;

    cout << "v1 == v2 ? " << boolalpha << (v1 == v2) << endl;
    cout << "v1 magnitude: " << v1.magnitude() << endl;
    cout << "v1[0] = " << v1[0] << ", v1[1] = " << v1[1] << endl;

    v1 += v2;
    cout << "After v1 += v2: " << v1 << endl;

    // Read from input
    Vector2D v3;
    // cin >> v3;   // reads two doubles

    return 0;
}
```

### Operators That Can / Cannot Be Overloaded

| Can Overload | Cannot Overload |
|---|---|
| `+  -  *  /  %` | `::` (scope resolution) |
| `==  !=  <  >  <=  >=` | `.` (member access) |
| `[]  ()  ->  &` | `.*` (member pointer) |
| `<<  >>  !  ~` | `?:` (ternary) |
| `++  --  +=  -=` | `sizeof`, `typeid` |

---

# 15. Virtual Functions & Runtime Polymorphism

## Definition

**Virtual functions** enable **runtime polymorphism** — the correct function is chosen at **runtime** based on the actual object type, not the pointer/reference type.

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

class Shape {
protected:
    string color;

public:
    Shape(string c = "White") : color(c) {}

    virtual ~Shape() {}   // ← ALWAYS make destructor virtual in base class!

    // Virtual function — can be overridden
    virtual double area() const {
        return 0.0;
    }

    virtual double perimeter() const {
        return 0.0;
    }

    virtual void draw() const {
        cout << "Drawing a " << color << " shape\n";
    }

    // Non-virtual — always calls Shape's version
    void printColor() const {
        cout << "Color: " << color << endl;
    }
};

class Circle3 : public Shape {
    double radius;

public:
    Circle3(double r, string c = "Red") : Shape(c), radius(r) {}

    double area()      const override { return 3.14159 * radius * radius; }
    double perimeter() const override { return 2 * 3.14159 * radius; }

    void draw() const override {
        cout << "Drawing a " << color << " circle with radius " << radius << " 🔴\n";
    }
};

class Rectangle2 : public Shape {
    double width, height;

public:
    Rectangle2(double w, double h, string c = "Blue")
        : Shape(c), width(w), height(h) {}

    double area()      const override { return width * height; }
    double perimeter() const override { return 2 * (width + height); }

    void draw() const override {
        cout << "Drawing a " << color << " rectangle [" << width << "x" << height << "] 🟦\n";
    }
};

class Triangle : public Shape {
    double a, b, c;  // three sides

public:
    Triangle(double a, double b, double c, string color = "Green")
        : Shape(color), a(a), b(b), c(c) {}

    double perimeter() const override { return a + b + c; }

    double area() const override {
        double s = perimeter() / 2;
        return sqrt(s * (s-a) * (s-b) * (s-c));  // Heron's formula
    }

    void draw() const override {
        cout << "Drawing a " << color << " triangle 🔺\n";
    }
};

// Polymorphic function — works with ANY Shape
void printShapeInfo(const Shape& s) {
    s.draw();
    cout << "  Area      : " << s.area()      << endl;
    cout << "  Perimeter : " << s.perimeter() << endl;
}

int main() {
    // Base class pointers — polymorphism in action
    Shape* shapes[] = {
        new Circle3(5, "Red"),
        new Rectangle2(4, 6, "Blue"),
        new Triangle(3, 4, 5, "Green")
    };

    for (Shape* s : shapes) {
        printShapeInfo(*s);
        cout << endl;
    }

    // IMPORTANT: cleanup
    for (Shape* s : shapes) delete s;

    cout << "\n--- Using references ---\n";
    Circle3 c(7, "Orange");
    Shape& ref = c;   // Shape reference to Circle3 object
    ref.draw();       // Calls Circle3::draw() — runtime polymorphism!

    return 0;
}
```

## Virtual Function Table (vtable)

Internally, C++ uses a **vtable** (virtual table) to implement runtime polymorphism:

```
Shape object:
┌──────────────┐
│ vtable ptr ──┼──→ Shape vtable
│ color        │    ┌─────────────────┐
└──────────────┘    │ &Shape::area    │
                    │ &Shape::draw    │
                    └─────────────────┘

Circle3 object:
┌──────────────┐
│ vtable ptr ──┼──→ Circle3 vtable
│ color        │    ┌──────────────────┐
│ radius       │    │ &Circle3::area   │ ← overrides Shape's
└──────────────┘    │ &Circle3::draw   │ ← overrides Shape's
                    └──────────────────┘
```

> 💡 **Interview Tips:**
> - `virtual` functions have a small runtime cost (vtable lookup)
> - Always make the base class destructor `virtual` when using polymorphism
> - `override` keyword (C++11) is optional but recommended — catches typos at compile time
> - `final` keyword prevents further overriding: `void draw() const final {}`

---

# 16. Abstract Classes & Pure Virtual Functions

## Definition

A **pure virtual function** has no implementation in the base class — derived classes **must** override it.
A class with at least one pure virtual function is an **abstract class** — it cannot be instantiated directly.

```cpp
// Pure virtual function syntax
virtual returnType functionName(params) = 0;
```

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

// Abstract class — cannot create objects of this type
class PaymentMethod {
protected:
    string name;
    double transactionLimit;

public:
    PaymentMethod(string n, double limit)
        : name(n), transactionLimit(limit) {}

    virtual ~PaymentMethod() {}

    // Pure virtual functions — MUST be overridden
    virtual bool processPayment(double amount) = 0;
    virtual void displayDetails()              = 0;
    virtual string getPaymentType()      const = 0;

    // Concrete (non-abstract) method — shared by all
    bool validateAmount(double amount) const {
        if (amount <= 0) {
            cout << "Invalid amount!\n";
            return false;
        }
        if (amount > transactionLimit) {
            cout << "Amount exceeds limit of ₹" << transactionLimit << "\n";
            return false;
        }
        return true;
    }

    void printReceipt(double amount) const {
        cout << "✅ Payment of ₹" << amount
             << " via " << getPaymentType()
             << " successful!\n";
    }
};

// Concrete class — implements all pure virtual functions
class CreditCard : public PaymentMethod {
    string cardNumber;
    string holderName;
    int    cvv;

public:
    CreditCard(string name, string cardNo, string holder, int cvv, double limit)
        : PaymentMethod(name, limit), cardNumber(cardNo),
          holderName(holder), cvv(cvv) {}

    bool processPayment(double amount) override {
        if (!validateAmount(amount)) return false;
        cout << "Processing credit card payment...\n";
        // Simulate processing...
        printReceipt(amount);
        return true;
    }

    void displayDetails() override {
        cout << "Credit Card  : " << name << endl;
        cout << "Holder       : " << holderName << endl;
        cout << "Card Number  : ****-****-****-"
             << cardNumber.substr(cardNumber.size() - 4) << endl;
        cout << "Limit        : ₹" << transactionLimit << endl;
    }

    string getPaymentType() const override { return "Credit Card"; }
};

class UPIPayment : public PaymentMethod {
    string upiId;
    string bankName;

public:
    UPIPayment(string upiId, string bank, double limit)
        : PaymentMethod(upiId, limit), upiId(upiId), bankName(bank) {}

    bool processPayment(double amount) override {
        if (!validateAmount(amount)) return false;
        cout << "Sending payment request to UPI app...\n";
        printReceipt(amount);
        return true;
    }

    void displayDetails() override {
        cout << "UPI ID   : " << upiId   << endl;
        cout << "Bank     : " << bankName << endl;
        cout << "Limit    : ₹" << transactionLimit << endl;
    }

    string getPaymentType() const override { return "UPI"; }
};

class NetBanking : public PaymentMethod {
    string username;
    string bankCode;

public:
    NetBanking(string user, string code, double limit)
        : PaymentMethod(user, limit), username(user), bankCode(code) {}

    bool processPayment(double amount) override {
        if (!validateAmount(amount)) return false;
        cout << "Redirecting to " << bankCode << " net banking portal...\n";
        printReceipt(amount);
        return true;
    }

    void displayDetails() override {
        cout << "Username : " << username << endl;
        cout << "Bank     : " << bankCode << endl;
    }

    string getPaymentType() const override { return "Net Banking"; }
};

int main() {
    // PaymentMethod pm; // ❌ Cannot instantiate abstract class!

    vector<PaymentMethod*> methods = {
        new CreditCard("HDFC Regalia", "1234567890123456", "Rohit Kumar", 123, 200000),
        new UPIPayment("rohit@upi",    "HDFC Bank",   100000),
        new NetBanking("rohit_hdfcuser", "HDFC",      500000)
    };

    cout << "=== Available Payment Methods ===\n";
    for (auto* m : methods) {
        cout << "\n[" << m->getPaymentType() << "]\n";
        m->displayDetails();
    }

    cout << "\n=== Processing Payments ===\n";
    methods[0]->processPayment(15000);
    methods[1]->processPayment(2500);
    methods[2]->processPayment(750000); // exceeds limit

    for (auto* m : methods) delete m;
    return 0;
}
```

### Abstract Class vs Interface (in C++)

| Feature | Abstract Class | Pure Interface (all = 0) |
|---|---|---|
| Has implementation | ✅ Some methods | ❌ No methods |
| Has data members | ✅ Yes | ❌ Typically no |
| Constructor | ✅ Yes | ✅ (but rarely used) |
| Purpose | Partial blueprint | Contract only |
| C++ keyword | `virtual f() = 0` | `virtual f() = 0` (same syntax) |

---

# 17. Abstraction

## Definition

**Abstraction** means hiding **complex implementation details** and showing only the **essential features** to the user. It focuses on *what* an object does, not *how* it does it.

> 📱 When you press the power button on your phone — you don't know the circuit logic. You just see the screen turn on. That's abstraction.

```cpp
#include <iostream>
#include <string>
#include <stdexcept>
using namespace std;

// Abstraction through abstract class
class DatabaseConnection {
public:
    virtual ~DatabaseConnection() {}

    // Exposed interface (what users need to know)
    virtual void connect(string host, int port) = 0;
    virtual void disconnect()                   = 0;
    virtual bool executeQuery(string sql)       = 0;
    virtual string fetchResult()                = 0;

    // Convenience method using the abstract interface
    bool executeAndFetch(string sql, string& result) {
        if (!executeQuery(sql)) return false;
        result = fetchResult();
        return true;
    }
};

class MySQLConnection : public DatabaseConnection {
    string host;
    int    port;
    bool   connected;
    string lastResult;

    // Private (hidden) implementation details
    bool authenticate(string host, int port) {
        // Complex authentication logic hidden here
        cout << "  [Internal] Authenticating with MySQL at " << host << ":" << port << "\n";
        return true;
    }

    string parseQueryResult(string sql) {
        // Complex result parsing hidden here
        return "Result: 42 rows from '" + sql + "'";
    }

public:
    MySQLConnection() : connected(false) {}

    void connect(string h, int p) override {
        cout << "Connecting to MySQL...\n";
        if (!authenticate(h, p))
            throw runtime_error("Authentication failed");
        host      = h;
        port      = p;
        connected = true;
        cout << "✅ MySQL Connected!\n";
    }

    void disconnect() override {
        if (connected) {
            connected = false;
            cout << "MySQL Disconnected.\n";
        }
    }

    bool executeQuery(string sql) override {
        if (!connected) throw runtime_error("Not connected!");
        cout << "Executing: " << sql << "\n";
        lastResult = parseQueryResult(sql);
        return true;
    }

    string fetchResult() override {
        return lastResult;
    }
};

// User code — doesn't care about MySQL internals
void processData(DatabaseConnection& db) {
    db.connect("localhost", 3306);

    string result;
    db.executeAndFetch("SELECT * FROM users WHERE active=1", result);
    cout << result << "\n";

    db.disconnect();
}

int main() {
    MySQLConnection mysql;
    processData(mysql);
    // Could swap in PostgreSQLConnection without changing processData!
    return 0;
}
```

---

# 18. Interfaces in C++

C++ doesn't have a separate `interface` keyword (unlike Java), but we simulate interfaces using **abstract classes with all pure virtual functions**.

```cpp
#include <iostream>
#include <string>
using namespace std;

// Interface — all pure virtual, no data members
class ISerializable {
public:
    virtual ~ISerializable() {}
    virtual string   serialize()             const = 0;
    virtual void     deserialize(string data)      = 0;
};

class IPrintable {
public:
    virtual ~IPrintable() {}
    virtual void print() const = 0;
};

class IComparable {
public:
    virtual ~IComparable() {}
    virtual int compareTo(const IComparable& other) const = 0;
    virtual bool operator<(const IComparable& other) const = 0;
};

// A class implementing multiple interfaces
class User : public ISerializable, public IPrintable {
    int    id;
    string name;
    string email;

public:
    User(int i, string n, string e) : id(i), name(n), email(e) {}

    // ISerializable implementation
    string serialize() const override {
        return to_string(id) + "," + name + "," + email;
    }

    void deserialize(string data) override {
        size_t pos1 = data.find(',');
        size_t pos2 = data.find(',', pos1 + 1);
        id    = stoi(data.substr(0, pos1));
        name  = data.substr(pos1 + 1, pos2 - pos1 - 1);
        email = data.substr(pos2 + 1);
    }

    // IPrintable implementation
    void print() const override {
        cout << "User[" << id << "] " << name << " <" << email << ">\n";
    }

    int getId()    const { return id; }
    string getName() const { return name; }
};

void saveToFile(const ISerializable& obj) {
    cout << "Saving: " << obj.serialize() << "\n";
}

void displayObject(const IPrintable& obj) {
    obj.print();
}

int main() {
    User u(1, "Rohit", "rohit@dev.com");

    saveToFile(u);    // uses ISerializable interface
    displayObject(u); // uses IPrintable interface

    // Deserialize
    User u2(0, "", "");
    u2.deserialize("2,Priya,priya@dev.com");
    u2.print();

    return 0;
}
```

---

# 19. Templates (Generic Programming)

**Templates** allow writing **type-independent code** — write once, use with any type. This is C++'s form of generic programming.

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <stdexcept>
using namespace std;

// ── Function Template ──
template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

template <typename T>
void swap2(T& a, T& b) {
    T temp = a;
    a = b;
    b = temp;
}

// Multiple type parameters
template <typename T, typename U>
void printPair(T first, U second) {
    cout << "(" << first << ", " << second << ")\n";
}

// ── Class Template ──
template <typename T>
class Stack {
    vector<T> elements;
    int maxSize;

public:
    Stack(int size = 100) : maxSize(size) {}

    void push(const T& item) {
        if (isFull()) throw overflow_error("Stack overflow!");
        elements.push_back(item);
        cout << "Pushed: " << item << "\n";
    }

    T pop() {
        if (isEmpty()) throw underflow_error("Stack underflow!");
        T top = elements.back();
        elements.pop_back();
        cout << "Popped: " << top << "\n";
        return top;
    }

    T peek() const {
        if (isEmpty()) throw underflow_error("Stack is empty!");
        return elements.back();
    }

    bool isEmpty() const { return elements.empty(); }
    bool isFull()  const { return (int)elements.size() >= maxSize; }
    int  size()    const { return elements.size(); }

    void display() const {
        cout << "Stack [top → bottom]: ";
        for (int i = elements.size() - 1; i >= 0; i--) {
            cout << elements[i];
            if (i > 0) cout << " → ";
        }
        cout << endl;
    }
};

// ── Template Specialization ──
// Generic version
template <typename T>
class Printer2 {
public:
    void print(T value) {
        cout << "Value: " << value << endl;
    }
};

// Specialized version for bool
template <>
class Printer2<bool> {
public:
    void print(bool value) {
        cout << "Boolean: " << (value ? "TRUE ✅" : "FALSE ❌") << endl;
    }
};

// Specialized version for string
template <>
class Printer2<string> {
public:
    void print(string value) {
        cout << "String (length=" << value.length() << "): \"" << value << "\"\n";
    }
};

int main() {
    // Function templates
    cout << maximum(10, 20)      << endl;   // int version
    cout << maximum(3.14, 2.71)  << endl;   // double version
    cout << maximum('A', 'Z')    << endl;   // char version

    printPair("Name", "Rohit");
    printPair(42, 3.14);

    // Class templates
    Stack<int>    intStack(5);
    Stack<string> strStack(5);

    intStack.push(10);
    intStack.push(20);
    intStack.push(30);
    intStack.display();
    intStack.pop();
    intStack.display();

    strStack.push("Flutter");
    strStack.push("C++");
    strStack.push("Dart");
    strStack.display();

    // Template specialization
    Printer2<int>    pi;  pi.print(42);
    Printer2<bool>   pb;  pb.print(true);
    Printer2<string> ps;  ps.print("Hello C++");

    return 0;
}
```

---

# 20. Exception Handling

Exception handling allows programs to deal with **runtime errors** gracefully without crashing.

```cpp
#include <iostream>
#include <string>
#include <stdexcept>
using namespace std;

// Custom exception classes
class AppException : public exception {
    string message;
    int    errorCode;

public:
    AppException(string msg, int code = 0)
        : message(msg), errorCode(code) {}

    const char* what() const noexcept override {
        return message.c_str();
    }

    int getCode() const { return errorCode; }
};

class ValidationException : public AppException {
    string fieldName;
public:
    ValidationException(string field, string msg)
        : AppException(msg, 400), fieldName(field) {}

    string getField() const { return fieldName; }
};

class DatabaseException : public AppException {
public:
    DatabaseException(string msg)
        : AppException(msg, 500) {}
};

// ── Class using exception handling ──
class UserRegistration {
public:
    void validateAge(int age) {
        if (age < 0 || age > 150)
            throw ValidationException("age", "Age must be between 0 and 150");
        if (age < 18)
            throw ValidationException("age", "Must be 18 or older to register");
    }

    void validateEmail(const string& email) {
        if (email.empty())
            throw ValidationException("email", "Email cannot be empty");
        if (email.find('@') == string::npos)
            throw ValidationException("email", "Invalid email format");
    }

    void saveToDatabase(const string& email) {
        // Simulate DB error
        if (email == "error@test.com")
            throw DatabaseException("Failed to insert into database");
        cout << "User saved: " << email << "\n";
    }

    void registerUser(const string& email, int age) {
        try {
            validateEmail(email);
            validateAge(age);
            saveToDatabase(email);
            cout << "✅ Registration successful!\n";
        }
        catch (const ValidationException& e) {
            cout << "❌ Validation Error on '" << e.getField()
                 << "': " << e.what() << "\n";
        }
        catch (const DatabaseException& e) {
            cout << "💾 DB Error (code " << e.getCode()
                 << "): " << e.what() << "\n";
        }
        catch (const AppException& e) {
            cout << "⚠️ App Error: " << e.what() << "\n";
        }
        catch (...) {
            cout << "🔥 Unknown error occurred!\n";
        }
    }
};

int main() {
    UserRegistration reg;

    reg.registerUser("rohit@dev.com", 25);         // success
    reg.registerUser("invalid-email", 25);          // validation error
    reg.registerUser("rohit@dev.com", 16);          // age error
    reg.registerUser("error@test.com", 25);         // DB error

    // Standard exceptions
    try {
        vector<int> v = {1, 2, 3};
        cout << v.at(10);            // throws out_of_range
    } catch (const out_of_range& e) {
        cout << "Out of range: " << e.what() << "\n";
    }

    // noexcept — function guarantees no exception
    auto safeMax = [](int a, int b) noexcept -> int {
        return (a > b) ? a : b;
    };
    cout << "Max: " << safeMax(5, 10) << "\n";

    return 0;
}
```

### Exception Hierarchy

```
std::exception
├── std::logic_error
│   ├── std::invalid_argument
│   ├── std::domain_error
│   ├── std::length_error
│   └── std::out_of_range
├── std::runtime_error
│   ├── std::overflow_error
│   ├── std::underflow_error
│   └── std::range_error
└── std::bad_alloc (memory allocation failure)
```

---

# 21. File Handling with OOP

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <sstream>
using namespace std;

struct StudentRecord {
    int    id;
    string name;
    float  cgpa;

    string toString() const {
        return to_string(id) + "," + name + "," + to_string(cgpa);
    }

    static StudentRecord fromString(const string& line) {
        StudentRecord s;
        stringstream ss(line);
        string token;
        getline(ss, token, ','); s.id   = stoi(token);
        getline(ss, token, ','); s.name = token;
        getline(ss, token, ','); s.cgpa = stof(token);
        return s;
    }
};

class FileDatabase {
    string filename;

public:
    FileDatabase(string file) : filename(file) {}

    bool save(const vector<StudentRecord>& records) {
        ofstream file(filename);    // open for writing
        if (!file.is_open()) {
            cerr << "Error: Cannot open file for writing: " << filename << "\n";
            return false;
        }
        for (const auto& r : records) {
            file << r.toString() << "\n";
        }
        cout << "Saved " << records.size() << " records to " << filename << "\n";
        return true;
    }

    bool append(const StudentRecord& record) {
        ofstream file(filename, ios::app);  // append mode
        if (!file.is_open()) return false;
        file << record.toString() << "\n";
        return true;
    }

    vector<StudentRecord> load() {
        vector<StudentRecord> records;
        ifstream file(filename);    // open for reading
        if (!file.is_open()) {
            cerr << "Warning: File not found: " << filename << "\n";
            return records;
        }
        string line;
        while (getline(file, line)) {
            if (!line.empty()) {
                records.push_back(StudentRecord::fromString(line));
            }
        }
        cout << "Loaded " << records.size() << " records from " << filename << "\n";
        return records;
    }
};

int main() {
    FileDatabase db("students.csv");

    // Save records
    vector<StudentRecord> students = {
        {1, "Rohit",  9.2f},
        {2, "Priya",  8.8f},
        {3, "Aditya", 7.5f}
    };
    db.save(students);

    // Append a new record
    db.append({4, "Anjali", 9.5f});

    // Load and display
    auto loaded = db.load();
    cout << "\n--- Student Records ---\n";
    for (const auto& s : loaded) {
        cout << "ID: " << s.id
             << " | Name: " << s.name
             << " | CGPA: " << s.cgpa << "\n";
    }

    return 0;
}
```

---

# 22. Smart Pointers & OOP

Smart pointers automatically manage memory — no more `delete` calls, no memory leaks.

```cpp
#include <iostream>
#include <memory>   // for smart pointers
#include <string>
#include <vector>
using namespace std;

class Resource {
    string name;

public:
    Resource(string n) : name(n) {
        cout << "Resource '" << name << "' created\n";
    }
    ~Resource() {
        cout << "Resource '" << name << "' destroyed\n";
    }
    void use() { cout << "Using resource: " << name << "\n"; }
    string getName() const { return name; }
};

// ── unique_ptr — single owner ──
void demonstrateUniquePtr() {
    cout << "\n--- unique_ptr ---\n";

    unique_ptr<Resource> res1 = make_unique<Resource>("Config");
    res1->use();

    // Transfer ownership (move — not copy)
    unique_ptr<Resource> res2 = move(res1);
    // res1 is now nullptr
    if (!res1) cout << "res1 is empty after move\n";
    res2->use();

    // Automatically destroyed when res2 goes out of scope
}  // ← Resource destroyed here

// ── shared_ptr — multiple owners ──
void demonstrateSharedPtr() {
    cout << "\n--- shared_ptr ---\n";

    shared_ptr<Resource> s1 = make_shared<Resource>("Database");
    cout << "Count: " << s1.use_count() << "\n";  // 1

    {
        shared_ptr<Resource> s2 = s1;   // both point to same resource
        shared_ptr<Resource> s3 = s1;
        cout << "Count inside: " << s1.use_count() << "\n";  // 3
        s2->use();
    }  // s2, s3 destroyed — but resource lives on

    cout << "Count after scope: " << s1.use_count() << "\n";  // 1
}  // s1 destroyed → resource destroyed

// ── weak_ptr — non-owning reference ──
void demonstrateWeakPtr() {
    cout << "\n--- weak_ptr ---\n";

    shared_ptr<Resource> shared = make_shared<Resource>("Cache");
    weak_ptr<Resource>   weak   = shared;

    cout << "shared count: " << shared.use_count() << "\n";  // 1

    // Lock to use (may return nullptr if object destroyed)
    if (auto locked = weak.lock()) {
        locked->use();
        cout << "count with lock: " << shared.use_count() << "\n";  // 2
    }
    // locked goes out of scope → count back to 1
}

// OOP with smart pointers
class Node {
public:
    int value;
    shared_ptr<Node> next;
    Node(int v) : value(v) { cout << "Node " << v << " created\n"; }
    ~Node() { cout << "Node " << value << " destroyed\n"; }
};

int main() {
    demonstrateUniquePtr();
    demonstrateSharedPtr();
    demonstrateWeakPtr();

    // Smart pointer in class hierarchy
    cout << "\n--- OOP with smart pointers ---\n";
    vector<unique_ptr<Resource>> resources;
    resources.push_back(make_unique<Resource>("File"));
    resources.push_back(make_unique<Resource>("Network"));
    resources.push_back(make_unique<Resource>("Memory"));

    for (auto& r : resources) {
        r->use();
    }
    // All resources auto-destroyed when vector goes out of scope

    return 0;
}
```

---

# 23. Advanced OOP Concepts

## Copy vs Move Semantics (C++11)

```cpp
#include <iostream>
#include <string>
using namespace std;

class Buffer {
    int*   data;
    size_t size;

public:
    Buffer(size_t s) : size(s), data(new int[s]) {
        cout << "Constructor: allocated " << s << " ints\n";
    }

    // Copy constructor — deep copy
    Buffer(const Buffer& other) : size(other.size), data(new int[other.size]) {
        copy(other.data, other.data + size, data);
        cout << "Copy constructor: copied " << size << " ints\n";
    }

    // Move constructor — transfer ownership (no copying!)
    Buffer(Buffer&& other) noexcept : size(other.size), data(other.data) {
        other.data = nullptr;   // leave source in valid state
        other.size = 0;
        cout << "Move constructor: transferred ownership\n";
    }

    // Copy assignment
    Buffer& operator=(const Buffer& other) {
        if (this != &other) {
            delete[] data;
            size = other.size;
            data = new int[size];
            copy(other.data, other.data + size, data);
            cout << "Copy assignment\n";
        }
        return *this;
    }

    // Move assignment
    Buffer& operator=(Buffer&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data       = other.data;
            size       = other.size;
            other.data = nullptr;
            other.size = 0;
            cout << "Move assignment\n";
        }
        return *this;
    }

    ~Buffer() {
        delete[] data;
        cout << "Destructor: freed memory\n";
    }

    size_t getSize() const { return size; }
};

int main() {
    Buffer b1(100);           // constructor
    Buffer b2 = b1;           // copy constructor
    Buffer b3 = move(b1);     // move constructor (b1 is now empty)
    Buffer b4(50);
    b4 = b2;                  // copy assignment
    Buffer b5(50);
    b5 = move(b2);            // move assignment
    return 0;
}
```

---

## RAII (Resource Acquisition Is Initialization)

A fundamental C++ idiom — resources are tied to object lifetime.

```cpp
class MutexGuard {
    // Hypothetical mutex type
    Mutex& mutex;

public:
    MutexGuard(Mutex& m) : mutex(m) {
        mutex.lock();    // acquire resource in constructor
    }

    ~MutexGuard() {
        mutex.unlock();  // release resource in destructor — guaranteed!
    }

    // Prevent copying
    MutexGuard(const MutexGuard&) = delete;
    MutexGuard& operator=(const MutexGuard&) = delete;
};

void criticalSection(Mutex& m) {
    MutexGuard guard(m);  // lock acquired
    // ... do work ...
}   // ← lock automatically released even if exception thrown!
```

---

# 24. Design Patterns

## Singleton Pattern

Ensures only **one instance** of a class exists.

```cpp
class ConfigManager {
    static ConfigManager* instance;
    string configFile;
    // private data...

    // Private constructor
    ConfigManager() : configFile("config.json") {
        cout << "Loading config...\n";
    }

    // Delete copy operations
    ConfigManager(const ConfigManager&)            = delete;
    ConfigManager& operator=(const ConfigManager&) = delete;

public:
    // Global access point
    static ConfigManager& getInstance() {
        if (!instance) {
            instance = new ConfigManager();
        }
        return *instance;
    }

    string getConfigFile() const { return configFile; }
    void   setConfigFile(string f) { configFile = f; }
};

ConfigManager* ConfigManager::instance = nullptr;

int main() {
    ConfigManager& c1 = ConfigManager::getInstance();
    ConfigManager& c2 = ConfigManager::getInstance();
    cout << (&c1 == &c2 ? "Same instance ✅" : "Different instances ❌") << "\n";
}
```

## Factory Pattern

Creates objects without exposing the creation logic.

```cpp
class Animal3 {
public:
    virtual ~Animal3() {}
    virtual void speak() const = 0;
};

class Dog3 : public Animal3 {
public:
    void speak() const override { cout << "Woof! 🐕\n"; }
};

class Cat3 : public Animal3 {
public:
    void speak() const override { cout << "Meow! 🐱\n"; }
};

class Bird : public Animal3 {
public:
    void speak() const override { cout << "Tweet! 🐦\n"; }
};

// Factory
class AnimalFactory {
public:
    static unique_ptr<Animal3> create(const string& type) {
        if (type == "dog")  return make_unique<Dog3>();
        if (type == "cat")  return make_unique<Cat3>();
        if (type == "bird") return make_unique<Bird>();
        throw invalid_argument("Unknown animal type: " + type);
    }
};

int main() {
    auto dog  = AnimalFactory::create("dog");
    auto cat  = AnimalFactory::create("cat");
    auto bird = AnimalFactory::create("bird");

    dog->speak();
    cat->speak();
    bird->speak();
}
```

## Observer Pattern

Defines a one-to-many dependency — when one object changes state, all dependents are notified.

```cpp
#include <vector>
#include <algorithm>

class Observer {
public:
    virtual ~Observer() {}
    virtual void update(double price) = 0;
};

class StockMarket {
    double price;
    vector<Observer*> observers;

public:
    StockMarket(double p) : price(p) {}

    void subscribe(Observer* o) {
        observers.push_back(o);
    }

    void unsubscribe(Observer* o) {
        observers.erase(remove(observers.begin(), observers.end(), o), observers.end());
    }

    void setPrice(double newPrice) {
        price = newPrice;
        notifyAll();
    }

    void notifyAll() {
        for (auto* o : observers) o->update(price);
    }
};

class PriceAlert : public Observer {
    string name;
    double threshold;
public:
    PriceAlert(string n, double t) : name(n), threshold(t) {}

    void update(double price) override {
        if (price > threshold) {
            cout << "🔔 Alert [" << name << "]: Price " << price
                 << " exceeded threshold " << threshold << "\n";
        }
    }
};

int main() {
    StockMarket tata(1500);
    PriceAlert alert1("Investor A", 1800);
    PriceAlert alert2("Investor B", 2000);

    tata.subscribe(&alert1);
    tata.subscribe(&alert2);

    tata.setPrice(1900);  // alert1 triggers
    tata.setPrice(2100);  // both trigger
}
```

---

# 25. Best Practices

## Code Style

```cpp
// ✅ DO: Use meaningful names
class OrderProcessingService { };       // not "OPS" or "MyClass"
void calculateDiscountedPrice() { }     // not "calc" or "doStuff"

// ✅ DO: const-correctness
class Person {
    string name;
public:
    string getName() const { return name; }   // const method — doesn't modify object
    void setName(const string& n) { name = n; } // const reference parameter
};

// ✅ DO: Initialize in initializer list, not in body
class Config {
    int port;
    string host;
public:
    Config(int p, string h) : port(p), host(h) { }  // ✅
    // Config(int p, string h) { port = p; host = h; } // ❌ Assignment, not initialization
};

// ✅ DO: Use override keyword
class Base {
    virtual void foo() {}
};
class Derived : public Base {
    void foo() override {}   // compiler catches if Base doesn't have foo()
};

// ✅ DO: Use nullptr instead of NULL
int* p = nullptr;   // ✅
// int* p = NULL;   // ❌ old style

// ✅ DO: Use range-based for
vector<int> nums = {1,2,3};
for (const int& n : nums) { }   // ✅
// for (int i = 0; i < nums.size(); i++) { } // ❌ verbose
```

## Memory Management Rules

```cpp
// ✅ Rule of Zero — prefer letting compiler generate all special functions
class SimpleData {
    string name;
    int value;
public:
    SimpleData(string n, int v) : name(n), value(v) {}
    // No destructor, copy, move needed — compiler does it right
};

// ✅ Prefer smart pointers over raw pointers
auto obj = make_unique<MyClass>(args);  // ✅
// MyClass* obj = new MyClass(args);    // ❌ Must manually delete

// ✅ RAII for all resources
class DatabaseConn {
    // Connection handle
public:
    DatabaseConn()  { /* acquire */ }
    ~DatabaseConn() { /* release */ }  // guaranteed cleanup
};

// ✅ Avoid naked new/delete in modern C++
// If you must use raw pointers, delete in destructor
// and follow Rule of Three/Five
```

## Naming Conventions

```cpp
// Classes — PascalCase
class UserAccount { };
class HttpClient { };

// Methods & functions — camelCase
void getUserById(int id) { }
double calculateTax(double amount) { }

// Private members — underscore suffix or prefix
class Config {
    string host_;    // trailing underscore
    int    port_;
    // OR: string _host; int _port;  // leading underscore
};

// Constants — UPPER_SNAKE_CASE
const int    MAX_CONNECTIONS = 100;
const string DEFAULT_HOST    = "localhost";

// Template parameters — single letter or PascalCase
template <typename T>     { }   // single letter
template <typename TKey, typename TValue> { }  // descriptive
```

---

# 26. Exercises & Challenges

## 🟢 Beginner

1. **Library System** — Create `Book`, `Member`, and `Library` classes. Members can borrow/return books. Track availability.

2. **Simple Calculator** — Class-based calculator with operator overloading for `+`, `-`, `*`, `/` on a `Number` class with validation.

3. **Student Report Card** — `Student` class with subjects, marks, grade calculation, and file save/load.

## 🟡 Intermediate

4. **Shape Area Calculator** — Abstract `Shape` base class with `Circle`, `Rectangle`, `Triangle`, `Pentagon` subclasses. Vector of Shape pointers, polymorphic `area()` calls.

5. **Employee Payroll System** — `Employee` base with `FullTimeEmployee`, `PartTimeEmployee`, `Contractor` subclasses. Each has different `calculateSalary()`. Generate monthly report.

6. **Generic Linked List** — Template `LinkedList<T>` class with insert, delete, search, reverse, sort.

## 🔴 Advanced

7. **Bank Management System** — `Account` hierarchy (Savings, Current, FixedDeposit). Transactions, interest calculation, statement generation. Persistence to file.

8. **Mini Expression Engine** — Parse and evaluate math expressions like `"3 + 4 * 2"` using OOP (Token, Lexer, Parser, Evaluator classes).

9. **Thread-Safe Singleton Logger** — Logger class using Singleton pattern. Supports multiple log levels (DEBUG, INFO, WARN, ERROR). Write to file and console.

```cpp
// Starter for Challenge 9
class Logger {
    static Logger*   instance;
    static mutex     mtx;
    ofstream         logFile;
    LogLevel         minLevel;

    Logger();

public:
    enum class LogLevel { DEBUG, INFO, WARNING, ERROR };

    static Logger& getInstance() {
        lock_guard<mutex> lock(mtx);
        if (!instance) instance = new Logger();
        return *instance;
    }

    void log(LogLevel level, const string& message);
    void setMinLevel(LogLevel level) { minLevel = level; }
};

// Usage
Logger::getInstance().log(Logger::LogLevel::INFO, "Application started");
```

---

# 27. Conclusion & Resources

## 🎯 OOP in C++ Roadmap

```
Beginner
├── Classes & Objects
├── Constructors & Destructors
├── Access Modifiers
├── Encapsulation (Getters/Setters)
└── Basic Inheritance

Intermediate
├── Polymorphism (Overloading & Overriding)
├── Virtual Functions
├── Abstract Classes
├── Operator Overloading
└── Templates

Advanced
├── Smart Pointers & RAII
├── Move Semantics
├── Multiple Inheritance & Diamond
├── Design Patterns
└── Exception Handling

Expert
├── Template Metaprogramming
├── CRTP (Curiously Recurring Template Pattern)
├── Type Traits & Concepts (C++20)
└── Custom Allocators
```

## 📚 Recommended Books

| Book | Author | Level |
|---|---|---|
| *The C++ Programming Language* | Bjarne Stroustrup | All levels |
| *Effective C++* | Scott Meyers | Intermediate |
| *More Effective C++* | Scott Meyers | Intermediate |
| *Effective Modern C++* | Scott Meyers | Advanced |
| *Design Patterns* (GoF) | Gang of Four | Advanced |
| *C++ Primer* | Lippman & Lajoie | Beginner |

## 🌐 Online Resources

- 📖 [cppreference.com](https://cppreference.com) — The C++ bible
- 🎮 [Compiler Explorer](https://godbolt.org) — See generated assembly
- 💻 [OnlineGDB](https://www.onlinegdb.com/online_c++_compiler) — Online C++ compiler
- 📚 [LearnCpp.com](https://www.learncpp.com) — Free comprehensive tutorial
- 🏆 [LeetCode](https://leetcode.com) — Practice problems in C++

## 🛠️ Recommended Tools

| Tool | Purpose |
|---|---|
| **g++ / clang++** | Compilers |
| **Visual Studio** | Full IDE (Windows) |
| **VS Code + C++ Extension** | Lightweight editor |
| **CLion** | JetBrains C++ IDE |
| **Valgrind** | Memory leak detection |
| **GDB** | Debugger |
| **CMake** | Build system |

## 🎉 Conclusion

You've covered **OOP in C++ from zero to hero**! Here's your journey recap:

- ✅ **Core OOP** — Classes, Objects, Encapsulation, Abstraction
- ✅ **Inheritance** — Single, Multiple, Multilevel, Hierarchical, Diamond Problem
- ✅ **Polymorphism** — Function Overloading, Operator Overloading, Virtual Functions
- ✅ **Advanced** — Templates, Smart Pointers, Move Semantics, RAII
- ✅ **Design Patterns** — Singleton, Factory, Observer
- ✅ **Exception Handling** — Custom exceptions, hierarchy

### The 4 Pillars — Quick Recall

```
┌─────────────────────────────────────────────────────────┐
│  ENCAPSULATION  │  Bundle data + methods. Hide internals │
│  ABSTRACTION    │  Show only what's needed. Hide how.    │
│  INHERITANCE    │  Reuse code. IS-A relationship.         │
│  POLYMORPHISM   │  One interface, many forms.             │
└─────────────────────────────────────────────────────────┘
```

---

> 💙 *"C++ is designed to allow you to express ideas, but if you don't have ideas or don't have any clue about how to express them, C++ doesn't offer much help."* — Bjarne Stroustrup

**Happy Coding! Keep Building! 🚀**

---

*Made with ❤️ | C++17/20 | OOP Complete Reference | Last updated: 2024*
