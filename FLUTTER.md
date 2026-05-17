# 🐦 Flutter: The Complete Handbook
### From Basics to Advanced — A Beginner-Friendly Guide

> *"Flutter — Build beautiful apps for any screen."* — Flutter Official Docs

![Flutter](https://img.shields.io/badge/Flutter-3.x-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-3.x-0175C2?style=for-the-badge&logo=dart&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Beginner%20to%20Advanced-orange?style=for-the-badge)

---

## 🤔 What is Flutter?

**Flutter** is an open-source UI toolkit developed by **Google** for building natively compiled, beautiful, and high-performance applications for **mobile, web, desktop, and embedded** platforms — all from a **single codebase**.

Flutter uses the **Dart** programming language and renders UI using its own high-performance **Skia/Impeller** rendering engine, which means Flutter controls every pixel on the screen — no web views, no platform bridges for UI.

In simple words: **Flutter = One Codebase → Runs Everywhere**

---

## 🚀 Why Use Flutter?

| Feature | Benefit |
|---|---|
| **Single Codebase** | Write once, deploy on iOS, Android, Web, Windows, macOS, Linux |
| **Hot Reload** | See changes instantly without restarting the app |
| **Beautiful UI** | Pixel-perfect custom designs on all platforms |
| **High Performance** | Compiled to native ARM code, runs at 60/120 fps |
| **Rich Ecosystem** | Thousands of packages on pub.dev |
| **Google Backed** | Strong community, regular updates |

---

## ⚡ Flutter vs React Native vs Native Development

| Feature | Flutter | React Native | Native (Android/iOS) |
|---|---|---|---|
| Language | Dart | JavaScript | Kotlin/Swift |
| Performance | Excellent (own renderer) | Good (JS bridge) | Best |
| Code Sharing | ~95% | ~80% | 0% |
| UI Rendering | Custom engine | Native components | Native |
| Hot Reload | ✅ | ✅ | ❌ |
| Learning Curve | Moderate | Low (if JS known) | High |
| Community | Large & growing | Very large | Platform-specific |

---

## 📚 Table of Contents

1. [Flutter Basics](#1-flutter-basics)
   - [Installation & Setup](#installation--setup)
   - [Flutter Project Structure](#flutter-project-structure)
   - [pubspec.yaml](#pubspecyaml)
   - [Running Flutter Apps](#running-flutter-apps)
2. [Dart Fundamentals](#2-dart-fundamentals)
   - [Variables & Data Types](#variables--data-types)
   - [Control Flow](#control-flow)
   - [Functions](#functions)
   - [Classes & OOP](#classes--oop)
   - [Null Safety](#null-safety)
   - [Async/Await & Futures](#asyncawait--futures)
3. [Flutter Widgets](#3-flutter-widgets)
   - [What are Widgets?](#what-are-widgets)
   - [StatelessWidget](#statelesswidget)
   - [StatefulWidget](#statefulwidget)
   - [Widget Lifecycle](#widget-lifecycle)
4. [Layout Widgets](#4-layout-widgets)
   - [Container](#container)
   - [Row & Column](#row--column)
   - [Stack](#stack)
   - [Expanded & Flexible](#expanded--flexible)
   - [ListView & GridView](#listview--gridview)
   - [Padding, Margin, Align](#padding-margin-align)
5. [UI Widgets](#5-ui-widgets)
   - [Text & RichText](#text--richtext)
   - [Image](#image)
   - [Icon & IconButton](#icon--iconbutton)
   - [Buttons](#buttons)
   - [TextField & Form](#textfield--form)
   - [Card & ListTile](#card--listtile)
   - [AppBar & Scaffold](#appbar--scaffold)
6. [Navigation & Routing](#6-navigation--routing)
   - [Navigator](#navigator)
   - [Named Routes](#named-routes)
   - [GoRouter](#gorouter)
   - [Passing Data Between Screens](#passing-data-between-screens)
7. [State Management](#7-state-management)
   - [setState](#setstate)
   - [InheritedWidget & Provider](#inheritedwidget--provider)
   - [Riverpod](#riverpod)
   - [BLoC Pattern](#bloc-pattern)
   - [GetX](#getx)
8. [Networking & API](#8-networking--api)
   - [http Package](#http-package)
   - [Dio](#dio)
   - [JSON Parsing](#json-parsing)
   - [FutureBuilder & StreamBuilder](#futurebuilder--streambuilder)
9. [Local Storage](#9-local-storage)
   - [SharedPreferences](#sharedpreferences)
   - [SQLite (sqflite)](#sqlite-sqflite)
   - [Hive](#hive)
10. [Firebase Integration](#10-firebase-integration)
    - [Firebase Setup](#firebase-setup)
    - [Authentication](#authentication)
    - [Firestore](#firestore)
    - [Firebase Storage](#firebase-storage)
11. [Animations](#11-animations)
    - [Implicit Animations](#implicit-animations)
    - [Explicit Animations](#explicit-animations)
    - [Hero Animations](#hero-animations)
    - [Lottie Animations](#lottie-animations)
12. [Advanced Flutter](#12-advanced-flutter)
    - [Custom Painter](#custom-painter)
    - [Platform Channels](#platform-channels)
    - [Isolates & Compute](#isolates--compute)
    - [Streams](#streams)
13. [Testing](#13-testing)
    - [Unit Tests](#unit-tests)
    - [Widget Tests](#widget-tests)
    - [Integration Tests](#integration-tests)
14. [Deployment](#14-deployment)
15. [Best Practices](#15-best-practices)
16. [Exercises & Challenges](#16-exercises--challenges)
17. [Conclusion & Resources](#17-conclusion--resources)

---

# 1. Flutter Basics

## Installation & Setup

### Step 1: Download Flutter SDK

```bash
# macOS
brew install --cask flutter

# Or download manually from https://flutter.dev/docs/get-started/install
# Then add to PATH:
export PATH="$PATH:/path/to/flutter/bin"
```

### Step 2: Verify Installation

```bash
flutter doctor
# This checks for all required dependencies and shows what's missing
```

### Step 3: Install Required Tools

```bash
# Android Studio (for Android)
# Xcode (for iOS — macOS only)
# VS Code with Flutter & Dart extensions

# Accept Android licenses
flutter doctor --android-licenses
```

### Step 4: Create Your First App

```bash
# Create new project
flutter create my_first_app

# Navigate into project
cd my_first_app

# Run on connected device / emulator
flutter run

# Run on specific platform
flutter run -d chrome      # Web
flutter run -d windows     # Windows
flutter run -d emulator-5554  # Android emulator
```

---

## Flutter Project Structure

```
my_flutter_app/
├── android/           # Android-specific code & config
├── ios/               # iOS-specific code & config
├── lib/               # Your Dart/Flutter code lives here ✨
│   ├── main.dart      # Entry point of the app
│   ├── screens/       # Full screen widgets
│   ├── widgets/       # Reusable custom widgets
│   ├── models/        # Data models (classes)
│   ├── services/      # API calls, business logic
│   ├── providers/     # State management
│   └── utils/         # Helper functions & constants
├── test/              # Test files
├── assets/            # Images, fonts, JSON files
│   ├── images/
│   └── fonts/
├── pubspec.yaml       # Project config & dependencies
└── pubspec.lock       # Locked dependency versions
```

> 💡 **Best Practice:** Always keep your `lib/` folder organized. Don't put everything in `main.dart`!

---

## pubspec.yaml

`pubspec.yaml` is the project configuration file — like `package.json` in Node.js.

```yaml
name: my_flutter_app
description: A Flutter application

# Version: major.minor.patch+buildNumber
version: 1.0.0+1

environment:
  sdk: '>=3.0.0 <4.0.0'

dependencies:
  flutter:
    sdk: flutter

  # Third-party packages from pub.dev
  http: ^1.1.0
  provider: ^6.1.1
  shared_preferences: ^2.2.2
  go_router: ^12.0.0
  cached_network_image: ^3.3.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0

flutter:
  uses-material-design: true

  # Register assets
  assets:
    - assets/images/
    - assets/data/config.json

  # Register custom fonts
  fonts:
    - family: Poppins
      fonts:
        - asset: assets/fonts/Poppins-Regular.ttf
        - asset: assets/fonts/Poppins-Bold.ttf
          weight: 700
```

```bash
# After editing pubspec.yaml, run:
flutter pub get

# Upgrade packages
flutter pub upgrade
```

---

## Running Flutter Apps

```bash
# List available devices
flutter devices

# Run in debug mode
flutter run

# Run in release mode (optimized, no debug info)
flutter run --release

# Run in profile mode (performance testing)
flutter run --profile

# Build APK
flutter build apk

# Build App Bundle (for Play Store)
flutter build appbundle

# Build iOS IPA
flutter build ios

# Build for web
flutter build web

# Hot reload (during run): press 'r'
# Hot restart:            press 'R'
# Quit:                   press 'q'
```

---

# 2. Dart Fundamentals

Dart is the programming language used by Flutter. It's easy to learn, especially if you know JavaScript or Java.

## Variables & Data Types

```dart
// ── Variable Declaration ──
var name = 'Rohit';        // Type inferred as String
String city = 'Nagpur';   // Explicit type
int age = 25;
double height = 5.11;
bool isActive = true;

// final — set once, cannot be changed
final String appName = 'MyApp';
// appName = 'Other'; // ❌ Error

// const — compile-time constant
const double PI = 3.14159;

// late — declare now, assign later (must assign before use)
late String token;
token = fetchToken(); // Must be assigned before reading

// ── Data Types ──
// String
String greeting = 'Hello, Flutter!';
String multiLine = '''
  This is
  a multi-line
  string
''';
String interpolated = 'My name is $name and I live in $city';
String expression = 'Age next year: ${age + 1}';

// Numbers
int count = 42;
double price = 99.99;
num flexible = 3;       // Can be int or double
flexible = 3.5;         // Still valid

// List (Array)
List<String> fruits = ['Apple', 'Mango', 'Banana'];
var numbers = <int>[1, 2, 3, 4, 5];

// Map (Dictionary)
Map<String, dynamic> user = {
  'name': 'Rohit',
  'age': 25,
  'isActive': true,
};

// Set (unique values)
Set<String> tags = {'flutter', 'dart', 'mobile'};

// Dynamic (avoid when possible)
dynamic anything = 'hello';
anything = 42; // OK but not type-safe
```

---

## Control Flow

```dart
// ── if/else ──
int score = 85;

if (score >= 90) {
  print('Grade: A');
} else if (score >= 80) {
  print('Grade: B');
} else {
  print('Grade: C');
}

// Ternary
String result = score >= 60 ? 'Pass ✅' : 'Fail ❌';

// ── for loops ──
for (int i = 0; i < 5; i++) {
  print('Count: $i');
}

// for-in (iterate collections)
for (String fruit in fruits) {
  print(fruit);
}

// forEach
fruits.forEach((fruit) => print(fruit));

// while
int x = 0;
while (x < 3) {
  print(x);
  x++;
}

// ── switch ──
String day = 'Mon';

switch (day) {
  case 'Sat':
  case 'Sun':
    print('Weekend 🎉');
    break;
  default:
    print('Weekday 💼');
}

// ── Null checks ──
String? nullableName;   // '?' makes it nullable

// Null-aware operators
print(nullableName ?? 'Guest');          // 'Guest' if null
print(nullableName?.toUpperCase());      // null if nullableName is null
nullableName ??= 'Default';             // assign only if null
```

---

## Functions

```dart
// ── Basic Function ──
int add(int a, int b) {
  return a + b;
}

// Arrow function (single expression)
int multiply(int a, int b) => a * b;

// void function
void printGreeting(String name) {
  print('Hello, $name!');
}

// ── Optional Parameters ──

// Optional positional parameters (use [])
String greet(String name, [String greeting = 'Hello']) {
  return '$greeting, $name!';
}
greet('Rohit');              // 'Hello, Rohit!'
greet('Rohit', 'Namaste');   // 'Namaste, Rohit!'

// Named parameters (use {}) — order-independent
void createUser({
  required String name,    // required named parameter
  int age = 0,             // optional with default
  String? email,           // optional nullable
}) {
  print('Creating user: $name, age: $age');
}

createUser(name: 'Rohit', age: 25);
createUser(name: 'Priya', email: 'priya@dev.com');

// ── Higher-Order Functions ──
List<int> numbers = [1, 2, 3, 4, 5, 6];

var evens = numbers.where((n) => n % 2 == 0).toList();     // [2, 4, 6]
var doubled = numbers.map((n) => n * 2).toList();           // [2, 4, 6, 8, 10, 12]
var sum = numbers.reduce((total, n) => total + n);          // 21
var any = numbers.any((n) => n > 4);                        // true
var all = numbers.every((n) => n > 0);                      // true

// ── Anonymous Functions / Lambdas ──
var square = (int n) => n * n;
print(square(5)); // 25

// ── Typedef (function type alias) ──
typedef MathOp = int Function(int, int);
MathOp addOp = (a, b) => a + b;
```

---

## Classes & OOP

```dart
// ── Basic Class ──
class Person {
  String name;
  int age;
  String? email; // nullable

  // Constructor
  Person(this.name, this.age); // shorthand constructor

  // Named constructor
  Person.guest() : name = 'Guest', age = 0;

  // Factory constructor
  factory Person.fromJson(Map<String, dynamic> json) {
    return Person(json['name'], json['age']);
  }

  // Methods
  String introduce() => 'Hi, I\'m $name, $age years old.';

  @override
  String toString() => 'Person(name: $name, age: $age)';
}

final person = Person('Rohit', 25);
final guest = Person.guest();
final fromJson = Person.fromJson({'name': 'Amit', 'age': 30});

// ── Inheritance ──
class Employee extends Person {
  String department;
  double salary;

  Employee(String name, int age, this.department, this.salary)
      : super(name, age); // call parent constructor

  @override
  String introduce() => '${super.introduce()} I work in $department.';
}

// ── Abstract Class ──
abstract class Shape {
  double getArea(); // abstract method

  String describe() => 'This shape has area: ${getArea().toStringAsFixed(2)}';
}

class Circle extends Shape {
  double radius;
  Circle(this.radius);

  @override
  double getArea() => 3.14159 * radius * radius;
}

// ── Mixins (multiple behavior) ──
mixin Flyable {
  void fly() => print('$runtimeType is flying! ✈️');
}

mixin Swimmable {
  void swim() => print('$runtimeType is swimming! 🏊');
}

class Duck extends Animal with Flyable, Swimmable {
  Duck(String name) : super(name);
}

// ── Interface (every class is an interface in Dart) ──
abstract class Printable {
  void printInfo();
}

class Invoice implements Printable {
  @override
  void printInfo() => print('Invoice details...');
}

// ── Getters & Setters ──
class Circle2 {
  double _radius; // private with underscore

  Circle2(this._radius);

  double get radius => _radius;
  double get area => 3.14159 * _radius * _radius;

  set radius(double value) {
    if (value < 0) throw ArgumentError('Radius cannot be negative');
    _radius = value;
  }
}
```

---

## Null Safety

Dart has **sound null safety** — variables cannot be null unless explicitly declared nullable.

```dart
// Non-nullable (default) — cannot be null
String name = 'Rohit';
// name = null; // ❌ Compile error

// Nullable — can be null (add '?')
String? nickname;
print(nickname); // null

// Null check before use
if (nickname != null) {
  print(nickname.toUpperCase()); // Safe
}

// Safe navigation operator (?.)
print(nickname?.length);    // null if nickname is null

// Null coalescing (??)
String display = nickname ?? 'No nickname';

// Null assertion (!) — tell Dart "I know this isn't null"
String definitelyNotNull = nickname!; // Will throw if actually null

// late variables
late String configValue;
void init() {
  configValue = 'loaded'; // assign before use
}

// Required in constructors
class User {
  final String name;
  final String? bio; // optional

  User({required this.name, this.bio});
}

final user = User(name: 'Rohit'); // bio is optional
```

---

## Async/Await & Futures

```dart
import 'dart:async';

// ── Future (like Promise in JS) ──
Future<String> fetchUserName(int id) async {
  // Simulate network delay
  await Future.delayed(Duration(seconds: 2));

  if (id > 0) return 'Rohit';
  throw Exception('User not found');
}

// ── Using async/await ──
void loadUser() async {
  try {
    String name = await fetchUserName(1);
    print('User: $name');
  } catch (e) {
    print('Error: $e');
  } finally {
    print('Done');
  }
}

// ── Future.wait (run parallel) ──
Future<void> loadAll() async {
  final results = await Future.wait([
    fetchUserName(1),
    fetchUserName(2),
    fetchUserName(3),
  ]);
  print(results); // ['Rohit', 'Rohit', 'Rohit']
}

// ── Streams (sequence of async events) ──
Stream<int> countDown(int from) async* {
  for (int i = from; i >= 0; i--) {
    await Future.delayed(Duration(seconds: 1));
    yield i; // emit value
  }
}

// Listen to stream
void startCountdown() {
  countDown(5).listen(
    (value) => print('$value...'),
    onDone: () => print('🚀 Blast off!'),
    onError: (e) => print('Error: $e'),
  );
}

// StreamController (manual stream)
StreamController<String> _controller = StreamController<String>();
Stream<String> get messages => _controller.stream;
void addMessage(String msg) => _controller.add(msg);
void dispose() => _controller.close();
```

---

# 3. Flutter Widgets

## What are Widgets?

In Flutter, **everything is a widget** — text, buttons, padding, layout, animations, even the app itself. Widgets describe what their view should look like given their current configuration and state.

```
App
└── MaterialApp
    └── Scaffold
        ├── AppBar
        │   └── Text ("My App")
        └── Body
            └── Column
                ├── Text ("Hello!")
                └── ElevatedButton ("Click Me")
```

There are two types of widgets:
- **StatelessWidget** — immutable, no internal state
- **StatefulWidget** — mutable, can rebuild when state changes

---

## StatelessWidget

Use `StatelessWidget` when your UI **doesn't change** after it's built.

```dart
import 'package:flutter/material.dart';

// Basic StatelessWidget
class WelcomeCard extends StatelessWidget {
  final String name;
  final String subtitle;

  // Constructor with named parameters
  const WelcomeCard({
    super.key,
    required this.name,
    this.subtitle = 'Welcome to Flutter!',
  });

  @override
  Widget build(BuildContext context) {
    return Card(
      elevation: 4,
      margin: const EdgeInsets.all(16),
      child: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              'Hello, $name! 👋',
              style: const TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
              ),
            ),
            const SizedBox(height: 8),
            Text(
              subtitle,
              style: TextStyle(
                fontSize: 16,
                color: Colors.grey[600],
              ),
            ),
          ],
        ),
      ),
    );
  }
}

// Using the widget
class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Home')),
      body: const WelcomeCard(name: 'Rohit'),
    );
  }
}
```

---

## StatefulWidget

Use `StatefulWidget` when your UI **needs to change** in response to user interaction or data.

```dart
class CounterWidget extends StatefulWidget {
  final String title;

  const CounterWidget({super.key, required this.title});

  @override
  State<CounterWidget> createState() => _CounterWidgetState();
}

class _CounterWidgetState extends State<CounterWidget> {
  int _count = 0;        // State variable
  bool _isLoading = false;

  // Called when state is initialized
  @override
  void initState() {
    super.initState();
    print('Widget created');
    // Fetch initial data here
  }

  // Called when widget is rebuilt with new props
  @override
  void didUpdateWidget(CounterWidget oldWidget) {
    super.didUpdateWidget(oldWidget);
    if (oldWidget.title != widget.title) {
      print('Title changed!');
    }
  }

  // Called when widget is removed from tree
  @override
  void dispose() {
    print('Widget destroyed');
    // Cancel subscriptions, controllers here
    super.dispose();
  }

  void _increment() {
    setState(() {         // Tell Flutter to rebuild
      _count++;
    });
  }

  void _decrement() {
    setState(() {
      if (_count > 0) _count--;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Text(
          widget.title, // access widget props via widget.xxx
          style: Theme.of(context).textTheme.headlineMedium,
        ),
        const SizedBox(height: 16),
        Text(
          '$_count',
          style: const TextStyle(fontSize: 72, fontWeight: FontWeight.bold),
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            FloatingActionButton(
              onPressed: _decrement,
              child: const Icon(Icons.remove),
            ),
            const SizedBox(width: 20),
            FloatingActionButton(
              onPressed: _increment,
              child: const Icon(Icons.add),
            ),
          ],
        ),
      ],
    );
  }
}
```

---

## Widget Lifecycle

```
StatefulWidget Lifecycle:
────────────────────────────────────────
createState()           → Create State object
     │
     ▼
initState()             → Called once when inserted into tree
     │                    (initialize data, subscribe to streams)
     ▼
didChangeDependencies() → Called when InheritedWidget changes
     │
     ▼
build()                 → Builds the widget tree (called many times)
     │
     ▼
didUpdateWidget()       → Called when parent rebuilds with new config
     │
     ▼
setState()              → Triggers rebuild
     │
     ▼
build()                 → Rebuilds widget
     │
     ▼
deactivate()            → Called when removed from tree temporarily
     │
     ▼
dispose()               → Called when permanently removed
                          (cancel streams, controllers, timers)
```

---

# 4. Layout Widgets

## Container

`Container` is one of the most versatile widgets — it combines painting, positioning, and sizing.

```dart
Container(
  width: 200,
  height: 150,
  margin: const EdgeInsets.all(16),           // space outside
  padding: const EdgeInsets.symmetric(        // space inside
    horizontal: 20,
    vertical: 10,
  ),
  decoration: BoxDecoration(
    color: Colors.blue,
    borderRadius: BorderRadius.circular(12),  // rounded corners
    boxShadow: [
      BoxShadow(
        color: Colors.black26,
        blurRadius: 8,
        offset: Offset(0, 4),
      ),
    ],
    gradient: LinearGradient(
      colors: [Colors.blue, Colors.purple],
      begin: Alignment.topLeft,
      end: Alignment.bottomRight,
    ),
  ),
  child: const Text(
    'Hello Flutter!',
    style: TextStyle(color: Colors.white, fontSize: 18),
  ),
)
```

---

## Row & Column

```dart
// Row — horizontal layout
Row(
  mainAxisAlignment: MainAxisAlignment.spaceBetween, // horizontal alignment
  crossAxisAlignment: CrossAxisAlignment.center,     // vertical alignment
  children: [
    Icon(Icons.star, color: Colors.yellow),
    Text('4.8 Rating'),
    ElevatedButton(onPressed: () {}, child: Text('Rate Now')),
  ],
)

// Column — vertical layout
Column(
  mainAxisAlignment: MainAxisAlignment.center,    // vertical alignment
  crossAxisAlignment: CrossAxisAlignment.stretch, // horizontal alignment
  children: [
    Text('Title', style: TextStyle(fontSize: 24)),
    SizedBox(height: 8),  // spacer
    Text('Subtitle'),
    SizedBox(height: 16),
    ElevatedButton(
      onPressed: () {},
      child: Text('Get Started'),
    ),
  ],
)

// MainAxisAlignment options:
// start | end | center | spaceBetween | spaceAround | spaceEvenly

// CrossAxisAlignment options:
// start | end | center | stretch | baseline
```

---

## Stack

`Stack` overlays widgets on top of each other.

```dart
Stack(
  alignment: Alignment.center,
  children: [
    // Bottom layer — background image
    ClipRRect(
      borderRadius: BorderRadius.circular(16),
      child: Image.network(
        'https://example.com/banner.jpg',
        width: 300,
        height: 200,
        fit: BoxFit.cover,
      ),
    ),
    // Middle layer — semi-transparent overlay
    Container(
      width: 300,
      height: 200,
      decoration: BoxDecoration(
        borderRadius: BorderRadius.circular(16),
        color: Colors.black45,
      ),
    ),
    // Top layer — text
    const Text(
      'Featured Product',
      style: TextStyle(
        color: Colors.white,
        fontSize: 22,
        fontWeight: FontWeight.bold,
      ),
    ),
    // Positioned widget — place anywhere in stack
    Positioned(
      top: 8,
      right: 8,
      child: Icon(Icons.favorite, color: Colors.red),
    ),
  ],
)
```

---

## Expanded & Flexible

```dart
Row(
  children: [
    // Expanded — takes all available space
    Expanded(
      flex: 2,  // takes 2/3 of available space
      child: Container(color: Colors.red, height: 50),
    ),
    Expanded(
      flex: 1,  // takes 1/3 of available space
      child: Container(color: Colors.blue, height: 50),
    ),
  ],
)

// Flexible — takes space but can be smaller if child is smaller
Row(
  children: [
    Flexible(
      child: Text('This text wraps if too long instead of overflowing'),
    ),
    Icon(Icons.info),
  ],
)
```

---

## ListView & GridView

```dart
// ListView — scrollable list
ListView(
  children: [
    ListTile(title: Text('Item 1')),
    ListTile(title: Text('Item 2')),
    ListTile(title: Text('Item 3')),
  ],
)

// ListView.builder — efficient for large lists (lazy loading)
ListView.builder(
  itemCount: 100,
  itemBuilder: (context, index) {
    return Card(
      margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 4),
      child: ListTile(
        leading: CircleAvatar(child: Text('${index + 1}')),
        title: Text('Item ${index + 1}'),
        subtitle: Text('Subtitle for item ${index + 1}'),
        trailing: Icon(Icons.arrow_forward_ios),
        onTap: () => print('Tapped item $index'),
      ),
    );
  },
)

// ListView.separated — with dividers
ListView.separated(
  itemCount: items.length,
  separatorBuilder: (context, index) => const Divider(),
  itemBuilder: (context, index) => ListTile(title: Text(items[index])),
)

// GridView.builder
GridView.builder(
  gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
    crossAxisCount: 2,       // 2 columns
    crossAxisSpacing: 10,    // horizontal gap
    mainAxisSpacing: 10,     // vertical gap
    childAspectRatio: 1.2,   // width/height ratio
  ),
  itemCount: products.length,
  itemBuilder: (context, index) {
    return ProductCard(product: products[index]);
  },
)
```

---

## Padding, Margin, Align

```dart
// Padding widget
Padding(
  padding: const EdgeInsets.all(16),           // all sides
  // padding: EdgeInsets.only(left: 16, top: 8),
  // padding: EdgeInsets.symmetric(horizontal: 20),
  child: Text('Padded text'),
)

// Align widget
Align(
  alignment: Alignment.centerRight,
  // Alignment options: topLeft, topCenter, topRight,
  //   centerLeft, center, centerRight,
  //   bottomLeft, bottomCenter, bottomRight
  child: Text('Right aligned'),
)

// Center widget (shorthand for Align.center)
Center(
  child: Text('Centered'),
)

// SizedBox — adds specific space or constrains size
SizedBox(height: 16)   // vertical spacer
SizedBox(width: 8)     // horizontal spacer
SizedBox(
  width: 200,
  height: 100,
  child: ElevatedButton(onPressed: () {}, child: Text('Button')),
)
```

---

# 5. UI Widgets

## Text & RichText

```dart
// Basic Text
Text(
  'Hello Flutter!',
  style: TextStyle(
    fontSize: 18,
    fontWeight: FontWeight.bold,
    color: Colors.blue,
    letterSpacing: 1.2,
    decoration: TextDecoration.underline,
    fontFamily: 'Poppins',
  ),
  textAlign: TextAlign.center,
  maxLines: 2,
  overflow: TextOverflow.ellipsis,
)

// RichText — different styles in one text block
RichText(
  text: TextSpan(
    style: TextStyle(color: Colors.black, fontSize: 16),
    children: [
      TextSpan(text: 'Hello '),
      TextSpan(
        text: 'Flutter',
        style: TextStyle(
          color: Colors.blue,
          fontWeight: FontWeight.bold,
          fontSize: 20,
        ),
      ),
      TextSpan(text: '! 🎉'),
    ],
  ),
)
```

---

## Image

```dart
// Image from assets
Image.asset(
  'assets/images/logo.png',
  width: 100,
  height: 100,
  fit: BoxFit.contain,
)

// Image from network
Image.network(
  'https://example.com/photo.jpg',
  width: 200,
  height: 200,
  fit: BoxFit.cover,
  loadingBuilder: (context, child, progress) {
    if (progress == null) return child;
    return CircularProgressIndicator();
  },
  errorBuilder: (context, error, stack) {
    return Icon(Icons.broken_image);
  },
)

// Cached Network Image (package: cached_network_image)
CachedNetworkImage(
  imageUrl: 'https://example.com/photo.jpg',
  placeholder: (context, url) => CircularProgressIndicator(),
  errorWidget: (context, url, error) => Icon(Icons.error),
)

// Circular image
ClipOval(
  child: Image.network(
    'https://example.com/avatar.jpg',
    width: 80,
    height: 80,
    fit: BoxFit.cover,
  ),
)
```

---

## Icon & IconButton

```dart
// Icon
Icon(
  Icons.favorite,
  color: Colors.red,
  size: 32,
)

// IconButton — tappable icon
IconButton(
  icon: Icon(Icons.share),
  iconSize: 28,
  color: Colors.blue,
  tooltip: 'Share',
  onPressed: () {
    print('Share tapped');
  },
)

// Some useful icons
// Icons.home, Icons.search, Icons.person, Icons.settings
// Icons.add, Icons.remove, Icons.delete, Icons.edit
// Icons.arrow_back, Icons.close, Icons.check, Icons.menu
```

---

## Buttons

```dart
// ElevatedButton — raised button (primary action)
ElevatedButton(
  onPressed: () => print('Pressed!'),
  style: ElevatedButton.styleFrom(
    backgroundColor: Colors.blue,
    foregroundColor: Colors.white,
    padding: EdgeInsets.symmetric(horizontal: 32, vertical: 14),
    shape: RoundedRectangleBorder(
      borderRadius: BorderRadius.circular(8),
    ),
  ),
  child: Text('Get Started', style: TextStyle(fontSize: 16)),
)

// TextButton — flat/text button (secondary action)
TextButton(
  onPressed: () {},
  child: Text('Learn More'),
)

// OutlinedButton — bordered button
OutlinedButton(
  onPressed: () {},
  style: OutlinedButton.styleFrom(
    side: BorderSide(color: Colors.blue, width: 2),
  ),
  child: Text('Outlined'),
)

// IconButton with label
ElevatedButton.icon(
  onPressed: () {},
  icon: Icon(Icons.download),
  label: Text('Download'),
)

// FloatingActionButton
FloatingActionButton(
  onPressed: () {},
  child: Icon(Icons.add),
)

// Disabled button
ElevatedButton(
  onPressed: null,  // null = disabled
  child: Text('Disabled'),
)
```

---

## TextField & Form

```dart
// Basic TextField
class LoginForm extends StatefulWidget {
  const LoginForm({super.key});

  @override
  State<LoginForm> createState() => _LoginFormState();
}

class _LoginFormState extends State<LoginForm> {
  final _formKey = GlobalKey<FormState>();
  final _emailController = TextEditingController();
  final _passwordController = TextEditingController();
  bool _obscurePassword = true;

  @override
  void dispose() {
    _emailController.dispose();   // Always dispose controllers!
    _passwordController.dispose();
    super.dispose();
  }

  void _submit() {
    if (_formKey.currentState!.validate()) {
      print('Email: ${_emailController.text}');
      print('Password: ${_passwordController.text}');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        children: [
          // Email field
          TextFormField(
            controller: _emailController,
            keyboardType: TextInputType.emailAddress,
            decoration: InputDecoration(
              labelText: 'Email',
              hintText: 'Enter your email',
              prefixIcon: Icon(Icons.email),
              border: OutlineInputBorder(
                borderRadius: BorderRadius.circular(8),
              ),
            ),
            validator: (value) {
              if (value == null || value.isEmpty) {
                return 'Please enter your email';
              }
              if (!RegExp(r'^[\w-.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(value)) {
                return 'Please enter a valid email';
              }
              return null; // valid
            },
          ),
          const SizedBox(height: 16),

          // Password field
          TextFormField(
            controller: _passwordController,
            obscureText: _obscurePassword,
            decoration: InputDecoration(
              labelText: 'Password',
              prefixIcon: Icon(Icons.lock),
              suffixIcon: IconButton(
                icon: Icon(_obscurePassword
                    ? Icons.visibility
                    : Icons.visibility_off),
                onPressed: () => setState(() {
                  _obscurePassword = !_obscurePassword;
                }),
              ),
              border: OutlineInputBorder(
                borderRadius: BorderRadius.circular(8),
              ),
            ),
            validator: (value) {
              if (value == null || value.length < 6) {
                return 'Password must be at least 6 characters';
              }
              return null;
            },
          ),
          const SizedBox(height: 24),

          SizedBox(
            width: double.infinity,
            child: ElevatedButton(
              onPressed: _submit,
              child: Text('Login'),
            ),
          ),
        ],
      ),
    );
  }
}
```

---

## Card & ListTile

```dart
// Card
Card(
  elevation: 4,
  shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
  child: Padding(
    padding: const EdgeInsets.all(16),
    child: Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Text('Card Title', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
        SizedBox(height: 8),
        Text('Card content goes here.'),
      ],
    ),
  ),
)

// ListTile — one-stop widget for list items
ListTile(
  leading: CircleAvatar(
    backgroundImage: NetworkImage('https://example.com/avatar.jpg'),
  ),
  title: Text('Rohit Kumar'),
  subtitle: Text('Flutter Developer'),
  trailing: Icon(Icons.arrow_forward_ios, size: 16),
  onTap: () => print('Tapped!'),
  onLongPress: () => print('Long pressed!'),
)
```

---

## AppBar & Scaffold

```dart
class MainScreen extends StatelessWidget {
  const MainScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // Top app bar
      appBar: AppBar(
        title: const Text('My App'),
        centerTitle: true,
        backgroundColor: Colors.blue,
        foregroundColor: Colors.white,
        elevation: 2,
        leading: IconButton(
          icon: Icon(Icons.menu),
          onPressed: () {},
        ),
        actions: [
          IconButton(icon: Icon(Icons.search), onPressed: () {}),
          IconButton(icon: Icon(Icons.notifications), onPressed: () {}),
        ],
      ),

      // Main content
      body: const Center(child: Text('Hello!')),

      // Bottom navigation
      bottomNavigationBar: NavigationBar(
        destinations: const [
          NavigationDestination(icon: Icon(Icons.home), label: 'Home'),
          NavigationDestination(icon: Icon(Icons.search), label: 'Search'),
          NavigationDestination(icon: Icon(Icons.person), label: 'Profile'),
        ],
      ),

      // Floating action button
      floatingActionButton: FloatingActionButton(
        onPressed: () {},
        child: Icon(Icons.add),
      ),

      // Side drawer
      drawer: Drawer(
        child: ListView(
          children: [
            UserAccountsDrawerHeader(
              accountName: Text('Rohit Kumar'),
              accountEmail: Text('rohit@example.com'),
              currentAccountPicture: CircleAvatar(child: Text('R')),
            ),
            ListTile(
              leading: Icon(Icons.home),
              title: Text('Home'),
              onTap: () {},
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## 📝 Exercises — Section 5

1. Build a **Profile Card** widget with avatar, name, bio, and a follow button.
2. Create a **Product Grid** screen showing 10 mock products in a 2-column grid.
3. Build a **Login Screen** with email validation and password toggle.

---

# 6. Navigation & Routing

## Navigator

```dart
// Push a new screen
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetailScreen(itemId: 42),
  ),
);

// Push and replace current screen
Navigator.pushReplacement(
  context,
  MaterialPageRoute(builder: (context) => HomeScreen()),
);

// Pop current screen (go back)
Navigator.pop(context);

// Pop with return value
Navigator.pop(context, 'result_data');

// Push and remove all previous screens (e.g., after login)
Navigator.pushAndRemoveUntil(
  context,
  MaterialPageRoute(builder: (context) => HomeScreen()),
  (route) => false, // remove all
);

// Wait for result from pushed screen
final result = await Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => SelectItemScreen()),
);
print('Selected: $result');
```

---

## Named Routes

```dart
// Define routes in MaterialApp
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => HomeScreen(),
    '/login': (context) => LoginScreen(),
    '/profile': (context) => ProfileScreen(),
    '/settings': (context) => SettingsScreen(),
  },
)

// Navigate using named route
Navigator.pushNamed(context, '/profile');

// With arguments
Navigator.pushNamed(
  context,
  '/profile',
  arguments: {'userId': 42, 'name': 'Rohit'},
);

// Receive arguments
class ProfileScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final args = ModalRoute.of(context)!.settings.arguments
        as Map<String, dynamic>;
    return Scaffold(
      body: Text('Profile of ${args['name']}'),
    );
  }
}
```

---

## GoRouter

`go_router` is the recommended modern routing package for Flutter.

```bash
flutter pub add go_router
```

```dart
import 'package:go_router/go_router.dart';

// Define routes
final router = GoRouter(
  initialLocation: '/',
  routes: [
    GoRoute(
      path: '/',
      builder: (context, state) => const HomeScreen(),
    ),
    GoRoute(
      path: '/product/:id',
      builder: (context, state) {
        final id = state.pathParameters['id']!;
        return ProductDetailScreen(productId: id);
      },
    ),
    GoRoute(
      path: '/profile',
      builder: (context, state) => const ProfileScreen(),
      routes: [
        // Nested route
        GoRoute(
          path: 'edit',
          builder: (context, state) => const EditProfileScreen(),
        ),
      ],
    ),
  ],
);

// In MaterialApp
MaterialApp.router(
  routerConfig: router,
  title: 'My App',
)

// Navigation
context.go('/');                     // Go to route (replace stack)
context.push('/product/42');         // Push onto stack
context.pop();                       // Go back
context.go('/product/${product.id}'); // Dynamic route
```

---

## Passing Data Between Screens

```dart
// Method 1: Constructor parameters
class ProductDetailScreen extends StatelessWidget {
  final Product product;
  const ProductDetailScreen({super.key, required this.product});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text(product.name)),
      body: Text(product.description),
    );
  }
}

// Usage
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => ProductDetailScreen(product: selectedProduct),
  ),
);
```

---

# 7. State Management

## setState

`setState` is the simplest form of state management — for local widget state.

```dart
class ShoppingCart extends StatefulWidget {
  const ShoppingCart({super.key});
  @override
  State<ShoppingCart> createState() => _ShoppingCartState();
}

class _ShoppingCartState extends State<ShoppingCart> {
  List<String> _items = [];

  void _addItem(String item) {
    setState(() {
      _items.add(item);
    });
  }

  void _removeItem(int index) {
    setState(() {
      _items.removeAt(index);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Cart (${_items.length} items)'),
        Expanded(
          child: ListView.builder(
            itemCount: _items.length,
            itemBuilder: (context, index) => ListTile(
              title: Text(_items[index]),
              trailing: IconButton(
                icon: Icon(Icons.delete),
                onPressed: () => _removeItem(index),
              ),
            ),
          ),
        ),
        ElevatedButton(
          onPressed: () => _addItem('New Item ${_items.length + 1}'),
          child: Text('Add Item'),
        ),
      ],
    );
  }
}
```

> 💡 **When to use setState:** Small, local UI state. Don't use for shared state across multiple screens.

---

## InheritedWidget & Provider

`Provider` is a lightweight state management solution built on `InheritedWidget`.

```bash
flutter pub add provider
```

```dart
// 1. Create a ChangeNotifier (model/store)
class CartProvider extends ChangeNotifier {
  final List<Product> _items = [];

  List<Product> get items => List.unmodifiable(_items);
  int get count => _items.length;
  double get total => _items.fold(0, (sum, item) => sum + item.price);

  void addItem(Product product) {
    _items.add(product);
    notifyListeners(); // ← Tells Flutter to rebuild listening widgets
  }

  void removeItem(Product product) {
    _items.remove(product);
    notifyListeners();
  }

  void clear() {
    _items.clear();
    notifyListeners();
  }
}

// 2. Provide it in the widget tree
void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => CartProvider(),
      child: const MyApp(),
    ),
  );
}

// 3. Consume in widgets
class CartBadge extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Watches changes — rebuilds when cart changes
    final cart = context.watch<CartProvider>();

    return Badge(
      label: Text('${cart.count}'),
      child: Icon(Icons.shopping_cart),
    );
  }
}

class AddToCartButton extends StatelessWidget {
  final Product product;
  const AddToCartButton({super.key, required this.product});

  @override
  Widget build(BuildContext context) {
    // read — doesn't watch, just reads once
    return ElevatedButton(
      onPressed: () => context.read<CartProvider>().addItem(product),
      child: Text('Add to Cart'),
    );
  }
}
```

---

## Riverpod

Riverpod is a more powerful and testable evolution of Provider.

```bash
flutter pub add flutter_riverpod
```

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

// Define a provider
final counterProvider = StateNotifierProvider<CounterNotifier, int>((ref) {
  return CounterNotifier();
});

class CounterNotifier extends StateNotifier<int> {
  CounterNotifier() : super(0);

  void increment() => state++;
  void decrement() => state--;
  void reset() => state = 0;
}

// Wrap app with ProviderScope
void main() {
  runApp(
    const ProviderScope(
      child: MyApp(),
    ),
  );
}

// Use ConsumerWidget instead of StatelessWidget
class CounterScreen extends ConsumerWidget {
  const CounterScreen({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final count = ref.watch(counterProvider);

    return Scaffold(
      appBar: AppBar(title: Text('Counter: $count')),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('$count', style: TextStyle(fontSize: 72)),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                ElevatedButton(
                  onPressed: () => ref.read(counterProvider.notifier).decrement(),
                  child: Icon(Icons.remove),
                ),
                SizedBox(width: 16),
                ElevatedButton(
                  onPressed: () => ref.read(counterProvider.notifier).increment(),
                  child: Icon(Icons.add),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

---

## BLoC Pattern

BLoC (Business Logic Component) is a powerful pattern using streams for reactive state management.

```bash
flutter pub add flutter_bloc
```

```dart
import 'package:flutter_bloc/flutter_bloc.dart';

// Events
abstract class AuthEvent {}
class LoginRequested extends AuthEvent {
  final String email;
  final String password;
  LoginRequested({required this.email, required this.password});
}
class LogoutRequested extends AuthEvent {}

// States
abstract class AuthState {}
class AuthInitial extends AuthState {}
class AuthLoading extends AuthState {}
class AuthSuccess extends AuthState {
  final String userId;
  AuthSuccess({required this.userId});
}
class AuthFailure extends AuthState {
  final String message;
  AuthFailure({required this.message});
}

// BLoC
class AuthBloc extends Bloc<AuthEvent, AuthState> {
  AuthBloc() : super(AuthInitial()) {
    on<LoginRequested>(_onLoginRequested);
    on<LogoutRequested>(_onLogoutRequested);
  }

  Future<void> _onLoginRequested(
    LoginRequested event,
    Emitter<AuthState> emit,
  ) async {
    emit(AuthLoading());
    try {
      await Future.delayed(Duration(seconds: 1)); // Simulate API
      emit(AuthSuccess(userId: 'user_123'));
    } catch (e) {
      emit(AuthFailure(message: e.toString()));
    }
  }

  void _onLogoutRequested(LogoutRequested event, Emitter<AuthState> emit) {
    emit(AuthInitial());
  }
}

// Usage in widget
BlocProvider(
  create: (context) => AuthBloc(),
  child: BlocBuilder<AuthBloc, AuthState>(
    builder: (context, state) {
      if (state is AuthLoading) return CircularProgressIndicator();
      if (state is AuthSuccess) return HomeScreen();
      if (state is AuthFailure) return Text('Error: ${state.message}');
      return LoginForm();
    },
  ),
)
```

### State Management Comparison

| Solution | Learning Curve | Best For |
|---|---|---|
| `setState` | Easy | Local, simple state |
| `Provider` | Easy-Medium | Small-medium apps |
| `Riverpod` | Medium | Medium-large apps |
| `BLoC` | Hard | Complex/enterprise apps |
| `GetX` | Easy | Rapid development |

---

# 8. Networking & API

## http Package

```bash
flutter pub add http
```

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class ApiService {
  static const String _baseUrl = 'https://jsonplaceholder.typicode.com';

  // GET request
  static Future<List<dynamic>> getPosts() async {
    final response = await http.get(
      Uri.parse('$_baseUrl/posts'),
      headers: {'Content-Type': 'application/json'},
    );

    if (response.statusCode == 200) {
      return jsonDecode(response.body) as List;
    } else {
      throw Exception('Failed to load posts: ${response.statusCode}');
    }
  }

  // POST request
  static Future<Map<String, dynamic>> createPost({
    required String title,
    required String body,
    required int userId,
  }) async {
    final response = await http.post(
      Uri.parse('$_baseUrl/posts'),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode({
        'title': title,
        'body': body,
        'userId': userId,
      }),
    );

    if (response.statusCode == 201) {
      return jsonDecode(response.body) as Map<String, dynamic>;
    } else {
      throw Exception('Failed to create post');
    }
  }

  // PUT request
  static Future<void> updatePost(int id, String title) async {
    await http.put(
      Uri.parse('$_baseUrl/posts/$id'),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode({'title': title}),
    );
  }

  // DELETE request
  static Future<void> deletePost(int id) async {
    await http.delete(Uri.parse('$_baseUrl/posts/$id'));
  }
}
```

---

## JSON Parsing

```dart
// ── Model class ──
class Post {
  final int id;
  final int userId;
  final String title;
  final String body;

  Post({
    required this.id,
    required this.userId,
    required this.title,
    required this.body,
  });

  // Parse from JSON
  factory Post.fromJson(Map<String, dynamic> json) {
    return Post(
      id: json['id'] as int,
      userId: json['userId'] as int,
      title: json['title'] as String,
      body: json['body'] as String,
    );
  }

  // Convert to JSON
  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'userId': userId,
      'title': title,
      'body': body,
    };
  }

  @override
  String toString() => 'Post(id: $id, title: $title)';
}

// Usage
final jsonData = jsonDecode(response.body);
final post = Post.fromJson(jsonData);
final posts = (jsonDecode(response.body) as List)
    .map((json) => Post.fromJson(json))
    .toList();
```

> 💡 **Tip:** Use `json_serializable` or `freezed` packages to auto-generate `fromJson`/`toJson` code for large projects.

---

## FutureBuilder & StreamBuilder

```dart
// FutureBuilder — displays data from a Future
class PostsScreen extends StatelessWidget {
  const PostsScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Posts')),
      body: FutureBuilder<List<Post>>(
        future: ApiService.getPosts(), // The Future
        builder: (context, snapshot) {
          // While loading
          if (snapshot.connectionState == ConnectionState.waiting) {
            return Center(child: CircularProgressIndicator());
          }
          // If error
          if (snapshot.hasError) {
            return Center(
              child: Text('Error: ${snapshot.error}'),
            );
          }
          // If no data
          if (!snapshot.hasData || snapshot.data!.isEmpty) {
            return Center(child: Text('No posts found'));
          }
          // Show data
          final posts = snapshot.data!;
          return ListView.builder(
            itemCount: posts.length,
            itemBuilder: (context, index) => ListTile(
              title: Text(posts[index].title),
              subtitle: Text(posts[index].body),
            ),
          );
        },
      ),
    );
  }
}

// StreamBuilder — displays data from a Stream
StreamBuilder<int>(
  stream: countDown(10),
  builder: (context, snapshot) {
    if (snapshot.connectionState == ConnectionState.done) {
      return Text('🚀 Done!');
    }
    if (snapshot.hasData) {
      return Text('${snapshot.data}', style: TextStyle(fontSize: 72));
    }
    return CircularProgressIndicator();
  },
)
```

---

# 9. Local Storage

## SharedPreferences

Best for small key-value data (user settings, auth tokens).

```bash
flutter pub add shared_preferences
```

```dart
import 'package:shared_preferences/shared_preferences.dart';

class PrefsService {
  static late SharedPreferences _prefs;

  static Future<void> init() async {
    _prefs = await SharedPreferences.getInstance();
  }

  // Save values
  static Future<void> saveToken(String token) async {
    await _prefs.setString('auth_token', token);
  }

  static Future<void> saveTheme(bool isDark) async {
    await _prefs.setBool('dark_mode', isDark);
  }

  // Read values
  static String? getToken() => _prefs.getString('auth_token');
  static bool isDarkMode() => _prefs.getBool('dark_mode') ?? false;

  // Delete
  static Future<void> clearToken() async {
    await _prefs.remove('auth_token');
  }

  static Future<void> clearAll() async {
    await _prefs.clear();
  }
}

// Initialize in main()
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await PrefsService.init();
  runApp(MyApp());
}
```

---

## SQLite (sqflite)

Best for structured/relational data.

```bash
flutter pub add sqflite path
```

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class DatabaseHelper {
  static Database? _database;

  static Future<Database> get database async {
    _database ??= await _initDatabase();
    return _database!;
  }

  static Future<Database> _initDatabase() async {
    final path = join(await getDatabasesPath(), 'app.db');
    return openDatabase(
      path,
      version: 1,
      onCreate: (db, version) async {
        await db.execute('''
          CREATE TABLE todos (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            title TEXT NOT NULL,
            isDone INTEGER NOT NULL DEFAULT 0,
            createdAt TEXT NOT NULL
          )
        ''');
      },
    );
  }

  // Insert
  static Future<int> insertTodo(Map<String, dynamic> todo) async {
    final db = await database;
    return db.insert('todos', todo);
  }

  // Read all
  static Future<List<Map<String, dynamic>>> getTodos() async {
    final db = await database;
    return db.query('todos', orderBy: 'createdAt DESC');
  }

  // Update
  static Future<int> updateTodo(int id, Map<String, dynamic> data) async {
    final db = await database;
    return db.update('todos', data, where: 'id = ?', whereArgs: [id]);
  }

  // Delete
  static Future<int> deleteTodo(int id) async {
    final db = await database;
    return db.delete('todos', where: 'id = ?', whereArgs: [id]);
  }
}
```

---

## Hive

Hive is a lightweight, fast NoSQL database — great for Flutter.

```bash
flutter pub add hive hive_flutter
```

```dart
import 'package:hive_flutter/hive_flutter.dart';

// Initialize
await Hive.initFlutter();
final box = await Hive.openBox('settings');

// Store data
await box.put('theme', 'dark');
await box.put('fontSize', 16);
await box.put('user', {'name': 'Rohit', 'age': 25});

// Read data
String theme = box.get('theme', defaultValue: 'light');
int fontSize = box.get('fontSize', defaultValue: 14);

// Delete
await box.delete('theme');
await box.clear(); // clear all
```

---

# 10. Firebase Integration

## Firebase Setup

```bash
# Install FlutterFire CLI
dart pub global activate flutterfire_cli

# Configure Firebase for your project
flutterfire configure

# Add Firebase packages
flutter pub add firebase_core firebase_auth cloud_firestore firebase_storage
```

```dart
// Initialize in main.dart
import 'package:firebase_core/firebase_core.dart';
import 'firebase_options.dart'; // Generated by flutterfire configure

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(const MyApp());
}
```

---

## Authentication

```dart
import 'package:firebase_auth/firebase_auth.dart';

class AuthService {
  final FirebaseAuth _auth = FirebaseAuth.instance;

  // Stream of auth state changes
  Stream<User?> get authStateChanges => _auth.authStateChanges();

  // Sign up with email & password
  Future<UserCredential?> signUp({
    required String email,
    required String password,
  }) async {
    try {
      return await _auth.createUserWithEmailAndPassword(
        email: email,
        password: password,
      );
    } on FirebaseAuthException catch (e) {
      throw _handleAuthError(e);
    }
  }

  // Sign in
  Future<UserCredential?> signIn({
    required String email,
    required String password,
  }) async {
    try {
      return await _auth.signInWithEmailAndPassword(
        email: email,
        password: password,
      );
    } on FirebaseAuthException catch (e) {
      throw _handleAuthError(e);
    }
  }

  // Sign out
  Future<void> signOut() => _auth.signOut();

  // Current user
  User? get currentUser => _auth.currentUser;

  String _handleAuthError(FirebaseAuthException e) {
    switch (e.code) {
      case 'weak-password': return 'Password too weak.';
      case 'email-already-in-use': return 'Email already registered.';
      case 'user-not-found': return 'No user found with this email.';
      case 'wrong-password': return 'Wrong password.';
      default: return e.message ?? 'Authentication error.';
    }
  }
}
```

---

## Firestore

```dart
import 'package:cloud_firestore/cloud_firestore.dart';

class FirestoreService {
  final FirebaseFirestore _db = FirebaseFirestore.instance;

  // Add document
  Future<DocumentReference> addPost(Map<String, dynamic> post) {
    return _db.collection('posts').add({
      ...post,
      'createdAt': FieldValue.serverTimestamp(),
    });
  }

  // Get all documents (one-time)
  Future<List<Map<String, dynamic>>> getPosts() async {
    final snapshot = await _db
        .collection('posts')
        .orderBy('createdAt', descending: true)
        .get();

    return snapshot.docs
        .map((doc) => {'id': doc.id, ...doc.data()})
        .toList();
  }

  // Real-time stream
  Stream<QuerySnapshot> postsStream() {
    return _db
        .collection('posts')
        .orderBy('createdAt', descending: true)
        .snapshots();
  }

  // Update document
  Future<void> updatePost(String id, Map<String, dynamic> data) {
    return _db.collection('posts').doc(id).update(data);
  }

  // Delete document
  Future<void> deletePost(String id) {
    return _db.collection('posts').doc(id).delete();
  }
}

// Real-time UI with StreamBuilder
StreamBuilder<QuerySnapshot>(
  stream: FirestoreService().postsStream(),
  builder: (context, snapshot) {
    if (!snapshot.hasData) return CircularProgressIndicator();
    final posts = snapshot.data!.docs;
    return ListView.builder(
      itemCount: posts.length,
      itemBuilder: (context, index) {
        final post = posts[index].data() as Map<String, dynamic>;
        return ListTile(title: Text(post['title'] ?? ''));
      },
    );
  },
)
```

---

# 11. Animations

## Implicit Animations

Implicit animations automatically animate when a property changes — easiest to use.

```dart
class AnimatedBox extends StatefulWidget {
  const AnimatedBox({super.key});
  @override
  State<AnimatedBox> createState() => _AnimatedBoxState();
}

class _AnimatedBoxState extends State<AnimatedBox> {
  bool _isExpanded = false;

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () => setState(() => _isExpanded = !_isExpanded),
      child: AnimatedContainer(
        duration: Duration(milliseconds: 400),
        curve: Curves.easeInOut,
        width: _isExpanded ? 300 : 100,
        height: _isExpanded ? 300 : 100,
        color: _isExpanded ? Colors.blue : Colors.red,
        child: Center(child: Text(_isExpanded ? 'Tap to shrink' : 'Tap!')),
      ),
    );
  }
}

// Other implicit animation widgets:
// AnimatedOpacity — fade in/out
AnimatedOpacity(
  opacity: _visible ? 1.0 : 0.0,
  duration: Duration(milliseconds: 300),
  child: Text('Fading text'),
)

// AnimatedPositioned — move widget in Stack
AnimatedPositioned(
  duration: Duration(milliseconds: 300),
  top: _isUp ? 0 : 200,
  left: 0,
  child: FlutterLogo(size: 80),
)

// AnimatedCrossFade — cross-fade between two widgets
AnimatedCrossFade(
  firstChild: CircularProgressIndicator(),
  secondChild: Text('Loaded!'),
  crossFadeState: _isLoaded
      ? CrossFadeState.showSecond
      : CrossFadeState.showFirst,
  duration: Duration(milliseconds: 300),
)
```

---

## Explicit Animations

More control over animation — use when you need fine-grained control.

```dart
class SpinningLogo extends StatefulWidget {
  const SpinningLogo({super.key});
  @override
  State<SpinningLogo> createState() => _SpinningLogoState();
}

class _SpinningLogoState extends State<SpinningLogo>
    with SingleTickerProviderStateMixin {
  late AnimationController _controller;
  late Animation<double> _rotationAnimation;
  late Animation<double> _scaleAnimation;

  @override
  void initState() {
    super.initState();

    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this, // SingleTickerProviderStateMixin provides this
    );

    _rotationAnimation = Tween<double>(begin: 0, end: 1).animate(
      CurvedAnimation(parent: _controller, curve: Curves.linear),
    );

    _scaleAnimation = Tween<double>(begin: 0.5, end: 1.5).animate(
      CurvedAnimation(parent: _controller, curve: Curves.elasticOut),
    );

    _controller.repeat(reverse: true);
  }

  @override
  void dispose() {
    _controller.dispose(); // Always dispose!
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _controller,
      builder: (context, child) {
        return Transform.scale(
          scale: _scaleAnimation.value,
          child: Transform.rotate(
            angle: _rotationAnimation.value * 2 * 3.14159,
            child: child,
          ),
        );
      },
      child: FlutterLogo(size: 100), // Built once, reused
    );
  }
}
```

---

## Hero Animations

Hero animations smoothly transition a widget between screens.

```dart
// Screen 1 — Source
GridView.builder(
  itemBuilder: (context, index) {
    return GestureDetector(
      onTap: () => Navigator.push(
        context,
        MaterialPageRoute(
          builder: (_) => ProductDetailScreen(product: products[index]),
        ),
      ),
      child: Hero(
        tag: 'product_image_${products[index].id}', // Unique tag
        child: Image.network(products[index].imageUrl, fit: BoxFit.cover),
      ),
    );
  },
)

// Screen 2 — Destination
class ProductDetailScreen extends StatelessWidget {
  final Product product;
  const ProductDetailScreen({super.key, required this.product});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          Hero(
            tag: 'product_image_${product.id}', // Same tag!
            child: Image.network(product.imageUrl, width: double.infinity),
          ),
          Text(product.name, style: TextStyle(fontSize: 24)),
        ],
      ),
    );
  }
}
```

---

# 12. Advanced Flutter

## Custom Painter

Draw custom shapes, charts, and graphics with `CustomPainter`.

```dart
class CircleProgressPainter extends CustomPainter {
  final double progress; // 0.0 to 1.0
  final Color color;

  CircleProgressPainter({required this.progress, required this.color});

  @override
  void paint(Canvas canvas, Size size) {
    final center = Offset(size.width / 2, size.height / 2);
    final radius = size.width / 2 - 10;

    // Background circle
    canvas.drawCircle(
      center,
      radius,
      Paint()
        ..color = Colors.grey[200]!
        ..style = PaintingStyle.stroke
        ..strokeWidth = 10,
    );

    // Progress arc
    canvas.drawArc(
      Rect.fromCircle(center: center, radius: radius),
      -3.14159 / 2,          // start angle (top)
      progress * 2 * 3.14159, // sweep angle
      false,
      Paint()
        ..color = color
        ..style = PaintingStyle.stroke
        ..strokeWidth = 10
        ..strokeCap = StrokeCap.round,
    );
  }

  @override
  bool shouldRepaint(CircleProgressPainter oldDelegate) {
    return oldDelegate.progress != progress || oldDelegate.color != color;
  }
}

// Usage
CustomPaint(
  size: Size(200, 200),
  painter: CircleProgressPainter(progress: 0.75, color: Colors.blue),
)
```

---

## Isolates & Compute

Run heavy computations on a background thread (Isolate) to keep UI smooth.

```dart
import 'package:flutter/foundation.dart';

// Heavy computation function (must be top-level or static)
List<int> findPrimes(int limit) {
  List<int> primes = [];
  for (int i = 2; i <= limit; i++) {
    bool isPrime = true;
    for (int j = 2; j * j <= i; j++) {
      if (i % j == 0) {
        isPrime = false;
        break;
      }
    }
    if (isPrime) primes.add(i);
  }
  return primes;
}

// Run on background isolate using compute
class PrimeCalculator extends StatefulWidget {
  const PrimeCalculator({super.key});
  @override
  State<PrimeCalculator> createState() => _PrimeCalculatorState();
}

class _PrimeCalculatorState extends State<PrimeCalculator> {
  List<int>? _primes;
  bool _loading = false;

  Future<void> _calculate() async {
    setState(() => _loading = true);

    // compute() runs findPrimes in a separate isolate
    final primes = await compute(findPrimes, 100000);

    setState(() {
      _primes = primes;
      _loading = false;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        ElevatedButton(
          onPressed: _loading ? null : _calculate,
          child: Text(_loading ? 'Calculating...' : 'Find Primes'),
        ),
        if (_primes != null)
          Text('Found ${_primes!.length} primes up to 100,000'),
      ],
    );
  }
}
```

---

# 13. Testing

## Unit Tests

```dart
// test/services/calculator_test.dart
import 'package:flutter_test/flutter_test.dart';
import 'package:my_app/services/calculator.dart';

void main() {
  group('Calculator', () {
    late Calculator calc;

    setUp(() {
      calc = Calculator(); // Runs before each test
    });

    test('add returns correct sum', () {
      expect(calc.add(2, 3), equals(5));
      expect(calc.add(-1, 1), equals(0));
      expect(calc.add(0, 0), equals(0));
    });

    test('divide throws on zero division', () {
      expect(() => calc.divide(10, 0), throwsArgumentError);
    });

    test('multiply handles negative numbers', () {
      expect(calc.multiply(-2, 3), equals(-6));
      expect(calc.multiply(-2, -3), equals(6));
    });
  });
}

// Run tests:
// flutter test
// flutter test test/services/calculator_test.dart
```

## Widget Tests

```dart
// test/widgets/counter_widget_test.dart
import 'package:flutter/material.dart';
import 'package:flutter_test/flutter_test.dart';
import 'package:my_app/widgets/counter_widget.dart';

void main() {
  testWidgets('Counter increments when + button tapped', (tester) async {
    // Build widget
    await tester.pumpWidget(
      MaterialApp(
        home: Scaffold(body: CounterWidget(title: 'Test Counter')),
      ),
    );

    // Find initial text
    expect(find.text('0'), findsOneWidget);
    expect(find.text('1'), findsNothing);

    // Tap + button
    await tester.tap(find.byIcon(Icons.add));
    await tester.pump(); // Trigger rebuild

    // Verify counter incremented
    expect(find.text('0'), findsNothing);
    expect(find.text('1'), findsOneWidget);
  });

  testWidgets('Counter cannot go below zero', (tester) async {
    await tester.pumpWidget(
      MaterialApp(home: Scaffold(body: CounterWidget(title: 'Test'))),
    );

    // Tap minus button
    await tester.tap(find.byIcon(Icons.remove));
    await tester.pump();

    // Should still show 0
    expect(find.text('0'), findsOneWidget);
  });
}
```

---

# 14. Deployment

## Android

```bash
# 1. Create keystore
keytool -genkey -v -keystore ~/key.jks -keyalias my_key -keyalgRSA -keysize 2048 -validity 10000

# 2. Configure signing in android/key.properties
storePassword=<password>
keyPassword=<password>
keyAlias=my_key
storeFile=<path to key.jks>

# 3. Build App Bundle (for Play Store — preferred)
flutter build appbundle --release

# 4. Build APK (for direct distribution)
flutter build apk --release
flutter build apk --split-per-abi  # Smaller per-architecture APKs

# Output: build/app/outputs/flutter-apk/
```

## iOS

```bash
# Must be on macOS with Xcode

# 1. Open in Xcode to configure signing
open ios/Runner.xcworkspace

# 2. Build for release
flutter build ios --release

# 3. Archive and upload via Xcode or Transporter
```

## Web

```bash
# Build for web
flutter build web --release

# With specific base href (for subdirectory deployment)
flutter build web --base-href /myapp/

# Output: build/web/
# Deploy to Firebase Hosting, Netlify, Vercel, etc.

# Firebase hosting
firebase deploy --only hosting
```

---

# 15. Best Practices

## Code Organization

```dart
// ✅ DO: Keep widgets small and focused
class UserAvatar extends StatelessWidget {
  final String imageUrl;
  final double size;

  const UserAvatar({super.key, required this.imageUrl, this.size = 40});

  @override
  Widget build(BuildContext context) {
    return CircleAvatar(
      radius: size / 2,
      backgroundImage: NetworkImage(imageUrl),
    );
  }
}

// ✅ DO: Extract business logic from widgets
class ProductViewModel extends ChangeNotifier {
  // All business logic here, not in widgets
  Future<void> addToCart(Product product) async { ... }
  double calculateDiscount(Product product) { ... }
}

// ✅ DO: Use const constructors everywhere possible
const Text('Hello');           // ✅ Doesn't rebuild unnecessarily
const SizedBox(height: 16);    // ✅
const EdgeInsets.all(16);      // ✅

// ✅ DO: Dispose resources
@override
void dispose() {
  _controller.dispose();
  _scrollController.dispose();
  _textController.dispose();
  _subscription.cancel();
  super.dispose();
}

// ❌ AVOID: deeply nested widget trees (callback hell for widgets)
// Use extract method refactoring to break it up
Widget _buildHeader() {
  return Row(children: [...]);
}

Widget _buildBody() {
  return Column(children: [...]);
}
```

## Naming Conventions

```dart
// Files — snake_case
// user_profile_screen.dart
// api_service.dart
// cart_provider.dart

// Classes — PascalCase
class UserProfileScreen {}
class ApiService {}
class CartProvider {}

// Variables & functions — camelCase
String userName = '';
void fetchUserData() {}

// Constants — camelCase with const
const int maxRetries = 3;
const String apiBaseUrl = 'https://api.example.com';

// Private members — prefix with underscore
String _password = '';
void _handleLogin() {}

// Widget keys — use meaningful names
Key('login_button')
Key('email_input')
```

## Performance Tips

```dart
// ✅ Use ListView.builder for long lists, never ListView with many children

// ✅ const widgets don't rebuild — use them everywhere
const Text('Static text');
const SizedBox(height: 8);

// ✅ RepaintBoundary — isolate heavy widgets from rebuilds
RepaintBoundary(
  child: ComplexChartWidget(),
)

// ✅ Cache expensive calculations with memoization
// Use select() to listen to only part of a provider
final userName = context.select<UserProvider, String>(
  (provider) => provider.user.name,
);

// ✅ Use Image.asset with cacheWidth/cacheHeight
Image.asset(
  'assets/images/banner.jpg',
  cacheWidth: 800, // decode at display size, not full res
)

// ✅ Avoid rebuilding entire tree — use Consumer/Selector in right place
// ❌ Bad — entire screen rebuilds
Consumer<CartProvider>(
  builder: (context, cart, child) => Scaffold(...), // Entire scaffold rebuilds!
)

// ✅ Good — only badge rebuilds
Scaffold(
  appBar: AppBar(
    actions: [
      Consumer<CartProvider>(
        builder: (context, cart, child) => CartBadge(count: cart.count),
      ),
    ],
  ),
  body: ProductGrid(), // Doesn't rebuild on cart changes
)
```

---

# 16. Exercises & Challenges

## 🟢 Beginner

1. **Counter App** — Build a counter with increment, decrement, and reset. Display history of last 5 values.
2. **Todo App** — CRUD todo app with local state. Checkboxes to mark complete, swipe to delete.
3. **Profile Card** — Build a card with avatar, name, bio, followers/following count, and a follow button that toggles.

## 🟡 Intermediate

4. **Weather App** — Fetch weather from OpenWeatherMap API, show current conditions and 5-day forecast.
5. **Notes App** — Notes with SQLite storage. CRUD, search, and sort by date.
6. **Quiz App** — MCQ quiz with timer, score tracking, and results screen with animation.

## 🔴 Advanced

7. **E-Commerce App** — Product listing, cart with Provider/Riverpod, checkout flow, order history with Firestore.
8. **Chat App** — Real-time chat using Firebase with message bubbles, typing indicator, and push notifications.
9. **Expense Tracker** — Track expenses with categories, charts (using `fl_chart`), monthly summaries, and export to CSV.

---

# 17. Conclusion & Resources

## 🎯 Flutter Learning Roadmap

```
Beginner
├── Dart fundamentals
├── StatelessWidget & StatefulWidget
├── Basic layout widgets
├── Navigation basics
└── Basic state with setState

Intermediate
├── State management (Provider/Riverpod)
├── REST APIs & JSON parsing
├── Local storage
├── Forms & validation
└── Firebase integration

Advanced
├── Custom animations
├── Custom painter
├── BLoC pattern
├── Testing (unit + widget)
└── Performance optimization

Expert
├── Platform channels (native code)
├── Custom render objects
├── Flutter engine internals
└── Package development & publishing
```

## 📚 Official Resources

- 🌐 [Flutter Official Docs](https://flutter.dev/docs)
- 🎮 [DartPad (Online Playground)](https://dartpad.dev)
- 📦 [pub.dev — Flutter Packages](https://pub.dev)
- 📖 [Dart Language Tour](https://dart.dev/language)
- 🎥 [Flutter YouTube Channel](https://www.youtube.com/@flutterdev)

## 🏆 Must-Know Packages

| Package | Use Case |
|---|---|
| `provider` | Simple state management |
| `flutter_riverpod` | Advanced state management |
| `flutter_bloc` | BLoC pattern |
| `go_router` | Declarative routing |
| `dio` | HTTP client |
| `hive` | Local NoSQL database |
| `sqflite` | SQLite database |
| `firebase_core` | Firebase |
| `cached_network_image` | Cached images |
| `fl_chart` | Beautiful charts |
| `lottie` | Lottie animations |
| `freezed` | Immutable data classes |
| `get_it` | Dependency injection |

## 🛠️ Recommended VS Code Extensions

| Extension | Purpose |
|---|---|
| **Flutter** | Official extension |
| **Dart** | Dart language support |
| **Pubspec Assist** | Manage dependencies easily |
| **Flutter Widget Snippets** | Code snippets |
| **Error Lens** | Inline errors |
| **Awesome Flutter Snippets** | More snippets |
| **Rainbow Brackets** | Bracket color coding |

## GitHub Repositories

- ⭐ [flutter/flutter](https://github.com/flutter/flutter) — Official Flutter repo
- 📚 [londonappbrewery/FlutterCourse](https://github.com/londonappbrewery/Flutter-Course-Resources)
- 🧩 [flutter/samples](https://github.com/flutter/samples)
- 📦 [felangel/bloc](https://github.com/felangel/bloc) — BLoC library

## 🎉 Conclusion

You've covered Flutter from **zero to hero**! Here's your journey recap:

- ✅ **Dart Basics** — Null safety, async/await, OOP
- ✅ **Widgets** — Stateless, Stateful, lifecycle
- ✅ **Layouts** — Row, Column, Stack, ListView, GridView
- ✅ **State Management** — setState, Provider, Riverpod, BLoC
- ✅ **Networking** — http, Dio, JSON parsing, FutureBuilder
- ✅ **Storage** — SharedPreferences, SQLite, Hive
- ✅ **Firebase** — Auth, Firestore, Storage
- ✅ **Animations** — Implicit, Explicit, Hero
- ✅ **Testing & Deployment**

### Key Takeaways

1. **Everything is a widget** — embrace it.
2. **Keep widgets small** — extract, reuse, compose.
3. **Pick state management carefully** — start with setState/Provider, graduate to Riverpod/BLoC as app grows.
4. **Always dispose controllers** — prevent memory leaks.
5. **Use const everywhere** — free performance boost.
6. **Test early** — widget and unit tests save debugging time.

---

> 💙 *"Flutter is not just a framework — it's a superpower for developers."*

**Happy Fluttering! Keep Building! 🚀**

---

*Made with ❤️ | Flutter 3.x | Dart 3.x | Last updated: 2024*
