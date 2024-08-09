# 3. Stream Operations

Stream operations are fundamental to input and output handling in C++. This chapter delves into various operations you can perform on streams, including reading, writing, formatting, and error handling.

## 3.1 Reading from Streams

Reading from streams involves extracting data from an input source. C++ provides various ways to read data using streams.

### 3.1.1 Using the Extraction Operator (`>>`)

The extraction operator (`>>`) is used to read data from an input stream.

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

### 3.1.2 Using `getline()`

The `getline()` function is used to read a line of text from an input stream.

```cpp
#include <iostream>
#include <string>

int main() {
    std::string line;
    std::cout << "Enter a line: ";
    std::getline(std::cin, line);
    std::cout << "You entered: " << line << std::endl;
    return 0;
}
```

### 3.1.3 Using `read()`

The `read()` function reads a specified number of characters from a stream into a buffer.

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ifstream file("example.txt", std::ios::binary);
    if (file.is_open()) {
        char buffer[100];
        file.read(buffer, sizeof(buffer));
        std::cout.write(buffer, file.gcount());
        file.close();
    }
    return 0;
}
```

## 3.2 Writing to Streams

Writing to streams involves sending data to an output destination.

### 3.2.1 Using the Insertion Operator (`<<`)

The insertion operator (`<<`) is used to write data to an output stream.

```cpp
#include <iostream>

int main() {
    int number = 42;
    std::cout << "The number is: " << number << std::endl;
    return 0;
}
```

### 3.2.2 Using `write()`

The `write()` function writes a specified number of characters from a buffer to a stream.

```cpp
#include <iostream>
#include <fstream>

int main() {
    std::ofstream file("example.txt", std::ios::binary);
    if (file.is_open()) {
        const char* text = "Hello, Binary File!";
        file.write(text, std::strlen(text));
        file.close();
    }
    return 0;
}
```

## 3.3 Stream Formatting

Stream formatting involves controlling the appearance of the data being input or output.

### 3.3.1 Manipulators

C++ provides several manipulators to format data in streams.

#### `std::setw`

Sets the width of the next input/output field.

```cpp
#include <iostream>
#include <iomanip>

int main() {
    int number = 42;
    std::cout << "Number with width 10: " << std::setw(10) << number << std::endl;
    return 0;
}
```

#### `std::setprecision`

Sets the decimal precision of floating-point numbers.

```cpp
#include <iostream>
#include <iomanip>

int main() {
    double number = 3.14159;
    std::cout << "Number with precision 3: " << std::setprecision(3) << number << std::endl;
    return 0;
}
```

#### `std::fixed` and `std::scientific`

Control the format of floating-point output.

```cpp
#include <iostream>
#include <iomanip>

int main() {
    double number = 12345.6789;
    std::cout << "Fixed: " << std::fixed << number << std::endl;
    std::cout << "Scientific: " << std::scientific << number << std::endl;
    return 0;
}
```

### 3.3.2 Flags

Flags are used to control various formatting options in streams.

#### `std::boolalpha` and `std::noboolalpha`

Control the formatting of boolean values.

```cpp
#include <iostream>

int main() {
    bool flag = true;
    std::cout << "Default: " << flag << std::endl;
    std::cout << std::boolalpha << "Boolalpha: " << flag << std::endl;
    std::cout << std::noboolalpha << "Noboolalpha: " << flag << std::endl;
    return 0;
}
```

#### `std::showbase` and `std::noshowbase`

Control the display of the base of integral values.

```cpp
#include <iostream>
#include <iomanip>

int main() {
    int number = 42;
    std::cout << "Default: " << number << std::endl;
    std::cout << std::showbase << std::hex << "Hex with base: " << number << std::endl;
    std::cout << std::noshowbase << "Hex without base: " << number << std::endl;
    return 0;
}
```

## 3.4 Error Handling

Handling errors in streams ensures robust and reliable input and output operations.

### 3.4.1 Checking Stream States

Streams have various states to indicate their status: `good`, `eof`, `fail`, and `bad`.

```cpp
#include <iostream>

int main() {
    std::cin.clear(); // Clear any error flags
    if (std::cin.fail()) {
        std::cerr << "Input failed!" << std::endl;
    }
    return 0;
}
```

### 3.4.2 Clearing Errors

Clearing errors allows you to reset the state of a stream after an error occurs.

```cpp
#include <iostream>

int main() {
    int number;
    std::cin >> number;
    if (std::cin.fail()) {
        std::cin.clear(); // Clear the error flag
        std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n'); // Ignore the invalid input
        std::cout << "Please enter a valid number: ";
        std::cin >> number;
    }
    std::cout << "You entered: " << number << std::endl;
    return 0;
}
```

## 3.5 Stream Buffers

Stream buffers manage the internal memory of streams and control the flow of data.

### 3.5.1 Custom Stream Buffers

You can create custom stream buffers by deriving from `std::streambuf`.

```cpp
#include <iostream>
#include <streambuf>

class MyStreamBuf : public std::streambuf {
protected:
    virtual int overflow(int c) override {
        if (c != EOF) {
            c = std::toupper(c);
            std::cout.put(c);
        }
        return c;
    }
};

int main() {
    MyStreamBuf buf;
    std::ostream out(&buf);
    out << "Hello, custom stream buffer!" << std::endl;
    return 0;
}
```

Understanding these stream operations allows you to effectively manage input and output in your C++ programs. Mastery of these concepts leads to the development of robust and efficient applications that can handle various data sources and formats with ease.