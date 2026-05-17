# 🎯 Dart Programming — From Basics to Advanced

> A comprehensive, beginner-friendly guide to learning Dart — the language that powers Flutter.

---

## 📖 Introduction

**Dart** is a modern, object-oriented, strongly-typed programming language developed by **Google**. It was first unveiled in 2011 and has since evolved into a versatile language used for building fast, cross-platform applications.

Dart compiles to native machine code (for mobile/desktop) and JavaScript (for web), making it remarkably flexible. Its clean syntax feels familiar if you've used Java, C#, or JavaScript — making the learning curve approachable.

### 🚀 Why Learn Dart?

- ⚡ **Flutter's Language** — Flutter, Google's UI toolkit for building natively compiled apps for mobile, web, and desktop from a single codebase, is written entirely in Dart. Learning Dart **is** learning Flutter.
- 🔒 **Sound Null Safety** — Dart's null safety system catches null errors at compile time, not runtime — a huge win for reliability.
- 🏎️ **High Performance** — AOT (Ahead-of-Time) compilation makes Dart apps fast.
- 🧠 **Easy to Learn** — Clean syntax, strong tooling, and great documentation.
- 🌍 **Growing Ecosystem** — Flutter/Dart is one of the fastest-growing frameworks globally.

---

## 📚 Table of Contents

