# Type Deduction

Type deduction in C++ refers to the compiler's ability to automatically determine the type of a variable or expression. This feature enhances code readability and maintainability by reducing the need to explicitly specify types. The main mechanisms for type deduction in C++ are the [`auto`](2_auto.md) keyword and the [`decltype`](3_decltype.md) keyword.

## `auto` Keyword

The `auto` keyword allows the compiler to infer the type of a variable from its initializer.

### Basic Usage

```cpp
auto x = 42;        // x is deduced as int
auto y = 3.14;      // y is deduced as double
auto str = "Hello"; // str is deduced as const char*
```

### Functions and `auto`

When used in function return types, `auto` can deduce the return type based on the return statements.

```cpp
auto add(int a, int b) {
    return a + b; // deduces return type as int
}

auto multiply(double a, double b) -> double {
    return a * b; // explicitly specifies return type
}
```

### Range-based For Loop

```cpp
#include <vector>

std::vector<int> vec = {1, 2, 3, 4, 5};
for (auto val : vec) {
    std::cout << val << std::endl;
}
```

### Type Deduction with `auto`

The type deduced by `auto` depends on the initializer. Here are a few rules and examples:

- **References and Pointers**: The deduced type retains references and pointers.

```cpp
int a = 5;
int& ref = a;
auto x = ref; // x is deduced as int (not int&)

int* ptr = &a;
auto y = ptr; // y is deduced as int*
```

- **Const and Volatile Qualifiers**: `auto` drops `const` and `volatile` qualifiers unless explicitly stated.

```cpp
const int ci = 42;
auto x1 = ci; // x is deduced as int, not const int

volatile int vi = 21;
auto x2 = vi; // x is deduced as int, not volatile int

const auto& y = ci; // y is deduced as const int&
```

## `decltype` Keyword

The `decltype` keyword deduces the type of an expression. Unlike `auto`, it does not depend on initialization but directly inspects the expression.

### Basic Usage

```cpp
int a = 5;
decltype(a) b = a; // b is deduced as int

decltype(a + 2.0) c; // c is deduced as double
```

### `decltype` with Expressions

`decltype` can be useful for deducing the type of complex expressions or the return type of functions.

```cpp
int foo() { return 42; }
decltype(foo()) x = foo(); // x is deduced as int

auto lambda = [](int a, double b) -> decltype(a + b) {
    return a + b; // return type deduced as double
};
```

### References and `decltype`

When `decltype` is used with expressions, it preserves references.

```cpp
int a = 5;
int& ref = a;
decltype(ref) x = a; // x is deduced as int&

decltype((a)) y = a; // y is deduced as int& (extra parentheses force it to deduce as reference)
```

### `decltype(auto)`

`decltype(auto)` combines the type deduction of `auto` with the reference preservation of `decltype`.

```cpp
int a = 5;
int& ref = a;

decltype(auto) x = ref; // x is deduced as int&
decltype(auto) y = a;   // y is deduced as int
```

## Practical Examples

### Functions Returning `auto`

```cpp
#include <vector>

auto createVector() {
    return std::vector<int>{1, 2, 3, 4, 5}; // deduces return type as std::vector<int>
}

auto add(int a, int b) -> decltype(a + b) {
    return a + b; // deduces return type based on expression type
}
```

### Complex Type Deduction

```cpp
#include <vector>
#include <iostream>

std::vector<int> vec = {1, 2, 3, 4, 5};

for (decltype(vec)::size_type i = 0; i < vec.size(); ++i) {
    std::cout << vec[i] << std::endl;
}
```

## Summary

- **`auto`**: Simplifies variable declaration by letting the compiler infer the type from the initializer.
- **`decltype`**: Deduces the type of an expression, useful for complex type deduction and preserving references.
- **`decltype(auto)`**: Combines the benefits of `auto` and `decltype` for more precise type deduction.

Type deduction enhances code readability and maintainability by reducing verbosity and minimizing type-related errors.