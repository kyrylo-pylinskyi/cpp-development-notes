# Basic Stream Classes

C++ provides several standard classes for handling input and output operations. These classes are designed to work seamlessly with the I/O system in C++ and offer a range of functionalities to perform data exchange operations. Here’s a detailed overview of the basic stream classes with code examples:

## `iostream`: Input and Output Stream Base Class

`std::iostream` is a base class that combines both input and output functionalities. It is derived from `std::istream` and `std::ostream`, making it suitable for operations that require both input and output capabilities.

### Example:

```cpp
#include <iostream>

int main() {
    std::string name;
    int age;

    // Input
    std::cout << "Enter your name: ";
    std::getline(std::cin, name);
    std::cout << "Enter your age: ";
    std::cin >> age;

    // Output
    std::cout << "Name: " << name << std::endl;
    std::cout << "Age: " << age << std::endl;

    return 0;
}
```

## `istream`: Input Stream

`std::istream` is a class designed for input operations. It provides methods to read data from various sources, such as the console, files, or custom input streams.

### Example:

```cpp
#include <iostream>

int main() {
    int number;
    std::cout << "Enter a number: ";
    std::cin >> number;
    std::cout << "You entered: " << number << std::endl;
    return 0;
}
```

## `ostream`: Output Stream

`std::ostream` is a class for output operations, allowing data to be written to various destinations like the console, files, or custom output streams.

### Example:

```cpp
#include <iostream>

int main() {
    std::string message = "Hello, World!";
    std::cout << message << std::endl;
    return 0;
}
```

## `fstream`: File Stream

`std::fstream` combines input and output operations for file streams. It allows both reading from and writing to files using a single stream object.

### Example:

```cpp
#include <fstream>
#include <iostream>

int main() {
    // Writing to a file
    std::ofstream outFile("example.txt");
    if (outFile.is_open()) {
        outFile << "This is a test file." << std::endl;
        outFile.close();
    }

    // Reading from a file
    std::ifstream inFile("example.txt");
    std::string line;
    if (inFile.is_open()) {
        while (getline(inFile, line)) {
            std::cout << line << std::endl;
        }
        inFile.close();
    }

    return 0;
}
```

## `ifstream`: Input File Stream

`std::ifstream` is a specialized stream class for reading data from files. It is derived from `std::istream` and is used exclusively for input operations on files.

### Example:

```cpp
#include <fstream>
#include <iostream>

int main() {
    std::ifstream file("example.txt");
    if (file.is_open()) {
        std::string line;
        while (getline(file, line)) {
            std::cout << line << std::endl;
        }
        file.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }
    return 0;
}
```

## `ofstream`: Output File Stream

`std::ofstream` is a specialized stream class for writing data to files. It is derived from `std::ostream` and is used exclusively for output operations on files.

### Example:

```cpp
#include <fstream>
#include <iostream>

int main() {
    std::ofstream file("output.txt");
    if (file.is_open()) {
        file << "Writing data to the file." << std::endl;
        file.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }
    return 0;
}
```

## `stringstream`: String Stream

`std::stringstream` is a stream class used to operate on strings. It allows for both input and output operations on string data.

### Example:

```cpp
#include <sstream>
#include <iostream>
#include <string>

int main() {
    std::stringstream ss;

    // Writing to string stream
    ss << "This is a string stream example.";

    // Reading from string stream
    std::string content;
    ss >> content;

    std::cout << "First word: " << content << std::endl;

    // Clear the stringstream and set new content
    ss.clear();
    ss.str("Another example");

    std::string newContent;
    ss >> newContent;

    std::cout << "New content: " << newContent << std::endl;

    return 0;
}
```

## `istringstream`: Input String Stream

`std::istringstream` is a specialized stream class derived from `std::istream` for reading data from strings. It is used for input operations on string data.

### Example:

```cpp
#include <sstream>
#include <iostream>
#include <string>

int main() {
    std::string data = "42 3.14 Hello";
    std::istringstream iss(data);

    int integer;
    double floatingPoint;
    std::string word;

    iss >> integer >> floatingPoint >> word;

    std::cout << "Integer: " << integer << std::endl;
    std::cout << "Floating point: " << floatingPoint << std::endl;
    std::cout << "Word: " << word << std::endl;

    return 0;
}
```

## `ostringstream`: Output String Stream

`std::ostringstream` is a specialized stream class derived from `std::ostream` for writing data to strings. It is used for output operations on string data.

### Example:

```cpp
#include <sstream>
#include <iostream>
#include <string>

int main() {
    std::ostringstream oss;

    // Writing to string stream
    oss << "The answer is: " << 42;

    std::string result = oss.str();
    std::cout << result << std::endl;

    return 0;
}
```

These basic stream classes provide the foundational tools for handling I/O operations in C++. Understanding these classes and their functionalities is crucial for effectively performing input and output tasks in C++ programming.