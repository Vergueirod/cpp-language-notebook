## 📘 Personal C++ Language Guide

---

### 1. Introduction

C++ is a general-purpose programming language created by Bjarne Stroustrup at Bell Labs starting in 1979. Initially an extension of the C language (hence "C with Classes"), it introduced object-oriented features while retaining C's efficiency. The core philosophy behind C++ is to provide high performance and fine-grained control over system resources while supporting multiple paradigms, including procedural, object-oriented, and generic programming.

**Compilation/Execution Example:**
```bash
# Compile a C++ program
g++ hello.cpp -o hello

# Execute the compiled program
./hello
```

---

### 2. Data Types and Variables

**Primitive Types:**
- `int` (integer)
- `float` (floating-point)
- `double` (double-precision floating-point)
- `char` (character)
- `bool` (boolean)

**Modifiers:**
- `short`, `long`, `signed`, `unsigned`

**Constants:**
```cpp
const int MAX_COUNT = 100;
```

**Enums:**
```cpp
enum Color { RED, GREEN, BLUE };
Color favorite = GREEN;
```

**Variable Declarations:**
```cpp
int age = 30;
float weight = 65.5f;
char grade = 'A';
bool isPassed = true;
```

---

### 3. Operators

**Arithmetic Operators:**
```cpp
int sum = a + b;
int diff = a - b;
int product = a * b;
int quotient = a / b;
int remainder = a % b;
```

**Relational Operators:**
```cpp
if (a == b)
if (a != b)
if (a > b)
if (a < b)
if (a >= b)
if (a <= b)
```

**Logical Operators:**
```cpp
if (a && b)
if (a || b)
if (!a)
```

**Bitwise Operators:**
```cpp
int result = a & b;
result = a | b;
result = a ^ b;
result = ~a;
result = a << 2;
result = a >> 2;
```

---

### 4. Input/Output (I/O)

**Standard I/O:**
```cpp
#include <iostream>
using namespace std;

cout << "Enter a number: ";
int num;
cin >> num;
cout << "You entered: " << num << endl;
```

**Clearing Input Buffer (cin.ignore, cin.clear):**
```cpp
// Clear the input buffer before reading a line after extracting input
type:
cin.ignore(numeric_limits<streamsize>::max(), '\n');
```

- **When to Use:** After reading input with `cin >>`, if you plan to use `getline` afterward. This clears leftover characters (like newline) from the input buffer.
- **Why Use:** Prevents unexpected behavior when mixing formatted and unformatted input methods.

**File I/O:**
```cpp
#include <fstream>
using namespace std;

ofstream outFile("output.txt");
outFile << "Hello, File!";
outFile.close();

ifstream inFile("output.txt");
string line;
getline(inFile, line);
cout << line << endl;
inFile.close();
```

---

### 5. Control Flow

**Conditionals:**
```cpp
if (x > 0) {
    cout << "Positive";
} else if (x < 0) {
    cout << "Negative";
} else {
    cout << "Zero";
}

switch (day) {
    case 1: cout << "Monday"; break;
    case 2: cout << "Tuesday"; break;
    default: cout << "Other day";
}
```

**Loops:**
```cpp
for (int i = 0; i < 5; i++) {
    cout << i << endl;
}

int j = 0;
while (j < 5) {
    cout << j << endl;
    j++;
}

do {
    cout << j << endl;
    j++;
} while (j < 5);
```

---

### 6. Functions/Methods

**Function Declaration and Usage:**
```cpp
int add(int a, int b) {
    return a + b;
}

cout << add(3, 4);
```

**Pass-by-Value and Pass-by-Reference:**
```cpp
void incrementByValue(int x) {
    x++;
}

void incrementByReference(int &x) {
    x++;
}

int num = 5;
incrementByValue(num);  // num remains 5
incrementByReference(num);  // num becomes 6
```

---

### 7. Advanced Structures

**Classes and Structs Overview:**

C++ supports object-oriented programming through **classes** and **structs**. The only difference is that members of a struct are **public by default**, while members of a class are **private by default**.

**Access Specifiers:**
- `public`: Accessible from outside the class.
- `private`: Accessible only within the class itself.
- `protected`: Accessible within the class and by derived classes.

**Example with Access Specifiers:**
```cpp
class Car {
private:
    string brand;  // Private member: accessible only within Car

public:
    Car(string b) { brand = b; }  // Public constructor

    void displayBrand() {  // Public method
        cout << "Brand: " << brand << endl;
    }
};

Car myCar("Toyota");
myCar.displayBrand();  // OK
// myCar.brand;  // Error: brand is private
```

**Deep Dive: Encapsulation** 

At its core, encapsulation is about hiding internal data and implementation details of a class, and exposing only what’s necessary through controlled interfaces (usually public methods).

Why?

- Prevents unauthorized or accidental modification of data.
- Allows you to change the internal implementation without breaking external code.
- Improves maintainability, security, and abstraction.

Think of it as putting sensitive components inside a box with a locked lid—users can only interact with it via buttons on the outside.

 **Getters and Setters: The Access Gateways**

These are public methods that allow reading (getter) or writing (setter) a private variable.
Without getters/setters, the variable is directly exposed and vulnerable.