1. [Print Statement](#1-print-statement)
2. [Operators](#2-operators)
3. [Comments](#3-comments)
4. [Variables](#4-variables)
5. [Control Flow](#5-control-flow)
6. [Exercise 1](#6-exercise-1)
7. [Loops](#7-loops)
8. [Functions](#8-functions)
9. [Classes](#9-classes)
10. [Inheritance](#10-inheritance)
11. [implements Keyword](#11-implements-keyword)
12. [Abstract Classes](#12-abstract-classes)
13. [OOP in Dart](#13-object-oriented-programming-oop-in-dart)
14. [Polymorphism](#14-polymorphism)
15. [Abstraction](#15-abstraction)
16. [Encapsulation](#16-encapsulation)
17. [OOP Brief](#17-oop-brief)
18. [Mixins](#18-mixins)
19. [Class Modifiers](#19-class-modifiers)
20. [Lists](#20-lists)
21. [Sets](#21-sets)
22. [Maps](#22-maps)
23. [Enums](#23-enums)
24. [Exception Handling](#24-exception-handling)
25. [Futures](#25-futures)
26. [Streams](#26-streams)
27. [Creating Records](#27-creating-records)
28. [Patterns & Pattern Matching](#28-patterns--pattern-matching)
29. [Extensions](#29-extensions)
30. [Conclusion & Resources](#30-conclusion--resources)

---

## 1. 🖨️ Print Statement

### 📌 Definition
The `print()` function outputs text or values to the console. It's the simplest way to display output and debug your code.

### 📝 Theory
In Dart, `print()` accepts any object and calls `.toString()` on it automatically. It always adds a newline at the end.

### 🔤 Syntax
```dart
print(value);
print("String literal");
print("Interpolation: $variable");
print("Expression: ${object.property}");
```

### 🌍 Real-World Use Case
Displaying user information in a console app, logging debug output, or printing API responses during development.

### 💡 Example
```dart
void main() {
  String name = "Flutter Developer";
  int year = 2024;

  print("Hello, World!");                         // Simple string
  print(name);                                    // Variable
  print("Name: $name");                           // String interpolation
  print("Year: ${year + 1}");                     // Expression interpolation
  print("Pi is approx ${3.14159.toStringAsFixed(2)}"); // Method call
}
```

**Output:**
```
Hello, World!
Flutter Developer
Name: Flutter Developer
Year: 2025
Pi is approx 3.14
```

### ⚠️ Important Points
- `print()` adds a newline (`\n`) automatically.
- Use `stdout.write()` from `dart:io` if you want output **without** a newline.
- String interpolation uses `$variable` for simple values and `${expression}` for expressions.

> 💡 **Tip:** Use `debugPrint()` in Flutter instead of `print()` to avoid log truncation in release mode.

---

## 2. ➕ Operators

### 📌 Definition
Operators are special symbols that perform operations on operands (values/variables).

### 📝 Theory
Dart supports all standard operators plus some unique ones like the null-aware operators (`??`, `?.`, `??=`) which are essential in modern Dart.

### 🔤 Syntax & Categories

#### Arithmetic Operators
```dart
void main() {
  int a = 10, b = 3;

  print(a + b);   // 13  → Addition
  print(a - b);   // 7   → Subtraction
  print(a * b);   // 30  → Multiplication
  print(a / b);   // 3.333... → Division (returns double)
  print(a ~/ b);  // 3   → Integer Division (truncates decimal)
  print(a % b);   // 1   → Modulus (remainder)
}
```

#### Relational / Comparison Operators
```dart
void main() {
  print(5 > 3);   // true
  print(5 < 3);   // false
  print(5 >= 5);  // true
  print(5 <= 4);  // false
  print(5 == 5);  // true
  print(5 != 3);  // true
}
```

#### Logical Operators
```dart
void main() {
  bool isAdult = true;
  bool hasTicket = false;

  print(isAdult && hasTicket);  // false → AND: both must be true
  print(isAdult || hasTicket);  // true  → OR: at least one must be true
  print(!isAdult);              // false → NOT: flips the value
}
```

#### Assignment Operators
```dart
void main() {
  int x = 10;
  x += 5;   // x = x + 5  → 15
  x -= 3;   // x = x - 3  → 12
  x *= 2;   // x = x * 2  → 24
  x ~/= 4;  // x = x ~/ 4 → 6
  print(x); // 6
}
```

#### Null-Aware Operators ⭐ (Dart-specific)
```dart
void main() {
  String? name = null;

  // ?? → returns right side if left is null
  String display = name ?? "Anonymous";
  print(display); // Anonymous

  // ??= → assigns only if variable is null
  name ??= "Default";
  print(name); // Default

  // ?. → calls method only if object is not null
  String? city = null;
  print(city?.toUpperCase()); // null (no error!)
}
```

#### Type Test Operators
```dart
void main() {
  var value = 42;
  print(value is int);     // true
  print(value is! String); // true
}
```

### ⚠️ Important Points
- `~/` is integer division — unique to Dart (not `//` like Python).
- `??` is the null-coalescing operator — heavily used in Flutter.
- `==` checks value equality; use `identical()` for reference equality.

> 🧠 **Memory Trick:** Think of `??` as "if null, then use..." — it's your null safety net.

---

## 3. 💬 Comments

### 📌 Definition
Comments are non-executable text in your code that explain what the code does.

### 📝 Theory
Dart supports three types of comments. Documentation comments are especially important as tools like `dart doc` can generate HTML documentation from them.

### 🔤 Syntax
```dart
void main() {
  // Single-line comment — use for brief inline notes

  /*
    Multi-line comment — use for longer explanations
    that span multiple lines.
  */

  /// Documentation comment — use for public APIs and classes.
  /// Dart's doc generator (dart doc) reads these.
  /// Supports [markdown] and references to [ClassName].

  print("Comments don't affect execution"); // Inline comment
}
```

### 💡 Example with Documentation Comment
```dart
/// Calculates the area of a rectangle.
///
/// Takes [width] and [height] as parameters.
/// Returns the area as a [double].
double calculateArea(double width, double height) {
  return width * height; // Simple multiplication
}
```

### ⚠️ Important Points
- Comments are ignored by the Dart compiler.
- `///` doc comments support Markdown syntax.
- Avoid obvious comments like `// increment x` for `x++` — comment the *why*, not the *what*.

> 💡 **Best Practice:** Write comments to explain **intent**, not just **mechanism**. Future-you will thank you.

---

## 4. 📦 Variables

### 📌 Definition
Variables are named containers that store data values in memory.

### 📝 Theory
Dart is strongly typed, but also supports type inference via `var`. Variables can be mutable or immutable (`final`/`const`). All variables in Dart are objects — even `int` and `bool`.

### 🔤 Syntax
```dart
// Explicit type
String name = "Dart";
int age = 10;
double pi = 3.14;
bool isOpen = true;

// Type inference (Dart figures out the type)
var language = "Dart";  // inferred as String
var count = 42;         // inferred as int

// Nullable variables (can hold null)
String? middleName = null;

// Immutable variables
final String country = "India"; // Set once at runtime
const double gravity = 9.8;    // Set at compile time
```

### 💡 Full Example
```dart
void main() {
  // Mutable variable — can be changed later
  var score = 0;
  score = 100;
  print(score); // 100

  // final — set once, cannot be reassigned
  final String appName = "MyApp";
  // appName = "NewApp"; // ❌ Error: cannot reassign final

  // const — compile-time constant
  const double taxRate = 0.18;
  print("Tax Rate: $taxRate");

  // Nullable — explicit null handling
  String? username;
  print(username ?? "Guest"); // Guest (username is null)
  username = "Alice";
  print(username); // Alice

  // Dynamic — avoid in production code!
  dynamic anything = 42;
  anything = "Now I'm a string"; // No error, but no type safety
  print(anything);
}
```

### 📊 Variable Comparison Table

| Keyword | Mutable | When Set | Use Case |
|---------|---------|----------|----------|
| `var` | ✅ Yes | Runtime | General variables with inference |
| `final` | ❌ No | Runtime | Values set once (e.g., fetched data) |
| `const` | ❌ No | Compile Time | True constants (PI, gravity) |
| `dynamic` | ✅ Yes | Runtime | Avoid — loses type safety |
| `late` | ✅ Yes | Deferred | Variables initialized after declaration |

### ⚠️ Important Points
- Prefer `final` over `var` when the value won't change.
- Prefer `const` over `final` for compile-time constants.
- `late` keyword: `late String name;` — tells Dart "I'll initialize this before I use it."
- `String?` vs `String` — the `?` makes it nullable. Without `?`, it can never be null.

> 🧠 **Interview Tip:** Know the difference between `final` and `const`. `const` values are embedded into the compiled binary; `final` values are computed at runtime.

---

## 5. 🔀 Control Flow

### 📌 Definition
Control flow statements determine the order in which code is executed based on conditions.

### 📝 Theory
Dart provides `if/else`, `switch`, and ternary operators for conditional branching.

### 🔤 Syntax & Examples

#### if / else if / else
```dart
void main() {
  int temperature = 38;

  if (temperature > 40) {
    print("Extremely hot! 🔥");
  } else if (temperature > 35) {
    print("Very hot! Stay hydrated. 💧");
  } else if (temperature > 25) {
    print("Warm and pleasant. 🌤️");
  } else {
    print("Cool or cold. 🧊");
  }
}
```

#### Ternary Operator
```dart
void main() {
  int marks = 75;

  // condition ? value_if_true : value_if_false
  String result = marks >= 50 ? "Pass ✅" : "Fail ❌";
  print(result); // Pass ✅
}
```

#### switch Statement
```dart
void main() {
  String day = "Monday";

  switch (day) {
    case "Monday":
    case "Tuesday":
    case "Wednesday":
    case "Thursday":
    case "Friday":
      print("Weekday — time to work! 💼");
      break;
    case "Saturday":
    case "Sunday":
      print("Weekend — time to rest! 🛋️");
      break;
    default:
      print("Invalid day");
  }
}
```

#### switch Expression (Dart 3+) ⭐
```dart
void main() {
  String day = "Saturday";

  // Modern switch — much cleaner!
  String type = switch (day) {
    "Saturday" || "Sunday" => "Weekend 🎉",
    "Monday" || "Tuesday" || "Wednesday" || "Thursday" || "Friday" => "Weekday 💼",
    _ => "Invalid", // _ is the default wildcard
  };

  print(type); // Weekend 🎉
}
```

### ⚠️ Important Points
- Traditional `switch` requires `break` to prevent fall-through.
- Dart 3 switch expressions are more concise and return a value directly.
- The `_` (underscore) acts as the default wildcard in pattern matching.

---

## 6. 🏋️ Exercise 1

Practice what you've learned so far!

```dart
// Exercise 1: Grade Calculator
// Write a program that:
// 1. Takes a student's marks (0-100)
// 2. Prints their grade based on:
//    90-100 → A+
//    80-89  → A
//    70-79  → B
//    60-69  → C
//    50-59  → D
//    Below 50 → Fail

void main() {
  int marks = 85; // Change this to test different values

  // YOUR SOLUTION HERE:
  String grade;

  if (marks >= 90) {
    grade = "A+";
  } else if (marks >= 80) {
    grade = "A";
  } else if (marks >= 70) {
    grade = "B";
  } else if (marks >= 60) {
    grade = "C";
  } else if (marks >= 50) {
    grade = "D";
  } else {
    grade = "Fail";
  }

  print("Marks: $marks → Grade: $grade");

  // Bonus: Try writing this using a switch expression!
}
```

**Try These:**
1. Modify to print the percentage alongside the grade.
2. Add special messages for perfect scores (100) and failing scores (0).
3. Refactor using a switch expression (Dart 3).

---

## 7. 🔁 Loops

### 📌 Definition
Loops execute a block of code repeatedly until a condition is met.

### 📝 Theory
Dart provides `for`, `while`, `do-while`, and `for-in` loops. Each suits different scenarios.

### 🔤 Syntax & Examples

#### for Loop
```dart
void main() {
  // Standard for loop
  for (int i = 1; i <= 5; i++) {
    print("Count: $i");
  }

  // Counting backwards
  for (int i = 5; i >= 1; i--) {
    print("Countdown: $i");
  }
}
```

#### while Loop
```dart
void main() {
  int balance = 1000;
  int withdrawal = 300;

  // Keep withdrawing while balance is sufficient
  while (balance >= withdrawal) {
    balance -= withdrawal;
    print("Withdrew $withdrawal. Remaining: $balance");
  }

  print("Insufficient balance. Final balance: $balance");
}
```

#### do-while Loop
```dart
void main() {
  int attempts = 0;

  // Executes at least ONCE, then checks condition
  do {
    attempts++;
    print("Attempt $attempts: Trying to connect...");
  } while (attempts < 3);

  print("Connection attempts exhausted.");
}
```

#### for-in Loop
```dart
void main() {
  List<String> fruits = ["Apple", "Banana", "Cherry"];

  // Iterate over each element
  for (String fruit in fruits) {
    print("🍎 Fruit: $fruit");
  }
}
```

#### forEach with Arrow Function
```dart
void main() {
  List<int> numbers = [1, 2, 3, 4, 5];

  numbers.forEach((n) => print("Number: $n"));
  // Or with named function:
  // numbers.forEach(print);
}
```

#### break and continue
```dart
void main() {
  for (int i = 1; i <= 10; i++) {
    if (i == 4) continue; // Skip 4
    if (i == 7) break;    // Stop at 7

    print(i); // Prints: 1, 2, 3, 5, 6
  }
}
```

### ⚠️ Important Points
- `for-in` is cleaner when you don't need the index.
- Use `forEach` for functional-style iteration.
- `do-while` guarantees at least one execution — useful for menu-driven programs.
- Avoid infinite loops: always ensure your loop condition will eventually be false.

> 💡 **Tip:** Prefer `for-in` or `forEach` over index-based `for` when you don't need the index — it's more readable and less error-prone.

---

## 8. 🔧 Functions

### 📌 Definition
A function is a reusable block of code that performs a specific task.

### 📝 Theory
In Dart, functions are first-class objects — they can be assigned to variables, passed as arguments, and returned from other functions. This enables functional programming patterns.

### 🔤 Syntax & Examples

#### Basic Function
```dart
// Return type  Function name  Parameters
int add(int a, int b) {
  return a + b;
}

void main() {
  int result = add(3, 5);
  print(result); // 8
}
```

#### void Function (no return value)
```dart
void greet(String name) {
  print("Hello, $name! 👋");
}

void main() {
  greet("Alice"); // Hello, Alice! 👋
}
```

#### Arrow Function (single expression)
```dart
// Full form:
int multiply(int a, int b) {
  return a * b;
}

// Arrow shorthand:
int multiplyArrow(int a, int b) => a * b;

void main() {
  print(multiplyArrow(4, 5)); // 20
}
```

#### Named Parameters
```dart
// Named parameters are optional by default; use required to force them
void createUser({
  required String name,
  int age = 18,       // Default value
  String? email,      // Optional nullable
}) {
  print("Name: $name, Age: $age, Email: ${email ?? 'N/A'}");
}

void main() {
  createUser(name: "Bob");                          // Uses defaults
  createUser(name: "Alice", age: 25, email: "a@b.com"); // All params
}
```

#### Positional Optional Parameters
```dart
String greet(String name, [String greeting = "Hello"]) {
  return "$greeting, $name!";
}

void main() {
  print(greet("Alice"));           // Hello, Alice!
  print(greet("Bob", "Hi there")); // Hi there, Bob!
}
```

#### Functions as First-Class Objects
```dart
// Function assigned to a variable
var square = (int n) => n * n;

// Function as a parameter (Higher-Order Function)
void applyAndPrint(int value, int Function(int) operation) {
  print(operation(value));
}

void main() {
  print(square(5)); // 25

  applyAndPrint(4, square);           // 16
  applyAndPrint(3, (n) => n * n * n); // 27 (cube)
}
```

#### Closures
```dart
// A closure captures variables from its surrounding scope
Function makeCounter() {
  int count = 0; // This variable is "closed over"

  return () {
    count++;
    print("Count: $count");
  };
}

void main() {
  var counter = makeCounter();
  counter(); // Count: 1
  counter(); // Count: 2
  counter(); // Count: 3
}
```

### ⚠️ Important Points
- Named parameters use `{}` braces; positional optional use `[]` brackets.
- Use `required` keyword to make named parameters mandatory.
- Arrow functions work only for single-expression functions.
- Closures are powerful — used extensively in Flutter's `setState` and callbacks.

> 🧠 **Interview Tip:** Know the difference between named `{}` and positional optional `[]` parameters. Named parameters are Flutter's preferred style for widget constructors.

---

## 9. 🏗️ Classes

### 📌 Definition
A class is a blueprint for creating objects that bundle data (properties) and behavior (methods).

### 📝 Theory
Dart is a fully object-oriented language. Everything is an object. Classes define the structure and capabilities of objects.

### 🔤 Syntax & Example
```dart
// Class definition
class Car {
  // Properties (fields)
  String brand;
  String model;
  int year;
  double _price; // _ prefix = private in Dart

  // Constructor
  Car(this.brand, this.model, this.year, this._price);

  // Named constructor
  Car.luxury(String brand) : this(brand, "Luxury Edition", 2024, 5000000.0);

  // Method
  void displayInfo() {
    print("$year $brand $model — ₹${_price.toStringAsFixed(0)}");
  }

  // Getter
  double get price => _price;

  // Setter with validation
  set price(double value) {
    if (value > 0) {
      _price = value;
    } else {
      throw ArgumentError("Price must be positive");
    }
  }

  // Override toString for readable output
  @override
  String toString() => "$brand $model ($year)";
}

void main() {
  // Create objects (instances)
  Car myCar = Car("Toyota", "Corolla", 2023, 1800000.0);
  myCar.displayInfo();

  // Using named constructor
  Car luxuryCar = Car.luxury("BMW");
  luxuryCar.displayInfo();

  // Using getter/setter
  myCar.price = 2000000.0;
  print("Updated price: ₹${myCar.price}");

  // toString override
  print(myCar); // Toyota Corolla (2023)
}
```

### ⚠️ Important Points
- Properties starting with `_` are private to the **library** (file), not just the class.
- Dart doesn't have `public`/`private`/`protected` keywords — visibility is library-based.
- Named constructors allow multiple ways to create objects.
- Always override `toString()` for meaningful debug output.

> 💡 **Tip:** Use `this.property` syntax in constructors for concise initialization — called "initializing formals".

---

## 10. 🧬 Inheritance

### 📌 Definition
Inheritance allows a class (child/subclass) to acquire properties and methods from another class (parent/superclass).

### 📝 Theory
Dart supports **single inheritance** — a class can extend only one parent. Use `extends` keyword. The child class can override parent methods and call parent constructors using `super`.

### 🔤 Syntax & Example
```dart
// Parent class
class Animal {
  String name;
  int age;

  Animal(this.name, this.age);

  void breathe() {
    print("$name is breathing...");
  }

  void eat() {
    print("$name is eating.");
  }

  @override
  String toString() => "Animal($name, age: $age)";
}

// Child class — inherits from Animal
class Dog extends Animal {
  String breed;

  // super() calls the parent constructor
  Dog(String name, int age, this.breed) : super(name, age);

  // New method specific to Dog
  void bark() {
    print("$name says: Woof! 🐕");
  }

  // Override parent method
  @override
  void eat() {
    super.eat(); // Call parent's eat()
    print("$name wags tail while eating! 🐾");
  }
}

class Cat extends Animal {
  Cat(String name, int age) : super(name, age);

  void meow() {
    print("$name says: Meow! 🐈");
  }
}

void main() {
  Dog dog = Dog("Buddy", 3, "Labrador");
  dog.breathe();  // Inherited from Animal
  dog.eat();      // Overridden method
  dog.bark();     // Dog-specific method

  Cat cat = Cat("Whiskers", 5);
  cat.breathe();  // Inherited
  cat.meow();     // Cat-specific

  // A Dog IS-A Animal (polymorphism)
  Animal a = Dog("Rex", 2, "German Shepherd");
  a.eat(); // Calls Dog's overridden eat()
}
```

### ⚠️ Important Points
- Dart supports only **single inheritance** (one parent class only).
- Use `@override` annotation when overriding — it catches typos and ensures the parent method exists.
- `super` accesses the parent class's methods and constructors.
- The child class inherits all non-private members.

> 🧠 **Memory Trick:** Think of inheritance as an "IS-A" relationship: A Dog **IS-A** Animal.

---

## 11. 🔌 implements Keyword

### 📌 Definition
`implements` forces a class to provide concrete implementations of all methods defined in another class or abstract class (used as an interface).

### 📝 Theory
Unlike `extends`, `implements` does NOT inherit the implementation — only the contract (method signatures). A class can `implement` **multiple** classes, solving Dart's single inheritance limitation.

### 🔤 Syntax & Example
```dart
// Used as an interface (contract)
class Flyable {
  void fly() {
    print("Flying generically");
  }

  void land() {
    print("Landing generically");
  }
}

class Swimmable {
  void swim() {
    print("Swimming generically");
  }
}

// Duck implements both — must provide ALL methods
class Duck implements Flyable, Swimmable {
  String name;
  Duck(this.name);

  @override
  void fly() {
    print("$name is flying with wings! 🦆");
  }

  @override
  void land() {
    print("$name lands on water.");
  }

  @override
  void swim() {
    print("$name is swimming happily! 🌊");
  }

  void quack() {
    print("$name says: Quack!");
  }
}

void main() {
  Duck duck = Duck("Donald");
  duck.fly();
  duck.swim();
  duck.quack();
}
```

### 📊 extends vs implements

| Feature | `extends` | `implements` |
|---------|-----------|--------------|
| Inherits implementation | ✅ Yes | ❌ No |
| Must override all methods | ❌ No | ✅ Yes |
| Multiple classes | ❌ No (single) | ✅ Yes (multiple) |
| IS-A relationship | ✅ True subtype | ✅ Also true |
| Use case | Code reuse | Define contracts |

> 💡 **Best Practice:** Prefer `abstract classes` as interfaces in Dart over concrete classes — it's clearer that they define a contract.

---

## 12. 🎭 Abstract Classes

### 📌 Definition
An abstract class is a class that **cannot be instantiated directly** and may contain abstract methods — methods with no body that subclasses must implement.

### 📝 Theory
Abstract classes define a common interface/contract for a group of related classes. They can have both concrete (implemented) and abstract (unimplemented) methods.

### 🔤 Syntax & Example
```dart
// Abstract class — cannot create an instance directly
abstract class Shape {
  // Abstract method — no body, must be overridden
  double area();
  double perimeter();

  // Concrete method — has implementation, can be inherited
  void describe() {
    print("I am a shape with area: ${area().toStringAsFixed(2)}");
  }
}

// Concrete subclass
class Circle extends Shape {
  double radius;
  Circle(this.radius);

  @override
  double area() => 3.14159 * radius * radius;

  @override
  double perimeter() => 2 * 3.14159 * radius;
}

class Rectangle extends Shape {
  double width, height;
  Rectangle(this.width, this.height);

  @override
  double area() => width * height;

  @override
  double perimeter() => 2 * (width + height);
}

void main() {
  // Shape s = Shape(); // ❌ Error: Cannot instantiate abstract class

  Shape circle = Circle(5.0);
  Shape rectangle = Rectangle(4.0, 6.0);

  circle.describe();       // Uses concrete method from Shape
  print(circle.area());    // 78.53...

  rectangle.describe();
  print(rectangle.perimeter()); // 20.0
}
```

### ⚠️ Important Points
- Abstract classes cannot be instantiated.
- All abstract methods MUST be implemented by concrete subclasses.
- Abstract classes can have constructors (used by subclasses via `super`).
- Use when you have shared behavior + forced contract.

> 🧠 **Interview Tip:** "When would you use abstract class vs interface?" — Use abstract class when there's shared code to reuse. Use interface (or abstract class with all abstract methods) when you only need a contract.

---

## 13. 🏛️ Object-Oriented Programming (OOP) in Dart

### 📌 Definition
OOP is a programming paradigm that organizes code around **objects** — combining data and behavior — rather than functions and logic.

### 📝 Theory
Dart is a pure OOP language. The four pillars of OOP are:
- **Encapsulation** — Bundling data and restricting access
- **Inheritance** — Reusing code from parent classes
- **Polymorphism** — Same interface, different behavior
- **Abstraction** — Hiding complexity, exposing essentials

### 💡 OOP in Action: A Complete Example
```dart
// Abstraction via abstract class
abstract class BankAccount {
  String accountNumber;
  double _balance; // Encapsulation: private field

  BankAccount(this.accountNumber, this._balance);

  // Abstract methods — subclasses define the rules
  void deposit(double amount);
  void withdraw(double amount);

  // Concrete — shared across all accounts
  double get balance => _balance;

  void printBalance() {
    print("Account $accountNumber: ₹${_balance.toStringAsFixed(2)}");
  }
}

// Inheritance: SavingsAccount IS-A BankAccount
class SavingsAccount extends BankAccount {
  double interestRate;

  SavingsAccount(String accNum, double balance, this.interestRate)
      : super(accNum, balance);

  @override
  void deposit(double amount) {
    _balance += amount;
    print("Deposited ₹$amount to savings.");
  }

  @override
  void withdraw(double amount) {
    if (amount <= _balance) {
      _balance -= amount;
      print("Withdrew ₹$amount from savings.");
    } else {
      print("Insufficient funds!");
    }
  }

  void addInterest() {
    double interest = _balance * interestRate / 100;
    _balance += interest;
    print("Interest added: ₹${interest.toStringAsFixed(2)}");
  }
}

void main() {
  BankAccount acc = SavingsAccount("SB001", 10000.0, 4.5);
  acc.deposit(5000);     // Polymorphism
  acc.withdraw(2000);
  acc.printBalance();
  (acc as SavingsAccount).addInterest();
  acc.printBalance();
}
```

---

## 14. 🦋 Polymorphism

### 📌 Definition
Polymorphism means "many forms" — the ability of different objects to respond to the same message (method call) in their own way.

### 📝 Theory
In Dart, polymorphism is achieved through **method overriding**. A parent class reference can hold a child class object and call overridden methods — which execute the child's version.

### 💡 Example
```dart
abstract class Instrument {
  void play(); // Each instrument plays differently
}

class Guitar extends Instrument {
  @override
  void play() => print("🎸 Strumming the guitar...");
}

class Piano extends Instrument {
  @override
  void play() => print("🎹 Playing the piano keys...");
}

class Drums extends Instrument {
  @override
  void play() => print("🥁 Beating the drums...");
}

void performConcert(List<Instrument> instruments) {
  // Polymorphism: same method, different behavior
  for (var instrument in instruments) {
    instrument.play(); // Calls each class's own play()
  }
}

void main() {
  List<Instrument> band = [Guitar(), Piano(), Drums()];
  performConcert(band);
}
```

**Output:**
```
🎸 Strumming the guitar...
🎹 Playing the piano keys...
🥁 Beating the drums...
```

### ⚠️ Important Points
- Runtime polymorphism is achieved via method overriding.
- The actual type of the object (not the reference type) determines which method runs.
- Polymorphism enables writing generic code that works with any subtype.

---

## 15. 🎭 Abstraction

### 📌 Definition
Abstraction means hiding the complex implementation details and showing only the essential features to the user.

### 📝 Theory
In Dart, abstraction is achieved through `abstract classes` and `interfaces`. The user interacts with a simplified API without needing to know the internals.

### 💡 Real-World Example
```dart
// Abstraction: User just calls start()/stop() — doesn't care HOW it works
abstract class Vehicle {
  void start();
  void stop();
  void refuel();
}

class ElectricCar extends Vehicle {
  @override
  void start() => print("⚡ Electric motor silently starts");

  @override
  void stop() => print("🔋 Regenerative braking engaged");

  @override
  void refuel() => print("🔌 Charging battery...");
}

class PetrolCar extends Vehicle {
  @override
  void start() => print("🔑 Engine ignites with a roar");

  @override
  void stop() => print("🛑 Brakes applied");

  @override
  void refuel() => print("⛽ Filling petrol tank...");
}

void main() {
  Vehicle car = ElectricCar();
  car.start();  // User doesn't know how
  car.refuel(); // Simple interface, complex hidden logic
  car.stop();
}
```

---

## 16. 🔒 Encapsulation

### 📌 Definition
Encapsulation is bundling data (properties) and methods that operate on that data within a single unit (class), and restricting direct access to some components.

### 📝 Theory
In Dart, encapsulation is achieved using the `_` prefix for private members and getters/setters for controlled access.

### 💡 Example
```dart
class Employee {
  String _name;      // Private
  double _salary;   // Private
  int _age;         // Private

  Employee(this._name, this._salary, this._age);

  // Controlled read access (getter)
  String get name => _name;
  double get salary => _salary;

  // Controlled write access with validation (setter)
  set salary(double value) {
    if (value < 15000) {
      throw ArgumentError("Salary below minimum wage!");
    }
    _salary = value;
  }

  set age(int value) {
    if (value < 18 || value > 65) {
      throw ArgumentError("Age must be between 18 and 65");
    }
    _age = value;
  }

  void displayInfo() {
    print("Employee: $_name | Age: $_age | Salary: ₹$_salary");
  }
}

void main() {
  Employee emp = Employee("Ravi", 50000, 28);
  emp.displayInfo();

  emp.salary = 60000; // Setter validates
  print("Updated salary: ${emp.salary}");

  // emp._salary = -1; // ❌ Not accessible outside the file
  // emp.salary = 5000; // ❌ Throws ArgumentError
}
```

### 📊 Abstraction vs Encapsulation

| Concept | Focus | How | Example |
|---------|-------|-----|---------|
| **Abstraction** | *What* it does | Abstract classes, interfaces | TV remote buttons |
| **Encapsulation** | *How* it's protected | Private fields, getters/setters | TV internal circuits hidden |

---

## 17. 📋 OOP Brief

### The Four Pillars — Quick Reference

| Pillar | Keyword/Tool | Purpose | Real-World Analogy |
|--------|-------------|---------|-------------------|
| **Encapsulation** | `_` prefix, getters/setters | Protect data | Bank vault |
| **Inheritance** | `extends` | Reuse code | Child inherits traits from parent |
| **Polymorphism** | Method override | Many forms | Same volume button, different devices |
| **Abstraction** | `abstract class` | Hide complexity | Car dashboard (hides engine) |

> 💡 **Rule of Thumb:**
> - Use **encapsulation** always — protect your data.
> - Use **inheritance** for IS-A relationships with shared code.
> - Use **abstraction** to define contracts and APIs.
> - **Polymorphism** happens naturally when you use the above well.

---

## 18. 🧩 Mixins

### 📌 Definition
A mixin is a way to reuse code across multiple class hierarchies without using inheritance. It's like "adding abilities" to a class.

### 📝 Theory
Since Dart supports only single inheritance, mixins solve the problem of sharing functionality across unrelated classes. Use the `mixin` keyword to define them and `with` keyword to use them.

### 🔤 Syntax & Example
```dart
// Define mixins — capabilities to add
mixin Swimmable {
  void swim() => print("$runtimeType is swimming 🏊");
}

mixin Flyable {
  void fly() => print("$runtimeType is flying 🦅");
}

mixin Runnable {
  void run() => print("$runtimeType is running 🏃");
}

// Base class
class Animal {
  String name;
  Animal(this.name);
}

// Mix capabilities into classes
class Duck extends Animal with Swimmable, Flyable, Runnable {
  Duck(super.name);
}

class Eagle extends Animal with Flyable, Runnable {
  Eagle(super.name);
}

class Fish extends Animal with Swimmable {
  Fish(super.name);
}

void main() {
  Duck duck = Duck("Donald");
  duck.swim();  // From Swimmable
  duck.fly();   // From Flyable
  duck.run();   // From Runnable

  Eagle eagle = Eagle("Sam");
  eagle.fly();  // From Flyable
  eagle.run();  // From Runnable
  // eagle.swim(); // ❌ Eagle doesn't have Swimmable

  Fish fish = Fish("Nemo");
  fish.swim();  // Only can swim
}
```

#### Mixin with Restrictions
```dart
// Restrict mixin to specific parent classes
mixin CanCode on Animal {
  void code() => print("$runtimeType is coding! 💻");
}

class SmartDog extends Animal with CanCode {
  SmartDog(super.name);
}

void main() {
  SmartDog sd = SmartDog("Robo");
  sd.code(); // Robo is coding! 💻
}
```

### ⚠️ Important Points
- Mixins cannot have constructors.
- Use `on ClassName` to restrict a mixin to certain class hierarchies.
- The order of `with` matters when methods conflict — last one wins.
- Mixins are Dart's elegant solution to multiple inheritance.

> 💡 **Flutter Use Case:** Flutter uses mixins extensively — e.g., `TickerProviderStateMixin` and `AutomaticKeepAliveClientMixin`.

---

## 19. 🛡️ Class Modifiers

### 📌 Definition
Class modifiers in Dart control how classes can be used, extended, or implemented by other code.

### 📝 Theory
Introduced in Dart 3, class modifiers give library authors fine-grained control over how their classes can be used.

### 📊 Class Modifiers Table

| Modifier | Can Extend | Can Implement | Can Mix In | Can Construct | Use Case |
|----------|-----------|--------------|-----------|--------------|----------|
| `class` | ✅ | ✅ | ❌ | ✅ | Default |
| `abstract` | ✅ | ✅ | ❌ | ❌ | Base with abstract methods |
| `final` | ❌ | ❌ | ❌ | ✅ | Prevent modification |
| `base` | ✅ | ❌ | ❌ | ✅ | Force inheritance |
| `interface` | ❌ | ✅ | ❌ | ✅ | Define contracts |
| `sealed` | ❌ | ❌ | ❌ | ❌ | Known subtypes only |
| `mixin class` | ✅ | ✅ | ✅ | ✅ | Both class and mixin |

### 💡 Example
```dart
// final class — cannot be extended or implemented
final class ImmutablePoint {
  final double x, y;
  const ImmutablePoint(this.x, this.y);

  double distanceTo(ImmutablePoint other) {
    double dx = x - other.x;
    double dy = y - other.y;
    return (dx * dx + dy * dy);
  }
}

// sealed class — known, closed set of subtypes
sealed class PaymentResult {}

class PaymentSuccess extends PaymentResult {
  final String transactionId;
  PaymentSuccess(this.transactionId);
}

class PaymentFailure extends PaymentResult {
  final String error;
  PaymentFailure(this.error);
}

void handlePayment(PaymentResult result) {
  // Exhaustive switch — compiler ensures all cases covered
  switch (result) {
    case PaymentSuccess(transactionId: var id):
      print("✅ Payment successful! ID: $id");
    case PaymentFailure(error: var err):
      print("❌ Payment failed: $err");
  }
}

void main() {
  handlePayment(PaymentSuccess("TXN_12345"));
  handlePayment(PaymentFailure("Card declined"));
}
```

> 💡 **Use `sealed` classes** when you have a known, finite set of subtypes — perfect for state management (like Success/Error/Loading states in Flutter).

---

## 20. 📋 Lists

### 📌 Definition
A List is an ordered collection of items that can be accessed by index. Lists allow duplicate values.

### 📝 Theory
Dart Lists are similar to arrays in other languages but are dynamic by default. They support a rich set of methods for transformation, filtering, and manipulation.

### 🔤 Syntax & Examples
```dart
void main() {
  // Fixed-type list
  List<String> fruits = ["Apple", "Banana", "Cherry"];

  // Dynamic list
  var numbers = [1, 2, 3, 4, 5];

  // Empty list
  List<int> scores = [];

  // Fixed-length list
  List<String> days = List.filled(7, "");

  // Access by index (0-based)
  print(fruits[0]); // Apple
  print(fruits.last); // Cherry

  // Common operations
  fruits.add("Date");               // Add to end
  fruits.insert(1, "Avocado");     // Insert at index 1
  fruits.remove("Banana");          // Remove by value
  fruits.removeAt(0);              // Remove by index

  print(fruits.length);             // Number of elements
  print(fruits.contains("Cherry")); // true
  print(fruits.indexOf("Cherry"));  // Returns index or -1

  // Iteration
  for (String fruit in fruits) {
    print(fruit);
  }

  // Functional operations
  List<int> nums = [1, 2, 3, 4, 5, 6];

  var evens = nums.where((n) => n.isEven).toList();
  var doubled = nums.map((n) => n * 2).toList();
  int total = nums.reduce((a, b) => a + b);

  print(evens);   // [2, 4, 6]
  print(doubled); // [2, 4, 6, 8, 10, 12]
  print(total);   // 21

  // Spread operator
  var list1 = [1, 2, 3];
  var list2 = [4, 5, 6];
  var combined = [...list1, ...list2];
  print(combined); // [1, 2, 3, 4, 5, 6]

  // Sort
  var unsorted = [3, 1, 4, 1, 5, 9];
  unsorted.sort();
  print(unsorted); // [1, 1, 3, 4, 5, 9]
}
```

---

## 21. 🔷 Sets

### 📌 Definition
A Set is an unordered collection of **unique** items — duplicates are automatically rejected.

### 📝 Theory
Sets are useful when uniqueness matters. They provide O(1) average time for lookup operations, making membership checking faster than Lists.

### 🔤 Syntax & Examples
```dart
void main() {
  // Create a Set
  Set<String> colors = {"Red", "Green", "Blue"};

  // Sets automatically remove duplicates
  Set<int> numbers = {1, 2, 3, 2, 1, 4};
  print(numbers); // {1, 2, 3, 4} — duplicates removed

  // Common operations
  colors.add("Yellow");          // Add element
  colors.remove("Red");          // Remove element
  print(colors.contains("Blue")); // true

  // Set operations
  Set<int> a = {1, 2, 3, 4};
  Set<int> b = {3, 4, 5, 6};

  print(a.union(b));        // {1, 2, 3, 4, 5, 6} — all unique elements
  print(a.intersection(b)); // {3, 4}             — common elements
  print(a.difference(b));   // {1, 2}             — in a but not b

  // Convert List to Set (to remove duplicates)
  List<String> withDups = ["a", "b", "a", "c", "b"];
  Set<String> unique = withDups.toSet();
  print(unique); // {a, b, c}

  // Convert back to List
  List<String> uniqueList = unique.toList();
}
```

---

## 22. 🗺️ Maps

### 📌 Definition
A Map is a collection of **key-value pairs**, where each key is unique. Also called a dictionary or hash map in other languages.

### 📝 Theory
Maps are perfect for storing structured data with named fields or looking up values by key. Both keys and values can be of any type.

### 🔤 Syntax & Examples
```dart
void main() {
  // Create a Map
  Map<String, int> studentScores = {
    "Alice": 95,
    "Bob": 82,
    "Charlie": 78,
  };

  // Access by key
  print(studentScores["Alice"]); // 95
  print(studentScores["David"]); // null (key doesn't exist)

  // Safe access with ??
  print(studentScores["David"] ?? 0); // 0

  // Add/Update
  studentScores["David"] = 88; // Add new key
  studentScores["Alice"] = 98; // Update existing key

  // Remove
  studentScores.remove("Bob");

  // Check existence
  print(studentScores.containsKey("Charlie")); // true
  print(studentScores.containsValue(78));       // true

  // Iterate
  studentScores.forEach((name, score) {
    print("$name: $score");
  });

  // Keys and values
  print(studentScores.keys.toList());   // [Alice, Charlie, David]
  print(studentScores.values.toList()); // [98, 78, 88]

  print(studentScores.length); // 3

  // Nested Map — like JSON objects
  Map<String, dynamic> user = {
    "name": "Alice",
    "age": 25,
    "address": {
      "city": "Mumbai",
      "pin": "400001",
    }
  };

  print(user["name"]);                        // Alice
  print((user["address"] as Map)["city"]);    // Mumbai
}
```

### 📊 List vs Set vs Map

| Feature | List | Set | Map |
|---------|------|-----|-----|
| Order | ✅ Ordered | ❌ Unordered | ✅ Insertion order (Dart) |
| Duplicates | ✅ Allowed | ❌ Not allowed | Keys: ❌ / Values: ✅ |
| Access | By index `[0]` | No direct access | By key `["name"]` |
| Use case | Ordered collections | Uniqueness checks | Key-value storage |
| Syntax | `[1, 2, 3]` | `{1, 2, 3}` | `{"key": "value"}` |

---

## 23. 🏷️ Enums

### 📌 Definition
An enum (enumeration) is a special type that represents a fixed set of named constant values.

### 📝 Theory
Enums make code more readable and type-safe by replacing magic strings or numbers with meaningful names. Dart's enhanced enums (Dart 2.17+) can have properties and methods.

### 🔤 Syntax & Examples
```dart
// Basic enum
enum Direction {
  north,
  south,
  east,
  west,
}

// Enhanced enum — with properties and methods
enum Planet {
  mercury(3.7),
  venus(8.87),
  earth(9.81),
  mars(3.72);

  final double gravity; // Property

  const Planet(this.gravity); // Constructor

  // Method on enum
  double weightOn(double earthWeight) {
    return earthWeight * gravity / 9.81;
  }
}

void main() {
  // Basic enum usage
  Direction dir = Direction.north;
  print(dir);           // Direction.north
  print(dir.name);      // north
  print(dir.index);     // 0

  // Switch on enum — exhaustive
  switch (dir) {
    case Direction.north:
      print("Going north! ⬆️");
    case Direction.south:
      print("Going south! ⬇️");
    case Direction.east:
      print("Going east! ➡️");
    case Direction.west:
      print("Going west! ⬅️");
  }

  // Enhanced enum
  Planet earth = Planet.earth;
  print("Earth gravity: ${earth.gravity}"); // 9.81

  double myWeight = 70.0;
  print("Weight on Mars: ${Planet.mars.weightOn(myWeight).toStringAsFixed(1)} kg");

  // All enum values
  for (var planet in Planet.values) {
    print("${planet.name}: ${planet.gravity} m/s²");
  }
}
```

### ⚠️ Important Points
- Enum values are automatically `const`.
- `values` gives all enum options as a List.
- `name` property (Dart 2.15+) gives the enum value as a String.
- Enhanced enums can implement interfaces.

> 💡 **Flutter Use Case:** Enums are perfect for managing state — `enum LoadingState { idle, loading, success, error }`.

---

## 24. ⚠️ Exception Handling

### 📌 Definition
Exception handling is the process of responding to errors (exceptions) that occur during program execution, preventing crashes.

### 📝 Theory
Dart uses `try-catch-finally` blocks. You can catch specific exception types or use a general `catch`. `throw` creates exceptions, and `rethrow` re-throws them up the call stack.

### 🔤 Syntax & Examples
```dart
// Custom Exception class
class InsufficientFundsException implements Exception {
  final double amount;
  final double balance;

  InsufficientFundsException(this.amount, this.balance);

  @override
  String toString() =>
      "Cannot withdraw ₹$amount. Available balance: ₹$balance";
}

class BankAccount {
  double _balance;
  BankAccount(this._balance);

  void withdraw(double amount) {
    if (amount <= 0) {
      throw ArgumentError("Amount must be positive: $amount");
    }
    if (amount > _balance) {
      throw InsufficientFundsException(amount, _balance);
    }
    _balance -= amount;
    print("Withdrew ₹$amount. New balance: ₹$_balance");
  }
}

void main() {
  BankAccount account = BankAccount(1000.0);

  // try-catch-finally
  try {
    account.withdraw(500);   // Works fine
    account.withdraw(800);   // Throws InsufficientFundsException
    account.withdraw(-100);  // Never reached
  } on InsufficientFundsException catch (e) {
    // Catch specific exception
    print("💰 Custom Error: $e");
  } on ArgumentError catch (e) {
    // Catch another specific type
    print("⚠️ Argument Error: ${e.message}");
  } catch (e, stackTrace) {
    // Catch ANY exception
    print("❌ Unexpected error: $e");
    print("Stack trace: $stackTrace");
  } finally {
    // Always runs — cleanup code
    print("✅ Transaction attempt complete.");
  }
}
```

#### Rethrowing Exceptions
```dart
void riskyOperation() {
  try {
    throw FormatException("Invalid data format");
  } catch (e) {
    print("Logging error: $e");
    rethrow; // Re-throw to caller
  }
}
```

### ⚠️ Important Points
- `finally` always executes, even if an exception was thrown or caught.
- Use `on ExceptionType` to catch specific types (preferred).
- `rethrow` preserves the original stack trace.
- Dart exceptions are not checked — you don't have to declare them.

> 💡 **Best Practice:** Create custom exception classes for domain-specific errors. It makes code more readable and catch blocks more precise.

---

## 25. ⏳ Futures

### 📌 Definition
A `Future` represents a value that will be available at some point in the future — the result of an asynchronous operation.

### 📝 Theory
Dart is single-threaded but handles asynchronous operations using an event loop. `Future` is Dart's promise — it represents an eventual value or error. Use `async/await` for readable async code.

### 🔤 Syntax & Examples
```dart
import 'dart:async';

// Simulating an API call
Future<String> fetchUserData(String userId) async {
  print("📡 Fetching data for user: $userId...");

  // Simulates network delay
  await Future.delayed(Duration(seconds: 2));

  if (userId.isEmpty) {
    throw Exception("User ID cannot be empty");
  }

  return "User{id: $userId, name: 'Alice', email: 'alice@example.com'}";
}

// Using async/await
Future<void> displayUser(String userId) async {
  try {
    String userData = await fetchUserData(userId);
    print("✅ Data received: $userData");
  } catch (e) {
    print("❌ Error: $e");
  }
}

// Using .then() / .catchError() (older style)
void fetchWithCallback(String userId) {
  fetchUserData(userId)
      .then((data) => print("Data: $data"))
      .catchError((e) => print("Error: $e"))
      .whenComplete(() => print("Request complete."));
}

// Running multiple futures concurrently
Future<void> parallelFetch() async {
  print("Starting parallel requests...");

  // Runs all simultaneously — faster than awaiting each one
  var results = await Future.wait([
    fetchUserData("U001"),
    fetchUserData("U002"),
    fetchUserData("U003"),
  ]);

  for (var result in results) {
    print(result);
  }
}

void main() async {
  await displayUser("U001");
  await parallelFetch();
}
```

### 📊 Future vs Stream

| Feature | Future | Stream |
|---------|--------|--------|
| Values | Single value | Multiple values |
| Completion | Completes once | Ongoing or completes |
| Keyword | `async/await` | `async*` / `yield` |
| Use case | API call, file read | Real-time data, WebSocket |
| Listen | `await` or `.then()` | `await for` or `.listen()` |

### ⚠️ Important Points
- Mark functions returning `Future` with `async`.
- `await` can only be used inside `async` functions.
- Use `Future.wait()` for parallel operations — much faster than sequential `await`.
- A Future can only complete once (either with a value or an error).

---

## 26. 🌊 Streams

### 📌 Definition
A `Stream` is a sequence of asynchronous events — it delivers multiple values over time, unlike a Future which delivers one.

### 📝 Theory
Streams are like a pipe through which data flows continuously. They're used for real-time data like user input events, network data, file reads, and more.

### 🔤 Syntax & Examples
```dart
import 'dart:async';

// Creating a simple stream with async*
Stream<int> countUp(int max) async* {
  for (int i = 1; i <= max; i++) {
    await Future.delayed(Duration(milliseconds: 500));
    yield i; // yield sends a value to the stream
  }
}

// Stream with transformation
Stream<String> temperatureAlerts() async* {
  List<double> readings = [36.5, 37.0, 38.5, 39.2, 37.8];

  for (double temp in readings) {
    await Future.delayed(Duration(seconds: 1));
    yield temp > 38.0 ? "🔥 HIGH: ${temp}°C" : "✅ Normal: ${temp}°C";
  }
}

void main() async {
  // Consuming a stream with await for
  print("Counting up:");
  await for (int count in countUp(5)) {
    print("  Count: $count");
  }

  // Stream with listen()
  print("\nTemperature monitor:");
  temperatureAlerts().listen(
    (alert) => print("  $alert"),
    onError: (e) => print("Error: $e"),
    onDone: () => print("  Monitoring complete ✅"),
  );

  // StreamController — manual stream control
  StreamController<String> controller = StreamController<String>();

  controller.stream.listen(
    (message) => print("📨 Received: $message"),
    onDone: () => print("Stream closed."),
  );

  controller.sink.add("Hello");
  controller.sink.add("World");
  controller.sink.add("Dart!");
  await controller.close();

  // Stream transformations
  Stream<int> numbers = Stream.fromIterable([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);

  await numbers
      .where((n) => n.isEven)        // Filter: only even numbers
      .map((n) => n * n)             // Transform: square them
      .take(3)                       // Take first 3
      .forEach((n) => print(n));     // Output: 4, 16, 36
}
```

### ⚠️ Important Points
- `yield` in `async*` functions sends values to a stream one at a time.
- `broadcast` streams allow multiple listeners; regular streams are single-subscriber.
- Always close `StreamController` when done to avoid memory leaks.
- Use `StreamTransformer` for complex stream transformations.

> 💡 **Flutter Use Case:** Flutter's `StreamBuilder` widget rebuilds UI whenever a stream emits a new value — essential for real-time apps.

---

## 27. 📦 Creating Records

### 📌 Definition
Records (introduced in Dart 3) are anonymous, immutable, structured value types that can bundle multiple values together without defining a full class.

### 📝 Theory
Records are like lightweight data containers — perfect when you need to return multiple values from a function or group related data without creating a whole class.

### 🔤 Syntax & Examples
```dart
void main() {
  // Positional record
  (String, int) person = ("Alice", 25);
  print(person.$1); // Alice (1-indexed)
  print(person.$2); // 25

  // Named record fields
  ({String name, int age, String city}) user = (
    name: "Bob",
    age: 30,
    city: "Mumbai",
  );

  print(user.name); // Bob
  print(user.age);  // 30
  print(user.city); // Mumbai

  // Records as function return type — return multiple values!
  (double lat, double lng) getCoordinates(String place) {
    // Simulated data
    return (19.0760, 72.8777); // Mumbai coordinates
  }

  var coords = getCoordinates("Mumbai");
  print("Lat: ${coords.lat}, Lng: ${coords.lng}");

  // Records are value types — equality by value
  var r1 = (1, 2);
  var r2 = (1, 2);
  print(r1 == r2); // true! (unlike class instances)

  // Mixed named and positional
  (int, {String name}) mixed = (42, name: "Answer");
  print(mixed.$1);    // 42
  print(mixed.name);  // Answer

  // Destructuring a record
  var (name, age) = ("Charlie", 28);
  print("$name is $age years old");
}
```

### ⚠️ Important Points
- Records are immutable — their fields cannot be changed after creation.
- Records support structural equality — two records with same types and values are equal.
- Positional fields accessed via `$1`, `$2`, etc.; named fields via `.fieldName`.
- Records eliminate the need for simple data classes.

> 💡 **Best Practice:** Use records when returning 2-3 related values from a function. For larger structures or when you need methods, use a class.

---

## 28. 🎯 Patterns & Pattern Matching

### 📌 Definition
Patterns are a structural template that values are matched against, allowing you to destructure data, check types, and extract values in one step (Dart 3+).

### 📝 Theory
Pattern matching in Dart brings powerful data decomposition. It works in `switch` statements/expressions, `if-case`, variable declarations, and more.

### 🔤 Syntax & Examples
```dart
void main() {
  // 1. Switch Expression with Patterns
  Object shape = ("circle", 5.0);

  String description = switch (shape) {
    ("circle", double r) => "Circle with radius $r",
    ("rectangle", double w, double h) => "Rectangle ${w}x$h",
    _ => "Unknown shape",
  };
  print(description); // Circle with radius 5.0

  // 2. Type Patterns
  Object value = 42;
  switch (value) {
    case int n when n > 0:
      print("Positive integer: $n");
    case int n when n < 0:
      print("Negative integer: $n");
    case String s:
      print("String: $s");
    default:
      print("Other type");
  }

  // 3. List Patterns — destructure lists
  List<int> numbers = [1, 2, 3];
  var [first, second, ...rest] = numbers;
  print("First: $first, Second: $second"); // 1, 2

  // 4. Map Patterns
  Map<String, dynamic> user = {"name": "Alice", "age": 25};
  if (user case {"name": String name, "age": int age}) {
    print("$name is $age years old");
  }

  // 5. Record Patterns
  (String, int) record = ("Dart", 3);
  var (language, version) = record;
  print("$language version $version"); // Dart version 3

  // 6. if-case Pattern
  Object response = {"status": "success", "data": [1, 2, 3]};
  if (response case {"status": "success", "data": List data}) {
    print("Success! Got ${data.length} items");
  }

  // 7. Sealed class + exhaustive switch (best combo!)
  sealed class ApiResponse {}
  class Success extends ApiResponse { final String data; Success(this.data); }
  class Error extends ApiResponse { final String message; Error(this.message); }
  class Loading extends ApiResponse {}

  ApiResponse state = Success("User data loaded");

  String ui = switch (state) {
    Success(data: var d) => "✅ Show: $d",
    Error(message: var m) => "❌ Error: $m",
    Loading() => "⏳ Loading...",
  };
  print(ui);
}
```

### ⚠️ Important Points
- Patterns work in switch, if-case, for-in, and variable declarations.
- `when` adds guards to pattern matches (like a filter condition).
- Sealed classes + switch expressions give **exhaustiveness checking** — the compiler warns if you miss a case.
- `...rest` in list patterns captures remaining elements.

---

## 29. 🔧 Extensions

### 📌 Definition
Extensions allow you to add new methods to existing classes — even built-in types like `String`, `int`, `List` — **without** modifying the original class or creating a subclass.

### 📝 Theory
Extensions solve the problem of wanting to add utility methods to types you don't own (like `String` or `DateTime`). They're syntactic sugar — the methods feel native but are defined elsewhere.

### 🔤 Syntax & Examples
```dart
// Extending String
extension StringExtensions on String {
  // Capitalize first letter
  String get capitalized =>
      isEmpty ? this : '${this[0].toUpperCase()}${substring(1)}';

  // Check if valid email (simple check)
  bool get isValidEmail => contains('@') && contains('.');

  // Repeat a string
  String repeat(int times) => this * times;

  // Convert to title case
  String get titleCase =>
      split(' ').map((word) => word.capitalized).join(' ');
}

// Extending int
extension IntExtensions on int {
  bool get isEven => this % 2 == 0;
  bool get isPrime {
    if (this < 2) return false;
    for (int i = 2; i <= this ~/ 2; i++) {
      if (this % i == 0) return false;
    }
    return true;
  }

  // Convert seconds to formatted time string
  String get toTimeString {
    int mins = this ~/ 60;
    int secs = this % 60;
    return "${mins}m ${secs}s";
  }
}

// Extending List
extension ListExtensions<T> on List<T> {
  // Safe first element access (no RangeError)
  T? get firstOrNull => isEmpty ? null : first;

  // Chunk list into groups
  List<List<T>> chunk(int size) {
    List<List<T>> chunks = [];
    for (int i = 0; i < length; i += size) {
      chunks.add(sublist(i, (i + size).clamp(0, length)));
    }
    return chunks;
  }
}

// Extension on DateTime
extension DateTimeExtensions on DateTime {
  bool get isToday {
    final now = DateTime.now();
    return year == now.year && month == now.month && day == now.day;
  }

  String get formatted => "$day/$month/$year";
}

void main() {
  // String extensions
  print("hello world".titleCase);     // Hello World
  print("dart".repeat(3));            // dartdartdart
  print("test@email.com".isValidEmail); // true

  // Int extensions
  print(7.isPrime);           // true
  print(125.toTimeString);   // 2m 5s

  // List extensions
  List<int> nums = [1, 2, 3, 4, 5, 6, 7];
  print(nums.firstOrNull);   // 1
  print(nums.chunk(3));      // [[1,2,3],[4,5,6],[7]]

  // DateTime extension
  print(DateTime.now().formatted);
  print(DateTime.now().isToday); // true
}
```

### ⚠️ Important Points
- Extensions cannot add fields/properties (only methods and getters/setters).
- Extension methods can be hidden or shown using `import ... hide/show`.
- If two extensions define the same method, you must specify which one to use explicitly.
- Extensions are purely static — they don't change the original class.

> 💡 **Best Practice:** Group related extensions in a dedicated file (e.g., `string_extensions.dart`) and import them where needed. This keeps code organized and reusable.

---

## 30. 🏁 Conclusion & Resources

### 🎉 Congratulations!

You've completed the Dart programming journey from basics to advanced! Here's what you've mastered:

✅ Basic syntax — print, variables, operators, comments
✅ Control flow — if/else, switch, loops
✅ Functions — named params, arrow functions, closures
✅ OOP — classes, inheritance, polymorphism, encapsulation, abstraction
✅ Advanced OOP — mixins, class modifiers, implements vs extends
✅ Collections — Lists, Sets, Maps
✅ Modern Dart — Enums, Records, Patterns
✅ Asynchronous — Futures, Streams
✅ Exception Handling
✅ Extensions

---

### 🗺️ What's Next?

Now that you know Dart, the natural path forward is:

1. **Flutter** — Build beautiful cross-platform apps with your Dart knowledge
2. **Dart on the server** — Use [Dart Frog](https://dartfrog.vgv.dev/) or [Shelf](https://pub.dev/packages/shelf) for backend
3. **State Management** — Learn Riverpod, BLoC, or Provider for Flutter
4. **Testing** — Write unit and widget tests in Dart

---

### 📚 Recommended Resources

#### Official Documentation
- 🌐 [Dart Official Documentation](https://dart.dev/guides) — The definitive reference
- 🌐 [Dart Language Tour](https://dart.dev/language) — Comprehensive language overview
- 🌐 [Dart API Reference](https://api.dart.dev/) — Complete API docs
- 🌐 [DartPad](https://dartpad.dev/) — Online Dart playground (try code instantly!)

#### Flutter Resources
- 🌐 [Flutter Official Documentation](https://flutter.dev/docs) — Everything Flutter
- 🌐 [Flutter Codelabs](https://flutter.dev/docs/codelabs) — Hands-on tutorials
- 🌐 [pub.dev](https://pub.dev/) — Dart/Flutter package repository
- 🌐 [Flutter Widget Catalog](https://flutter.dev/docs/development/ui/widgets) — All Flutter widgets

#### Learning Platforms
- 🌐 [Dart Apprentice Book](https://www.kodeco.com/books/dart-apprentice) — Excellent beginner book
- 🌐 [Flutter & Dart — The Complete Guide (Udemy)](https://www.udemy.com/course/learn-flutter-dart-to-build-ios-android-apps/) — Comprehensive video course
- 🌐 [Official Flutter YouTube Channel](https://www.youtube.com/@flutterdev) — Free tutorials from the team

#### Community
- 💬 [Flutter Community Slack](https://fluttercommunity.dev/) — Connect with developers
- 💬 [r/FlutterDev](https://www.reddit.com/r/FlutterDev/) — Active community
- 💬 [Flutter Discord](https://discord.gg/flutter) — Real-time help

---

### 💡 Final Tips for Your Dart Journey

1. **Practice daily** — Even 30 minutes of coding makes a huge difference.
2. **Build projects** — Don't just read; apply concepts in real apps.
3. **Read others' code** — Browse open-source Flutter projects on GitHub.
4. **Use DartPad** — Experiment without any setup at [dartpad.dev](https://dartpad.dev/).
5. **Embrace null safety** — It's Dart's superpower; don't fight it.

---

*Happy Coding! 🚀 The best Dart developer is the one who keeps building.*

---

> 📝 **Maintained by:** Community Contributors
> 📅 **Last Updated:** 2024
> 🎯 **Dart Version:** 3.x
> 📄 **License:** MIT
