# Java Programming Notes

## Table of Contents
1. [Data Types](#data-types)
2. [Reading Java Code](#reading-java-code)
3. [Input and Output](#input-and-output)
4. [Control Statements](#control-statements)
5. [Recursive Methods](#recursive-methods)

## Data Types

### Primitive Data Types

1. **Integer Types**
   - `byte`: 8-bit integer (-128 to 127)
   - `short`: 16-bit integer (-32,768 to 32,767)
   - `int`: 32-bit integer (-2^31 to 2^31-1)
   - `long`: 64-bit integer (-2^63 to 2^63-1)

   Example:
   ```java
   byte age = 25;
   short population = 32000;
   int worldPopulation = 7800000;
   long bankBalance = 1234567890L; // Note the 'L' suffix for long
   ```

2. **Floating-Point Types**
   - `float`: 32-bit floating-point (6-7 decimal digits)
   - `double`: 64-bit floating-point (15-16 decimal digits)

   Example:
   ```java
   float price = 19.99f;  // Note the 'f' suffix for float
   double pi = 3.14159265359;
   ```

3. **Character Type**
   - `char`: 16-bit Unicode character

   Example:
   ```java
   char grade = 'A';
   char symbol = '$';
   ```

4. **Boolean Type**
   - `boolean`: true or false

   Example:
   ```java
   boolean isJavaFun = true;
   boolean isCodingHard = false;
   ```

### Reference Data Types

1. **String**
   ```java
   String name = "John Doe";
   String message = new String("Hello, World!");
   ```

2. **Arrays**
   ```java
   int[] numbers = {1, 2, 3, 4, 5};
   String[] names = new String[3];
   names[0] = "Alice";
   ```

3. **Classes and Objects**
   ```java
   class Person {
       String name;
       int age;
   }
   Person person = new Person();
   ```

## Reading Java Code

### Basic Structure of a Java Program

```java
// Package declaration (optional)
package com.example;

// Import statements (optional)
import java.util.Scanner;

// Class declaration
public class Main {
    // Main method - program entry point
    public static void main(String[] args) {
        // Code goes here
    }
}
```

### Naming Conventions
- Classes: PascalCase (MyClass)
- Methods and Variables: camelCase (myMethod, myVariable)
- Constants: UPPER_SNAKE_CASE (MAX_VALUE)
- Packages: lowercase (com.example.project)

## Input and Output

### Console Output
```java
// Print without new line
System.out.print("Hello");

// Print with new line
System.out.println("Hello, World!");

// Formatted output
System.out.printf("Name: %s, Age: %d%n", "John", 25);
```

### Console Input
```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);

// Reading different types
String name = scanner.nextLine();     // Read a line of text
int age = scanner.nextInt();          // Read an integer
double salary = scanner.nextDouble(); // Read a double
boolean flag = scanner.nextBoolean(); // Read a boolean

// Don't forget to close the scanner
scanner.close();
```

## Control Statements

### 1. Conditional Statements

#### If-Else
```java
if (condition) {
    // code if condition is true
} else if (anotherCondition) {
    // code if anotherCondition is true
} else {
    // code if all conditions are false
}
```

#### Switch
```java
switch (variable) {
    case value1:
        // code
        break;
    case value2:
        // code
        break;
    default:
        // default code
}
```

### 2. Loops

#### For Loop
```java
// Traditional for loop
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}

// Enhanced for loop (for-each)
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```

#### While Loop
```java
int count = 0;
while (count < 5) {
    System.out.println(count);
    count++;
}
```

#### Do-While Loop
```java
int x = 0;
do {
    System.out.println(x);
    x++;
} while (x < 5);
```

## Recursive Methods

Recursion is when a method calls itself to solve a problem by breaking it down into smaller subproblems.

### Example 1: Factorial Calculation
```java
public static int factorial(int n) {
    // Base case
    if (n == 0 || n == 1) {
        return 1;
    }
    // Recursive case
    return n * factorial(n - 1);
}
```

### Example 2: Fibonacci Sequence
```java
public static int fibonacci(int n) {
    // Base cases
    if (n <= 1) {
        return n;
    }
    // Recursive case
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```

### Example 3: Binary Search
```java
public static int binarySearch(int[] arr, int left, int right, int target) {
    if (right >= left) {
        int mid = left + (right - left) / 2;

        // If element is present at the middle
        if (arr[mid] == target)
            return mid;

        // If element is smaller than mid
        if (arr[mid] > target)
            return binarySearch(arr, left, mid - 1, target);

        // If element is larger than mid
        return binarySearch(arr, mid + 1, right, target);
    }

    // Element not present in array
    return -1;
}
```

### Tips for Writing Recursive Methods
1. Always have a base case to prevent infinite recursion
2. Each recursive call should work towards the base case
3. Ensure the recursive solution is more efficient than an iterative one
4. Be mindful of stack overflow for deep recursions

### Common Use Cases for Recursion
- Tree and graph traversal
- Divide and conquer algorithms
- Backtracking problems
- Mathematical calculations
- File system operations
