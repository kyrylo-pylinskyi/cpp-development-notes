# Method Overloading in Static Polymorphism

Method overloading is a key feature in C++ that enables static polymorphism, also known as compile-time polymorphism. This feature allows multiple methods to share the same name but differ in their parameter lists (i.e., the number and/or types of their parameters). The compiler determines which method to invoke based on the arguments provided in the function call.

## Key Concepts

### Definition

Method overloading means having multiple functions with the same name in the same scope, but with different parameter lists.

### Syntax

To overload a method, you simply define multiple versions of the method with different signatures (parameter lists).

```cpp
ReturnType MethodName(ParameterList1);
ReturnType MethodName(ParameterList2);
```

### Example: Method Overloading

Here's an example of method overloading in a class:

```cpp
#include <iostream>

class Print {
public:
    // Overloaded method for integer
    void display(int i) {
        std::cout << "Displaying integer: " << i << std::endl;
    }

    // Overloaded method for double
    void display(double d) {
        std::cout << "Displaying double: " << d << std::endl;
    }

    // Overloaded method for string
    void display(const std::string& s) {
        std::cout << "Displaying string: " << s << std::endl;
    }
};

int main() {
    Print printer;

    printer.display(10);             // Calls display(int)
    printer.display(3.14);           // Calls display(double)
    printer.display("Hello World");  // Calls display(const std::string&)
    return 0;
}
```

### Function Resolution

The compiler resolves the function call at compile time based on the arguments' types and number. This is why method overloading is considered a form of static polymorphism.

## Advantages of Method Overloading

1. **Readability**: Using the same method name for similar actions improves code readability.
2. **Maintainability**: It is easier to maintain and modify overloaded methods since they are logically grouped under the same name.
3. **Type Safety**: Errors are caught at compile time, ensuring type safety.

## Disadvantages of Method Overloading

1. **Code Bloat**: Can lead to larger binary sizes because multiple versions of a function need to be compiled.
2. **Complexity**: Can increase the complexity of the codebase if overused or not well-documented.

## Advanced Examples

### Overloading with Default Arguments

Default arguments can also be combined with method overloading:

```cpp
#include <iostream>

class Example {
public:
    void func(int x, int y = 10) {
        std::cout << "First function: " << x << ", " << y << std::endl;
    }

    void func(double x) {
        std::cout << "Second function: " << x << std::endl;
    }
};

int main() {
    Example ex;

    ex.func(5);        // Calls func(int, int) with default y = 10
    ex.func(5, 15);    // Calls func(int, int) with y = 15
    ex.func(3.14);     // Calls func(double)
    return 0;
}
```

### Overloading with Reference and Const

Method overloading can also differentiate based on whether parameters are passed by value, by reference, or as const references:

```cpp
#include <iostream>

class Example {
public:
    void func(int& x) {
        std::cout << "Non-const reference: " << x << std::endl;
    }

    void func(const int& x) {
        std::cout << "Const reference: " << x << std::endl;
    }
};

int main() {
    int a = 10;
    const int b = 20;

    Example ex;
    ex.func(a); // Calls func(int&)
    ex.func(b); // Calls func(const int&)
    return 0;
}
```

### Combining Overloading and Templates

Combining templates with method overloading enables even more powerful and flexible designs:

```cpp
#include <iostream>

class Example {
public:
    void func(int x) {
        std::cout << "Integer function: " << x << std::endl;
    }

    void func(double x) {
        std::cout << "Double function: " << x << std::endl;
    }

    template <typename T>
    void func(T x) {
        std::cout << "Template function: " << x << std::endl;
    }
};

int main() {
    Example ex;

    ex.func(5);       // Calls func(int)
    ex.func(3.14);    // Calls func(double)
    ex.func("Hello"); // Calls func(T) - template version
    return 0;
}
```

## Best Practices

1. **Clarity**: Overloaded methods should have a clear, distinct purpose and not perform unrelated tasks.
2. **Consistency**: Maintain consistency in method names and parameters to ensure readability.
3. **Documentation**: Document the purpose and usage of each overloaded method to avoid confusion.

## Conclusion

Method overloading in C++ is a powerful feature that enhances code readability and maintainability by allowing multiple functions to share the same name but operate on different parameters. This form of static polymorphism enables compile-time type checking, resulting in safer and more efficient code. Understanding and using method overloading effectively is essential for writing clean, maintainable, and efficient C++ code.