# C++ Notes

## Data Types in C++

C++ supports several data types, which can be broadly categorized into:

- **Primitive Data Types**: These include `int`, `char`, `float`, `double`, and `bool`.
- **Derived Data Types**: These include arrays, pointers, and references.
- **User-defined Data Types**: These include structures, unions, and classes.

### Examples:

- **int**: Used to store integers.
  ```cpp
  int age = 25;
  ```

- **char**: Used to store single characters.
  ```cpp
  char grade = 'A';
  ```

- **float** and **double**: Used to store floating-point numbers.
  ```cpp
  float salary = 50000.50;
  double pi = 3.14159;
  ```

- **bool**: Used to store boolean values (`true` or `false`).
  ```cpp
  bool isStudent = true;
  ```

## Reading Java Code

While C++ and Java are different languages, understanding Java code can be easier if you know C++ because both are object-oriented. Key differences include:

- **Syntax**: Java uses `System.out.println()` for output, while C++ uses `std::cout`.
- **Memory Management**: Java has automatic garbage collection, whereas C++ requires manual memory management.
- **Inheritance**: Java supports single inheritance with interfaces, while C++ supports multiple inheritance.

## Input and Output in C++

C++ uses streams for input and output operations:

- **Input**: `std::cin` is used to read input from the standard input (keyboard).
- **Output**: `std::cout` is used to write output to the standard output (screen).

### Example:

```cpp
#include <iostream>
using namespace std;

int main() {
    int number;
    cout << "Enter a number: ";
    cin >> number;
    cout << "You entered: " << number << endl;
    return 0;
}
```

## Types of Statements

- **Conditional Statements**: `if`, `else if`, `else`, and `switch`.
- **Looping Statements**: `for`, `while`, and `do-while`.
- **Jump Statements**: `break`, `continue`, and `return`.

### Example:

```cpp
#include <iostream>
using namespace std;

int main() {
    int num = 10;

    // Conditional statement
    if (num > 0) {
        cout << "Positive number" << endl;
    } else {
        cout << "Non-positive number" << endl;
    }

    // Looping statement
    for (int i = 0; i < 5; i++) {
        cout << "i: " << i << endl;
    }

    return 0;
}
```

## Recursive Methods

Recursion is a method where a function calls itself to solve a problem. It's often used for problems that can be broken down into smaller, similar problems.

### Example: Factorial Calculation

```cpp
#include <iostream>
using namespace std;

int factorial(int n) {
    if (n <= 1) return 1; // Base case
    return n * factorial(n - 1); // Recursive call
}

int main() {
    int num = 5;
    cout << "Factorial of " << num << " is " << factorial(num) << endl;
    return 0;
}
```
