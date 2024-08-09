# File IO

File I/O (Input/Output) in C++ is handled through file streams, which allow you to read from and write to files. The C++ Standard Library provides the `<fstream>` header, which includes classes for file stream operations.

## File Stream Classes

### `std::ifstream`

Used for reading from files.

```cpp
#include <fstream>
#include <iostream>

int main() {
    std::ifstream inputFile("example.txt");
    if (inputFile.is_open()) {
        std::string line;
        while (std::getline(inputFile, line)) {
            std::cout << line << std::endl;
        }
        inputFile.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }
    return 0;
}
```

### `std::ofstream`

Used for writing to files.

```cpp
#include <fstream>

int main() {
    std::ofstream outputFile("example.txt");
    if (outputFile.is_open()) {
        outputFile << "Hello, World!" << std::endl;
        outputFile.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }
    return 0;
}
```

### `std::fstream`

Used for both reading from and writing to files.

```cpp
#include <fstream>
#include <iostream>

int main() {
    std::fstream file("example.txt", std::ios::in | std::ios::out | std::ios::app);
    if (file.is_open()) {
        file << "Appending this line." << std::endl;

        file.seekg(0, std::ios::beg); // Go to the beginning of the file
        std::string line;
        while (std::getline(file, line)) {
            std::cout << line << std::endl;
        }
        file.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }
    return 0;
}
```

## File Open Modes

File streams can be opened in various modes, defined by the `std::ios` flags:

- `std::ios::in` - Open for input operations.
- `std::ios::out` - Open for output operations.
- `std::ios::binary` - Open in binary mode.
- `std::ios::ate` - Open and seek to the end of the file.
- `std::ios::app` - Open for output and append to the end of the file.
- `std::ios::trunc` - If the file is opened for output, the file is truncated.

### Example of Opening a File in Different Modes

```cpp
#include <fstream>

int main() {
    std::ofstream outputFile("example.txt", std::ios::out | std::ios::app);
    if (outputFile.is_open()) {
        outputFile << "Appending this line." << std::endl;
        outputFile.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }
    return 0;
}
```

## Checking File State

After performing file operations, you should check the state of the file stream using various member functions:

- `bool good()` - Returns `true` if no errors have occurred.
- `bool eof()` - Returns `true` if the end-of-file has been reached.
- `bool fail()` - Returns `true` if a logical error occurs.
- `bool bad()` - Returns `true` if a read/write error occurs.

### Example of Checking File State

```cpp
#include <fstream>
#include <iostream>

int main() {
    std::ifstream inputFile("example.txt");
    if (inputFile.is_open()) {
        std::string line;
        while (std::getline(inputFile, line)) {
            std::cout << line << std::endl;
        }
        if (inputFile.eof()) {
            std::cout << "End of file reached" << std::endl;
        }
        if (inputFile.fail()) {
            std::cerr << "Logical error on input operation" << std::endl;
        }
        if (inputFile.bad()) {
            std::cerr << "Read/writing error on input operation" << std::endl;
        }
        inputFile.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }
    return 0;
}
```

## Reading and Writing Binary Files

To read and write binary files, you need to open the file in binary mode using the `std::ios::binary` flag.

### Example of Writing to a Binary File

```cpp
#include <fstream>

int main() {
    std::ofstream outputFile("binary.dat", std::ios::binary);
    if (outputFile.is_open()) {
        int number = 12345;
        outputFile.write(reinterpret_cast<char*>(&number), sizeof(number));
        outputFile.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }
    return 0;
}
```

### Example of Reading from a Binary File

```cpp
#include <fstream>
#include <iostream>

int main() {
    std::ifstream inputFile("binary.dat", std::ios::binary);
    if (inputFile.is_open()) {
        int number;
        inputFile.read(reinterpret_cast<char*>(&number), sizeof(number));
        std::cout << "Read number: " << number << std::endl;
        inputFile.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }
    return 0;
}
```

## Handling File Paths

Since C++17, the `<filesystem>` library provides support for handling file paths in a more portable and convenient way.

### Example Using `std::filesystem`

```cpp
#include <fstream>
#include <iostream>
#include <filesystem>

namespace fs = std::filesystem;

int main() {
    fs::path filePath = "example.txt";

    // Check if the file exists
    if (fs::exists(filePath)) {
        std::cout << "File exists." << std::endl;
    } else {
        std::cerr << "File does not exist." << std::endl;
    }

    // Open file for writing
    std::ofstream outputFile(filePath);
    if (outputFile.is_open()) {
        outputFile << "Hello, Filesystem!" << std::endl;
        outputFile.close();
    } else {
        std::cerr << "Unable to open file" << std::endl;
    }

    return 0;
}
```

File I/O in C++ provides robust functionality for handling file operations, whether reading from or writing to text or binary files, and helps ensure that files are managed efficiently and correctly within your programs.