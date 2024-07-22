# Exceptions

Exceptions are a powerful mechanism in C++ for handling errors and exceptional situations during program execution. This topic covers both standard exceptions provided by the Standard Library (STL) and how to define and use custom exceptions in your programs.

#### Standard Exceptions in STL

The STL (Standard Template Library) provides a set of [[3_standard_exceptions|standard exception classes]] defined in `<stdexcept>` header. Here are some commonly used standard exceptions:

- **`std::exception`**: The base class for all standard C++ exceptions. It defines the virtual function `what()` which returns an explanatory string.
  
- **`std::runtime_error`**: Represents errors detected during runtime, such as logic errors or errors that can only be determined during execution.
  
- **`std::logic_error`**: Represents errors in the program's logic, such as invalid argument errors that should be detected before execution.
  
- **`std::invalid_argument`**: Indicates that a function has been called with an invalid argument.
  
- **`std::domain_error`**: Indicates errors where a mathematical function is not defined (e.g., calculating the square root of a negative number).
  
- **`std::length_error`**: Indicates that a container (such as `std::string` or `std::vector`) reached its maximum allowable size.
  
- **`std::out_of_range`**: Indicates that an argument value is out of the allowed range (e.g., accessing an element out of bounds in a container).

Example of using standard exceptions:

```cpp
#include <iostream>
#include <stdexcept>

void processInput(int value) {
    if (value <= 0) {
        throw std::invalid_argument("Value must be positive.");
    }
    // Process valid input
    std::cout << "Input value: " << value << std::endl;
}

int main() {
    try {
        processInput(-5);
    } catch (const std::exception& e) {
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
    return 0;
}
```

#### User-Defined Exceptions

You can define your own exception classes to handle specific error conditions in your application. This allows you to encapsulate detailed error information and customize error handling.

```cpp
#include <iostream>
#include <exception>

class FileOpenException : public std::exception {
private:
    std::string message_;

public:
    FileOpenException(const std::string& message) : message_(message) {}

    const char* what() const noexcept override {
        return message_.c_str();
    }
};

void openFile(const std::string& filename) {
    if (!std::ifstream(filename)) {
        throw FileOpenException("Failed to open file: " + filename);
    }
    std::cout << "File opened successfully: " << filename << std::endl;
}

int main() {
    try {
        openFile("nonexistent.txt");
    } catch (const FileOpenException& e) {
        std::cerr << "FileOpenException caught: " << e.what() << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
    return 0;
}
```

In this example:
- `FileOpenException` is a custom exception class derived from `std::exception`.
- It overrides the `what()` function to provide a meaningful error message.
- `openFile()` function throws `FileOpenException` when it fails to open a file.

### Best Practices for Exception Handling

- **Catch Exceptions Appropriately**: Catch exceptions at an appropriate level of abstraction, handling specific exceptions first.
  
- **Provide Contextual Information**: Ensure exceptions provide enough information for debugging and error diagnosis.
  
- **Use RAII**: Use RAII (Resource Acquisition Is Initialization) to manage resources safely, ensuring proper cleanup in case of exceptions.
  
- **Consistent Error Handling**: Maintain consistency in error handling across your codebase, choosing between exceptions and error codes where appropriate.

### Conclusion

Exception handling in C++ improves code robustness by allowing graceful recovery from errors. By understanding and using both standard exceptions and user-defined exceptions effectively, you can write more reliable and maintainable C++ programs. Choose the right exceptions for your application's error-handling needs to ensure software stability and resilience.