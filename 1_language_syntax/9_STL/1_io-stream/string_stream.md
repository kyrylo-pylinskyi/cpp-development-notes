# String Streams

String streams in C++ are a part of the `<sstream>` header and are used to perform input and output operations on `std::string` objects. They provide a convenient way to work with strings as if they were streams, allowing for easy conversion and manipulation of string data.

## Basic Classes

### `std::stringstream`

A stream class to operate on strings. It allows both input and output operations on a string.

### `std::istringstream`

A stream class for input operations on strings. It is used to read from strings like you would read from other input streams (e.g., `std::cin`).

### `std::ostringstream`

A stream class for output operations on strings. It is used to write to strings like you would write to other output streams (e.g., `std::cout`).

## Examples

### Using `std::stringstream`

```cpp
#include <sstream>
#include <iostream>

int main() {
    std::stringstream ss;

    ss << "Hello, ";
    ss << "world!";
    
    std::string result = ss.str();
    std::cout << result << std::endl; // Output: Hello, world!
    
    return 0;
}
```

### Using `std::istringstream`

```cpp
#include <sstream>
#include <iostream>

int main() {
    std::string data = "123 45.67 example";
    std::istringstream iss(data);

    int i;
    float f;
    std::string s;
    
    iss >> i >> f >> s;
    
    std::cout << "Integer: " << i << std::endl;    // Output: Integer: 123
    std::cout << "Float: " << f << std::endl;      // Output: Float: 45.67
    std::cout << "String: " << s << std::endl;     // Output: String: example
    
    return 0;
}
```

### Using `std::ostringstream`

```cpp
#include <sstream>
#include <iostream>

int main() {
    std::ostringstream oss;
    
    int i = 123;
    float f = 45.67;
    std::string s = "example";
    
    oss << i << " " << f << " " << s;
    
    std::string result = oss.str();
    std::cout << result << std::endl; // Output: 123 45.67 example
    
    return 0;
}
```

## Practical Use Cases

### Converting Between Types

String streams are often used for type conversions between strings and other data types.

#### String to Number

```cpp
#include <sstream>
#include <iostream>

int main() {
    std::string numberString = "42";
    int number;
    
    std::istringstream(numberString) >> number;
    
    std::cout << "Converted number: " << number << std::endl; // Output: Converted number: 42
    
    return 0;
}
```

#### Number to String

```cpp
#include <sstream>
#include <iostream>

int main() {
    int number = 42;
    std::ostringstream oss;
    
    oss << number;
    std::string numberString = oss.str();
    
    std::cout << "Converted string: " << numberString << std::endl; // Output: Converted string: 42
    
    return 0;
}
```

### Parsing Complex Strings

String streams can be used to parse and extract data from complex string formats.

```cpp
#include <sstream>
#include <iostream>

int main() {
    std::string data = "Name: John, Age: 30, Country: USA";
    std::istringstream iss(data);

    std::string name;
    int age;
    std::string country;

    iss.ignore(6); // Ignore "Name: "
    iss >> name;
    iss.ignore(6); // Ignore ", Age: "
    iss >> age;
    iss.ignore(10); // Ignore ", Country: "
    iss >> country;

    std::cout << "Name: " << name << std::endl;
    std::cout << "Age: " << age << std::endl;
    std::cout << "Country: " << country << std::endl;

    return 0;
}
```

## Error Checking

As with other streams, you should check the state of string streams after operations to ensure they have succeeded.

```cpp
#include <sstream>
#include <iostream>

int main() {
    std::string data = "123 abc";
    std::istringstream iss(data);
    
    int i;
    iss >> i;
    
    if (iss.fail()) {
        std::cerr << "Error: Failed to convert string to integer." << std::endl;
    } else {
        std::cout << "Converted integer: " << i << std::endl; // Output: Converted integer: 123
    }
    
    return 0;
}
```

String streams provide a powerful and flexible way to manipulate and convert string data in C++. They are particularly useful for tasks such as type conversion, parsing, and formatting complex strings, making them an essential tool in a C++ programmer's toolkit.