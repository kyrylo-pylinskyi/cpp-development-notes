# Error Handling

Error handling is crucial in software development to manage and recover from unexpected or exceptional situations during program execution. In C++, error handling is typically achieved using exceptions and error codes. This section covers both approaches and best practices for effective error management.

## Exceptions

[[2_exceptions|Exceptions]] provide a powerful mechanism to handle errors and propagate them across different parts of a program. They allow you to separate error-handling code from normal program flow, promoting cleaner and more maintainable code.

### Throwing Exceptions

In C++, exceptions are thrown using the `throw` keyword followed by an exception object. Exceptions can be of any type, including standard library types or custom-defined types.

```cpp
#include <iostream>

void processData(int value) {
    if (value < 0) {
        throw std::runtime_error("Value cannot be negative.");
    }
    // Process data if value is valid
    std::cout << "Processing data with value: " << value << std::endl;
}

int main() {
    try {
        processData(-10);
    } catch (const std::runtime_error& e) {
        std::cerr << "Exception caught: " << e.what() << std::endl;
    }
    return 0;
}
```

In this example:
- `processData` function checks if the `value` parameter is negative.
- If `value` is negative, a `std::runtime_error` exception is thrown with an appropriate error message.
- In `main`, the exception is caught using a `try-catch` block, and the error message (`e.what()`) is printed.

### Custom Exception Classes

You can define custom exception classes to encapsulate specific error conditions in your application.

```cpp
#include <iostream>
#include <stdexcept>

class FileIOException : public std::runtime_error {
public:
    FileIOException(const std::string& message) : std::runtime_error(message) {}
};

void readFromFile(const std::string& filename) {
    // Attempt to open file
    if (!std::ifstream(filename)) {
        throw FileIOException("Failed to open file: " + filename);
    }
    // Read file contents
    std::cout << "Reading from file: " << filename << std::endl;
}

int main() {
    try {
        readFromFile("nonexistent.txt");
    } catch (const FileIOException& e) {
        std::cerr << "FileIOException caught: " << e.what() << std::endl;
    }
    return 0;
}
```

### Exception Specifications

C++ allows specifying the types of exceptions that a function can throw using exception specifications (`throw` clause), but modern C++ prefers using `noexcept` specifier for better performance and safety.

```cpp
void mightThrow() noexcept(false); // Can throw any exception except noexcept

void noThrow() noexcept; // Does not throw any exceptions

void oldStyleThrow() throw(int, std::runtime_error); // Can throw int or std::runtime_error
```

## Error Codes

Error codes are traditional C-style error-handling mechanisms where functions return an error code to indicate success or failure. Error codes are simpler but can lead to error-prone code if not handled properly.

### Returning Error Codes

Functions return error codes (typically integer values) where a non-zero value indicates an error.

```cpp
#include <iostream>

int divide(int numerator, int denominator, int& result) {
    if (denominator == 0) {
        return -1; // Return -1 to indicate division by zero
    }
    result = numerator / denominator;
    return 0; // Return 0 to indicate success
}

int main() {
    int numerator = 10, denominator = 0, result;
    if (divide(numerator, denominator, result) != 0) {
        std::cerr << "Error: Division by zero." << std::endl;
    } else {
        std::cout << "Result of division: " << result << std::endl;
    }
    return 0;
}
```

### Error Handling with Error Codes

Error codes need to be checked explicitly after each function call, which can clutter the main logic with error-handling code.

## Choosing Between Exceptions and Error Codes

- **Exceptions**: Use when the error is exceptional and the normal flow of the program cannot handle it easily. Provides cleaner code with separation of error-handling logic.
  
- **Error Codes**: Use when the error is expected and can be handled locally. Suitable for simple functions or performance-critical code where exceptions might be too costly.

### Best Practices

- **Consistency**: Choose one error-handling mechanism (exceptions or error codes) and stick with it throughout your codebase.
- **Specificity**: Use specific exception classes or error codes to convey detailed error information.
- **Resource Management**: Ensure proper resource cleanup using [[5_RAII_in_exception_handling|RAII]] (Resource Acquisition Is Initialization) with exceptions.
- **Logging**: Log error messages for debugging and tracing purposes.
- **Documentation**: Document error-handling strategies and expected exceptions in function documentation.

### Conclusion

Effective error handling is essential for writing robust and maintainable C++ programs. Understanding when to use exceptions versus error codes and following best practices ensures reliable software that gracefully handles unexpected situations. Choose the right approach based on the context and requirements of your application.