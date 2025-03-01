# C# Programming Notes

## Table of Contents
1. [Data Types](#data-types)
2. [Variables and Constants](#variables-and-constants)
3. [Input and Output](#input-and-output)
4. [Control Statements](#control-statements)
5. [Methods and Recursion](#methods-and-recursion)
6. [Converting from Java to C#](#converting-from-java-to-c)

## Data Types

### Value Types (Stored on Stack)

1. **Integer Types**
   - `byte`: 8-bit unsigned integer (0 to 255)
   - `sbyte`: 8-bit signed integer (-128 to 127)
   - `short`: 16-bit signed integer (-32,768 to 32,767)
   - `ushort`: 16-bit unsigned integer (0 to 65,535)
   - `int`: 32-bit signed integer (-2^31 to 2^31-1)
   - `uint`: 32-bit unsigned integer (0 to 2^32-1)
   - `long`: 64-bit signed integer
   - `ulong`: 64-bit unsigned integer

   Example:
   ```csharp
   int age = 25;
   long population = 7800000000L;
   ```

2. **Floating-Point Types**
   - `float`: 32-bit single-precision (7 digits precision)
   - `double`: 64-bit double-precision (15-17 digits precision)
   - `decimal`: 128-bit precise decimal (28-29 digits precision)

   Example:
   ```csharp
   float price = 19.99f;
   double pi = 3.14159265359;
   decimal accountBalance = 1234.56m;
   ```

3. **Boolean Type**
   - `bool`: Represents true/false values

   Example:
   ```csharp
   bool isActive = true;
   bool hasPermission = false;
   ```

4. **Character Type**
   - `char`: 16-bit Unicode character

   Example:
   ```csharp
   char grade = 'A';
   char symbol = '$';
   ```

### Reference Types (Stored on Heap)

1. **String**
   - Immutable sequence of characters

   Example:
   ```csharp
   string name = "John Doe";
   string message = $"Hello, {name}!"; // String interpolation
   ```

2. **Object**
   - Base type of all other types

   Example:
   ```csharp
   object obj = 42;
   object str = "Hello";
   ```

3. **Arrays**
   - Fixed-size collection of elements

   Example:
   ```csharp
   int[] numbers = new int[5];
   string[] names = {"Alice", "Bob", "Charlie"};
   ```

## Variables and Constants

### Variable Declaration
```csharp
// Type inference
var age = 25;
var name = "John";

// Explicit type declaration
int count = 0;
string message = "Hello";

// Multiple declarations
int x = 1, y = 2, z = 3;
```

### Constants
```csharp
const double PI = 3.14159;
const string APP_NAME = "MyApp";
```

## Input and Output

### Console Input
```csharp
// Reading a string
Console.Write("Enter your name: ");
string name = Console.ReadLine();

// Reading and converting to other types
Console.Write("Enter your age: ");
int age = Convert.ToInt32(Console.ReadLine());

// Alternative parsing
Console.Write("Enter a number: ");
if (int.TryParse(Console.ReadLine(), out int number))
{
    Console.WriteLine($"Parsed number: {number}");
}
```

### Console Output
```csharp
// Basic output
Console.WriteLine("Hello, World!");

// Formatted output
string name = "Alice";
int age = 25;
Console.WriteLine("Name: {0}, Age: {1}", name, age);

// String interpolation
Console.WriteLine($"Name: {name}, Age: {age}");

// Formatting numbers
double price = 19.99;
Console.WriteLine($"Price: ${price:F2}");
```

## Control Statements

### If-Else Statements
```csharp
int age = 18;

if (age >= 18)
{
    Console.WriteLine("Adult");
}
else if (age >= 13)
{
    Console.WriteLine("Teenager");
}
else
{
    Console.WriteLine("Child");
}
```

### Switch Statement
```csharp
char grade = 'B';

switch (grade)
{
    case 'A':
        Console.WriteLine("Excellent!");
        break;
    case 'B':
        Console.WriteLine("Good!");
        break;
    case 'C':
        Console.WriteLine("Fair");
        break;
    default:
        Console.WriteLine("Invalid grade");
        break;
}
```

### Loops

1. **For Loop**
```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine($"Iteration {i}");
}
```

2. **While Loop**
```csharp
int count = 0;
while (count < 5)
{
    Console.WriteLine($"Count: {count}");
    count++;
}
```

3. **Do-While Loop**
```csharp
int num = 1;
do
{
    Console.WriteLine(num);
    num *= 2;
} while (num <= 8);
```

4. **Foreach Loop**
```csharp
string[] fruits = {"apple", "banana", "orange"};
foreach (string fruit in fruits)
{
    Console.WriteLine(fruit);
}
```

## Methods and Recursion

### Method Declaration
```csharp
// Basic method
public void Greet(string name)
{
    Console.WriteLine($"Hello, {name}!");
}

// Method with return value
public int Add(int a, int b)
{
    return a + b;
}

// Method with optional parameters
public void PrintInfo(string name, int age = 20)
{
    Console.WriteLine($"{name} is {age} years old");
}
```

### Recursive Methods
```csharp
// Factorial calculation using recursion
public int Factorial(int n)
{
    if (n <= 1)
        return 1;
    return n * Factorial(n - 1);
}

// Fibonacci sequence using recursion
public int Fibonacci(int n)
{
    if (n <= 1)
        return n;
    return Fibonacci(n - 1) + Fibonacci(n - 2);
}
```

## Converting from Java to C#

### Key Differences

1. **Naming Conventions**
   - C#: PascalCase for methods and properties
   - Java: camelCase for methods

2. **Properties vs Getters/Setters**
```csharp
// C# Property
public string Name { get; set; }

// Java equivalent
private String name;
public String getName() { return name; }
public void setName(String name) { this.name = name; }
```

3. **Package vs Namespace**
```csharp
// C#
namespace MyApplication
{
    // code here
}

// Java
package myapplication;
// code here
```

4. **Main Method**
```csharp
// C#
public static void Main(string[] args)
{
    // code here
}

// Java
public static void main(String[] args)
{
    // code here
}
```

5. **Arrays**
```csharp
// C#
int[] numbers = new int[5];
string[] names = new string[] {"Alice", "Bob"};

// Java
int[] numbers = new int[5];
String[] names = new String[] {"Alice", "Bob"};
```

### Common Java to C# Translations

| Java | C# |
|------|-----|
| System.out.println() | Console.WriteLine() |
| String | string |
| Integer | int |
| Boolean | bool |
| null | null |
| this | this |
| extends | : |
| implements | : |
| interface | interface |
| final | sealed |
| import | using |
