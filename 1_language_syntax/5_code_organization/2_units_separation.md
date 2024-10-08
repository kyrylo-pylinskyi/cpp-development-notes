
# Headers and CPP Units Separation

Separating header files (`.h` or `.hpp`) from source files (`.cpp`) is a common practice in C++ programming that promotes modularity, maintainability, and clarity. This separation helps manage large codebases by clearly defining interfaces and implementations.

## Key Concepts

### 1. Header Files

Header files contain declarations of classes, functions, constants, and macros. They provide the interface that other parts of the program can use without exposing the implementation details.

#### Example: `MyClass.h`

```cpp
#ifndef MYCLASS_H
#define MYCLASS_H

class MyClass {
public:
    MyClass();
    ~MyClass();

    void doSomething();

private:
    int data;
};

#endif // MYCLASS_H
```

### 2. Source Files

Source files contain the definitions of the functions and methods declared in the header files. They include the corresponding header file and provide the actual implementation.

#### Example: `MyClass.cpp`

```cpp
#include "MyClass.h"
#include <iostream>

MyClass::MyClass() : data(0) {
    // Constructor implementation
}

MyClass::~MyClass() {
    // Destructor implementation
}

void MyClass::doSomething() {
    std::cout << "Doing something with data: " << data << std::endl;
}
```

### 3. Include Guards

Include guards prevent multiple inclusions of the same header file, which can cause errors. They are usually implemented with preprocessor directives `#ifndef`, `#define`, and `#endif`.

#### Example

```cpp
#ifndef MYCLASS_H
#define MYCLASS_H

// Declarations

#endif // MYCLASS_H
```

### 4. Forward Declarations
[[3_forward_declaration]]

Forward declarations declare the existence of a class or function without defining it. This helps reduce dependencies and compilation times.

#### Example

```cpp
// Forward declaration
class MyClass;

class AnotherClass {
    MyClass* ptr; // Use of forward-declared class
};
```

### 5. Dependencies Management

Separating headers and source files helps manage dependencies more effectively. Changes in implementation do not require recompilation of dependent files, only those directly including the modified header.

### 6. Implementation Hiding

By separating the interface (header) from the implementation (source), details of the implementation can be hidden from the users of the class. This allows for changes in the implementation without affecting the users of the class.

## Benefits

- **Modularity**: Clear separation of interface and implementation promotes modular design.
- **Maintainability**: Easier to maintain and update code as the interface and implementation are distinct.
- **Compilation Efficiency**: Reduces the amount of code that needs to be recompiled when changes are made.
- **Encapsulation**: Hides implementation details, exposing only what is necessary.

## Best Practices

- **Consistent Naming**: Use consistent naming conventions for header and source files (e.g., `MyClass.h` and `MyClass.cpp`).
- **Minimal Headers**: Include only necessary headers in other headers; include other dependencies in source files.
- **Use Forward Declarations**: Where possible, use forward declarations to reduce dependencies.
- **Avoid Implementation in Headers**: Avoid defining functions in headers unless they are template functions or inline functions.

## Conclusion

Separating headers and source files is a fundamental practice in C++ that enhances the clarity, modularity, and maintainability of code. By adhering to best practices in separating declarations and implementations, developers can create more robust and scalable applications.