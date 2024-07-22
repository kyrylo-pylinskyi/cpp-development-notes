# Structures

In C++, a structure (`struct`) is a user-defined data type that groups together variables of different data types under a single name. While similar to classes, structures have some distinct characteristics and historical usage differences, particularly from C.

## Syntax

The syntax for defining a structure is straightforward:

```cpp
struct StructureName {
    // Member variables
    DataType1 variable1;
    DataType2 variable2;
    // ... more variables
};
```

## Example

```cpp
#include <iostream>
#include <string>

struct Person {
    std::string name;
    int age;
    double height;

    // Member function to display details
    void display() const {
        std::cout << "Name: " << name << "\nAge: " << age << "\nHeight: " << height << " meters" << std::endl;
    }
};

int main() {
    Person p1 = {"John Doe", 30, 1.75};
    p1.display();
    return 0;
}
```

## Differences Between Structures and Classes

- **Default Access Specifier**: In a structure, members are public by default, whereas in a [[2_classes|class]], members are private by default.
- **Use Cases**: Structures are traditionally used for passive objects with public access to data, while classes are used for active objects with private data and public member functions.

## Advanced Usage

### Member Functions

Structures can have member functions, just like classes:

```cpp
struct Vector {
    float x, y;

    void add(const Vector& other) {
        x += other.x;
        y += other.y;
    }
};
```

### Constructors and Destructors

Structures can have constructors and destructors to initialize and clean up resources:

```cpp
struct Point {
    int x, y;

    // Constructor
    Point(int xCoord, int yCoord) : x(xCoord), y(yCoord) {}

    // Destructor
    ~Point() {
        // Clean up code (if needed)
    }
};
```

### Operator Overloading

Structures can overload operators to define custom behavior for operators such as `+`, `-`, `==`, etc.:

```cpp
struct Complex {
    double real, imag;

    Complex operator+(const Complex& other) const {
        return {real + other.real, imag + other.imag};
    }
};
```

### Inheritance

Although not common, structures can be used in inheritance hierarchies:

```cpp
struct Base {
    int id;
};

struct Derived : public Base {
    std::string name;
};
```

### Usage with Standard Library

Structures can be used effectively with the C++ Standard Library, especially with templates:

```cpp
#include <vector>
#include <algorithm>

struct Data {
    int key;
    double value;
};

int main() {
    std::vector<Data> dataList = {{1, 2.5}, {2, 3.5}, {3, 4.5}};
    std::sort(dataList.begin(), dataList.end(), [](const Data& a, const Data& b) {
        return a.key < b.key;
    });
    return 0;
}
```

### Best Practices

1. **Encapsulation**: Even though structures default to public access, consider using access specifiers to encapsulate data.
2. **Initialization**: Use constructors to ensure members are initialized properly.
3. **Const Correctness**: Use `const` where applicable to ensure member functions do not modify the object.
4. **Pass by Reference**: Pass structures by reference to functions to avoid unnecessary copying.

### Conclusion

Structures in C++ provide a flexible and powerful way to group related variables. Understanding the nuances of structures, especially in relation to classes, allows for more effective and efficient programming. By leveraging advanced features like member functions, constructors, destructors, and operator overloading, you can create robust and maintainable code.