```cpp
#include <iostream>
#include <string>
using namespace std;

class Person {
private:
    string name;
    int age;

public:
    // Constructor
    Person(string name, int age) {
        this->name = name;
        setAge(age);  // validate age at initialization
    }

    // Getter for name
    string getName() {
        return name;
    }

    // Setter for name
    void setName(string newName) {
        if (newName.empty()) {
            cout << "Name cannot be empty!" << endl;
        } else {
            name = newName;
        }
    }

    // Getter for age
    int getAge() {
        return age;
    }

    // Setter for age
    void setAge(int newAge) {
        if (newAge >= 0 && newAge <= 150) {
            age = newAge;
        } else {
            cout << "Invalid age!" << endl;
        }
    }

    void display() {
        cout << "Name: " << name << ", Age: " << age << endl;
    }
};

int main() {
    Person p1("Alice", 30);
    p1.display();

    p1.setAge(200);  // Invalid attempt
    p1.setName("");  // Invalid attempt

    p1.setAge(35);
    p1.setName("Alice Cooper");
    p1.display();

    return 0;
}
```

**Real-World Analogy: Car Dashboard**
Think of encapsulation like a car’s dashboard:

You (the driver) don’t access the engine directly.

You use the gas pedal (setter) to control speed → the car takes care of complex inner mechanics.

You read the speedometer (getter) to know current speed.

The engine internals are encapsulated; you're only given a safe, simple interface.






**When to Use Access Specifiers:**
- **Private:** For data encapsulation and hiding implementation details. Keeps internal state safe from unintended modifications.
- **Public:** For methods or variables that form the class interface (e.g., getters, setters, or public operations).
- **Protected:** Mainly used in inheritance to expose internals to derived classes but not the outside world.

**When Not to Use:**
- Avoid using `public` data members. Prefer private data with public getters/setters to maintain control over the internal state.

**Types of Classes:**
- **Concrete Class:** Implements full functionality. Use for standard class design.
- **Abstract Class:** Contains at least one pure virtual function (`virtual void foo() = 0;`). Use for defining base interfaces requiring derived class implementations.
- **Interface Class:** Abstract class with only pure virtual functions. Use to define consistent APIs across unrelated classes.
- **Final Class:** Prevents further inheritance (`class MyClass final`). Use to lock the hierarchy to improve safety or performance.
- **Polymorphic Class:** Designed to support runtime polymorphism via virtual functions. Useful for dynamic behavior binding.

**When Not to Use Certain Classes:**
- Avoid abstract/interface classes if no clear benefit from polymorphism.
- Avoid deep or wide inheritance trees as they complicate maintenance and reduce flexibility.
- Prefer composition over inheritance when possible for better modularity.

**Arrays:**
```cpp
int arr[3] = {1, 2, 3};
```

**Vectors:**
```cpp
#include <vector>
vector<int> vec = {1, 2, 3};
vec.push_back(4);
```

**Pointers and References:**
```cpp
int val = 10;
int* ptr = &val;  // Pointer
int& ref = val;  // Reference
```

**Classes and Structs:**
```cpp
class Person {
public:
    string name;
    int age;

    void greet() {
        cout << "Hello, " << name << endl;
    }
};

Person p;
p.name = "John";
p.age = 30;
p.greet();
```

**Types of Classes:**
- **Concrete Class:** Implements full functionality. Use for general object-oriented design.
- **Abstract Class:** Contains at least one pure virtual function (`virtual void foo() = 0;`). Use when defining interfaces for derived classes.
- **Interface Class:** Abstract class with only pure virtual functions. Use when multiple unrelated classes need a common API.
- **Final Class:** Prevents further inheritance (`class MyClass final`). Use to lock hierarchy for performance or design reasons.
- **When Not to Use:** Avoid unnecessary abstractions or deep inheritance trees, as they complicate maintenance.

---

### 8. Memory Management

**Stack vs Heap:**
- Stack: Automatically managed, fast, limited size.
- Heap: Dynamically allocated, must be manually managed, flexible size.

**Dynamic Memory Allocation:**
```cpp
int* ptr = new int(5);  // Allocates on heap
cout << *ptr << endl;
delete ptr;  // Free memory
```

---

### 9. Macros/Preprocessor

```cpp
#define PI 3.14159

#ifdef PI
cout << "PI is defined" << endl;
#endif
```

---

### 10. Practical Examples Section

**Hello World:**
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```

**Simple Calculator:**
```cpp
#include <iostream>
using namespace std;

int main() {
    char op;
    double num1, num2;
    cout << "Enter operator (+, -, *, /): ";
    cin >> op;
    cout << "Enter two numbers: ";
    cin >> num1 >> num2;

    switch(op) {
        case '+': cout << num1 + num2; break;
        case '-': cout << num1 - num2; break;
        case '*': cout << num1 * num2; break;
        case '/': cout << num1 / num2; break;
        default: cout << "Invalid operator";
    }
    return 0;
}
```

**File Reader:**
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ifstream file("example.txt");
    string line;

    while (getline(file, line)) {
        cout << line << endl;
    }
    file.close();
    return 0;
}
```

---

### 11. Common Errors and Technical Explanations

1. **Segmentation Fault:**
   - **Cause:** Dereferencing null or invalid pointers.
   - **Solution:** Always initialize pointers and check their validity before use.

2. **Mixing cin and getline without clearing buffer:**
   - **Cause:** `cin` leaves newline characters in the input buffer, causing `getline` to read an empty line.
   - **Solution:** Use `cin.ignore()` before calling `getline`.

3. **Memory Leaks:**
   - **Cause:** Forgetting to `delete` dynamically allocated memory.
   - **Solution:** Always pair `new` with `delete` and consider using smart pointers (`std::unique_ptr`, `std::shared_ptr`).

4. **Undefined Behavior:**
   - **Cause:** Accessing uninitialized variables, dangling pointers, or out-of-bounds array indices.
   - **Solution:** Initialize variables, avoid manual pointer arithmetic, and use container classes like `std::vector`.

5. **Name Collisions in Multiple Headers:**
   - **Cause:** Defining the same function or variable in multiple translation units.
   - **Solution:** Use include guards (`#ifndef HEADER_H`) or `#pragma once`.
