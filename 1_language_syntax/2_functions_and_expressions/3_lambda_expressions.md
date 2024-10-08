# Lambda Expressions

Lambda expressions in C++ provide a concise way to define anonymous functions directly in the code. Introduced in C++11, they enable developers to write inline function definitions, making code more readable and expressive, especially when dealing with algorithms or callback functions.

## Key Features of Lambda Expressions

### 1. Syntax

The basic syntax of a lambda expression is:

```cpp
[capture](parameters) -> return_type { body }
```

- **Capture**: Specifies which variables from the surrounding scope are accessible within the lambda.
- **Parameters**: Similar to function parameters, defining the input for the lambda.
- **Return Type**: Optional specification of the return type; if omitted, the compiler deduces it.
- **Body**: The function implementation, enclosed in braces.

### 2. Capture Lists

The capture list defines how variables from the surrounding scope are used within the lambda. There are several capture modes:

- **By Value**: `[x]` captures `x` by value.
- **By Reference**: `[&x]` captures `x` by reference.
- **All By Value**: `[=]` captures all accessible variables by value.
- **All By Reference**: `[&]` captures all accessible variables by reference.

#### Example

```cpp
int a = 10;
auto lambdaByValue = [a]() { return a + 5; }; // Captures a by value
auto lambdaByReference = [&a]() { a += 5; }; // Captures a by reference
```

### 3. Implicit Return Type

If the return type is omitted, the compiler deduces it. If the lambda has a single return statement, the return type can be inferred automatically.

#### Example

```cpp
auto square = [](int x) { return x * x; }; // Return type deduced as int
```

### 4. Mutable Lambdas

By default, lambdas that capture variables by value cannot modify them. To allow modifications, use the `mutable` keyword.

#### Example

```cpp
int a = 5;
auto lambda = [a]() mutable { a += 10; return a; }; // a is modified inside the lambda
```

### 5. Lambda Expressions as Function Objects

Lambdas can be used wherever function objects are required, such as in algorithms or when passing callbacks.

#### Example

```cpp
#include <vector>
#include <algorithm>

std::vector<int> vec = {1, 2, 3, 4, 5};
std::for_each(vec.begin(), vec.end(), [](int x) { std::cout << x * 2 << " "; });
```

### 6. Lambdas in Standard Library Algorithms

Lambdas are often used with standard library algorithms to create more readable and concise code.

#### Example

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

std::vector<int> numbers = {1, 2, 3, 4, 5};
std::for_each(numbers.begin(), numbers.end(), [](int n) { std::cout << n * n << " "; });
```

### 7. Capturing `this` Pointer

In member functions, you can capture the `this` pointer to access class members.

#### Example

```cpp
class Example {
public:
    void display() {
        int x = 10;
        auto lambda = [this, x]() { std::cout << this->memberVar + x; };
        lambda();
    }

private:
    int memberVar = 5;
};
```

## Use Cases for Lambda Expressions

### 1. Inline Function Definitions

Lambdas allow you to define functions inline, which can make your code cleaner and reduce the need for separate function definitions.

### 2. Customizing Standard Algorithms

Lambdas are ideal for customizing the behavior of standard algorithms, such as sorting, filtering, and transforming collections.

### 3. Callback Functions

Lambdas can serve as concise callback functions, making it easier to pass behavior to functions without the overhead of defining a separate function.

## Conclusion

Lambda expressions are a powerful feature of C++ that enhance the expressiveness and readability of code. By allowing inline function definitions and providing flexible capture mechanisms, lambdas facilitate the development of modern C++ applications, especially when used with the standard library and algorithms. Understanding and utilizing lambda expressions is essential for any C++ programmer looking to write clean and efficient code.