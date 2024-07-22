# Try and Catch in C++

Exception handling in C++ is a crucial feature that allows a program to deal with unexpected situations or errors in a controlled manner. The `try` and `catch` blocks are the primary constructs used for this purpose.

## Structure of Exception Handling

1. **Try Block**: Encapsulates the code that might throw an exception.
2. **Catch Block**: Captures and handles the exception.

### Basic Example

```cpp
#include <iostream>
#include <stdexcept>

void mayThrow() {
    throw std::runtime_error("An error occurred");
}

int main() {
    try {
        mayThrow();
    } catch (const std::runtime_error& e) {
        std::cerr << "Caught a runtime_error: " << e.what() << std::endl;
    } catch (...) {
        std::cerr << "Caught an unknown exception" << std::endl;
    }

    return 0;
}
```

### Detailed Exception Handling

In real-world scenarios, you might want to catch different types of exceptions separately, including standard library exceptions, custom exceptions, and catch-all blocks for any other exceptions.

#### Standard Library Exceptions

The C++ Standard Library provides a hierarchy of exception classes, all derived from `std::exception`. Some common ones include:
- `std::logic_error`
- `std::runtime_error`
- `std::bad_alloc`
- `std::out_of_range`

#### User-Defined Exceptions

You can create your own exception classes by inheriting from `std::exception` or any of its derived classes.

```cpp
class MyException : public std::exception {
public:
    const char* what() const noexcept override {
        return "MyException occurred";
    }
};
```

### Comprehensive Example

This example demonstrates how to handle various types of exceptions, including custom exceptions and using RAII for resource management.

```cpp
#include <iostream>
#include <stdexcept>
#include <memory>

// User-defined exception
class MyException : public std::exception {
public:
    const char* what() const noexcept override {
        return "MyException occurred";
    }
};

void riskyOperation() {
    // Uncomment one of the following lines to test different exceptions
    // throw std::runtime_error("Standard library exception");
    // throw MyException();
    // throw 42; // Catch-all example
}

int main() {
    try {
        riskyOperation();
    } catch (const std::runtime_error& e) {
        std::cerr << "Caught a runtime_error: " << e.what() << std::endl;
    } catch (const MyException& e) {
        std::cerr << "Caught MyException: " << e.what() << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Caught a standard exception: " << e.what() << std::endl;
    } catch (...) {
        std::cerr << "Caught an unknown exception" << std::endl;
    }

    return 0;
}
```

### RAII in Exception Handling

RAII ensures resources are properly released even if an exception occurs. Smart pointers like `std::unique_ptr` and `std::shared_ptr` manage dynamic memory, freeing it when it goes out of scope.

#### Example: Using RAII with Smart Pointers

```cpp
#include <iostream>
#include <memory>

class Resource {
public:
    Resource() {
        std::cout << "Resource acquired\n";
    }

    ~Resource() {
        std::cout << "Resource released\n";
    }

    void doSomething() {
        std::cout << "Doing something with resource\n";
    }
};

void useResource() {
    try {
        std::unique_ptr<Resource> resource = std::make_unique<Resource>();
        resource->doSomething();

        // Simulate an exception
        throw std::runtime_error("An error occurred");

        resource->doSomething(); // This will not be called
    } catch (const std::exception& e) {
        std::cerr << "Exception: " << e.what() << std::endl;
    }
}

int main() {
    useResource();

    return 0;
}
```

In this example, the `Resource` object is automatically cleaned up when an exception is thrown, preventing resource leaks.

### Catching Multiple Exception Types

C++ allows you to catch multiple types of exceptions by placing multiple `catch` blocks after a `try` block. The first matching `catch` block is executed.

```cpp
try {
    // Code that might throw exceptions
} catch (const std::runtime_error& e) {
    // Handle runtime errors
} catch (const std::logic_error& e) {
    // Handle logic errors
} catch (const MyException& e) {
    // Handle user-defined exceptions
} catch (const std::exception& e) {
    // Handle all other standard exceptions
} catch (...) {
    // Catch-all handler for any other types of exceptions
}
```

### Summary

Exception handling with `try` and `catch` blocks in C++ provides a robust mechanism to handle runtime errors and exceptional conditions. By using RAII, you can ensure that resources are managed correctly, preventing leaks and undefined behavior even in the presence of exceptions.