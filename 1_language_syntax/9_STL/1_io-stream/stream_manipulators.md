# Stream Manipulators

Stream manipulators in C++ allow you to control the formatting and behavior of input and output streams. They can be used to adjust field widths, set precision, control the display of numbers, and manage other formatting tasks. These manipulators are part of the `<iomanip>` library.

## Common Stream Manipulators

### `std::endl`

Inserts a newline character and flushes the output buffer.

```cpp
std::cout << "Hello, World!" << std::endl;
```

### `std::setw`

Sets the width of the next input/output field.

```cpp
std::cout << std::setw(10) << 123 << std::endl;
```

### `std::setprecision`

Sets the decimal precision for floating-point values.

```cpp
std::cout << std::setprecision(3) << 3.14159 << std::endl; // Output: 3.14
```

### `std::fixed` and `std::scientific`

Forces floating-point output to be in fixed-point notation or scientific notation.

```cpp
std::cout << std::fixed << 3.14159 << std::endl;     // Output: 3.141590
std::cout << std::scientific << 3.14159 << std::endl; // Output: 3.141590e+00
```

### `std::setfill`

Sets the fill character used for padding.

```cpp
std::cout << std::setfill('*') << std::setw(10) << 123 << std::endl; // Output: *******123
```

### `std::left` and `std::right`

Aligns output to the left or right.

```cpp
std::cout << std::left << std::setw(10) << 123 << std::endl;  // Output: 123       
std::cout << std::right << std::setw(10) << 123 << std::endl; // Output:       123
```

### `std::boolalpha` and `std::noboolalpha`

Controls the representation of boolean values.

```cpp
std::cout << std::boolalpha << true << std::endl;  // Output: true
std::cout << std::noboolalpha << true << std::endl; // Output: 1
```

### `std::showbase` and `std::noshowbase`

Controls the display of the numeric base prefix (0 for octal, 0x for hexadecimal).

```cpp
std::cout << std::showbase << std::hex << 255 << std::endl; // Output: 0xff
std::cout << std::noshowbase << std::hex << 255 << std::endl; // Output: ff
```

### `std::uppercase` and `std::nouppercase`

Controls the case of hexadecimal digits and scientific notation.

```cpp
std::cout << std::uppercase << std::hex << 255 << std::endl; // Output: FF
std::cout << std::nouppercase << std::hex << 255 << std::endl; // Output: ff
```

## Custom Stream Manipulators

You can define your own stream manipulators to perform custom formatting.

### Creating a Custom Manipulator

A custom manipulator can be created by defining a function that takes a stream reference and performs the desired operation.

```cpp
#include <iostream>
#include <iomanip>

// Custom manipulator to reset the stream formatting
std::ostream& reset(std::ostream& os) {
    os.copyfmt(std::ios(NULL));
    return os;
}

int main() {
    std::cout << std::setw(10) << 123 << std::endl; // Output:        123
    std::cout << reset << 123 << std::endl;        // Output: 123 (without width formatting)
    return 0;
}
```

### Using Custom Manipulators

Custom manipulators are used in the same way as standard manipulators.

```cpp
std::cout << customManipulator << someData;
```

Stream manipulators are a powerful tool in C++ for controlling the format and behavior of I/O operations, making it easier to produce well-formatted and readable output.