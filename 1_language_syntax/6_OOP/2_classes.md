
# Classes

In C++, a class is a user-defined data type that represents a blueprint for creating objects. Classes encapsulate data for the object and methods to manipulate that data. They are fundamental to [[3_OOP|object-oriented programming (OOP)]] and provide a means of combining data and functions that operate on that data.

## Syntax

The basic syntax for defining a class is as follows:

```cpp
class ClassName {
public:
    // Public member variables and methods
    DataType1 variable1;
    void memberFunction1();

protected:
    // Protected member variables and methods
    DataType2 variable2;

private:
    // Private member variables and methods
    DataType3 variable3;
};
```

## Example

```cpp
#include <iostream>
#include <string>

class Person {
public:
    // Constructor
    Person(const std::string& name, int age, double height) 
        : name(name), age(age), height(height) {}

    // Member function to display details
    void display() const {
        std::cout << "Name: " << name << "\nAge: " << age << "\nHeight: " << height << " meters" << std::endl;
    }

private:
    std::string name;
    int age;
    double height;
};

int main() {
    Person p1("John Doe", 30, 1.75);
    p1.display();
    return 0;
}
```

## Key Concepts

### Encapsulation

Encapsulation is the bundling of data and methods that operate on that data within a single unit, the class. It restricts direct access to some of the object’s components, which is a means of preventing accidental interference and misuse of the data.

### Access Specifiers

- **public**: Members are accessible from outside the class.
- **protected**: Members are accessible within the class and by derived class instances.
- **private**: Members are accessible only within the class itself.

### Constructors and Destructors

- **Constructors**: Special member functions that are called when an object is instantiated. They initialize the object's members.
- **Destructors**: Special member functions that are called when an object goes out of scope or is explicitly deleted. They clean up resources allocated by the object.

### Example with Constructor and Destructor

```cpp
class Rectangle {
public:
    // Constructor
    Rectangle(double length, double width) : length(length), width(width) {}

    // Destructor
    ~Rectangle() {
        // Cleanup code if needed
    }

    double area() const {
        return length * width;
    }

private:
    double length;
    double width;
};
```

### Member Functions

Member functions are functions that are declared within a class. They can operate on the data members of the class.

```cpp
class Circle {
public:
    Circle(double radius) : radius(radius) {}

    double area() const {
        return 3.14159 * radius * radius;
    }

private:
    double radius;
};
```

## Advanced Concepts

### Inheritance

Inheritance is a mechanism by which one class (derived class) can inherit properties and behaviors (methods) from another class (base class).

```cpp
class Animal {
public:
    void eat() {
        std::cout << "Eating..." << std::endl;
    }
};

class Dog : public Animal {
public:
    void bark() {
        std::cout << "Barking..." << std::endl;
    }
};
```

### Polymorphism

Polymorphism allows methods to do different things based on the object it is acting upon. It is usually implemented via virtual functions.

```cpp
class Shape {
public:
    virtual void draw() const {
        std::cout << "Drawing Shape" << std::endl;
    }
};

class Circle : public Shape {
public:
    void draw() const override {
        std::cout << "Drawing Circle" << std::endl;
    }
};

class Square : public Shape {
public:
    void draw() const override {
        std::cout << "Drawing Square" << std::endl;
    }
};
```

### Operator Overloading

Classes can overload operators to provide intuitive interactions with user-defined types.

```cpp
class Complex {
public:
    Complex(double real, double imag) : real(real), imag(imag) {}

    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }

private:
    double real;
    double imag;
};
```

### Copy and Move Semantics

Copy and move semantics are essential for managing resource ownership in C++.

## Copy Semantics

Copy semantics involve making a copy of an object. This is typically used when you need a new object with the same value as an existing one.

### Copy Constructor

A copy constructor initializes a new object as a copy of an existing object.

```cpp
class Resource {
public:
    int* data;
    
    // Constructor
    Resource(int value) : data(new int(value)) {}

    // Copy Constructor
    Resource(const Resource& other) : data(new int(*other.data)) {
        std::cout << "Copy Constructor Called" << std::endl;
    }

    ~Resource() {
        delete data;
    }
};

int main() {
    Resource res1(10);
    Resource res2 = res1; // Copy constructor is called
    return 0;
}
```

### Copy Assignment Operator

The copy assignment operator assigns the contents of an existing object to another existing object.

```cpp
class Resource {
public:
    int* data;

    Resource(int value) : data(new int(value)) {}

    Resource(const Resource& other) : data(new int(*other.data)) {
        std::cout << "Copy Constructor Called" << std::endl;
    }

    Resource& operator=(const Resource& other) {
        if (this != &other) {
            delete data;
            data = new int(*other.data);
        }
        std::cout << "Copy Assignment Operator Called" << std::endl;
        return *this;
    }

    ~Resource() {
        delete data;
    }
};

int main() {
    Resource res1(10);
    Resource res2(20);
    res2 = res1; // Copy assignment operator is called
    return 0;
}
```

## Move Semantics

Move semantics involve transferring ownership of resources from one object to another, instead of copying. This is useful for optimizing performance, particularly with objects that manage dynamic memory or other resources.

### Move Constructor

A move constructor transfers resources from a temporary object to a new object.

```cpp
class Resource {
public:
    int* data;

    Resource(int value) : data(new int(value)) {}

    Resource(Resource&& other) noexcept : data(other.data) {
        other.data = nullptr;
        std::cout << "Move Constructor Called" << std::endl;
    }

    ~Resource() {
        delete data;
    }
};

int main() {
    Resource res1(10);
    Resource res2 = std::move(res1); // Move constructor is called
    return 0;
}
```

### Move Assignment Operator

The move assignment operator transfers resources from a temporary object to an existing object.

```cpp
class Resource {
public:
    int* data;

    Resource(int value) : data(new int(value)) {}

    Resource(Resource&& other) noexcept : data(other.data) {
        other.data = nullptr;
        std::cout << "Move Constructor Called" << std::endl;
    }

    Resource& operator=(Resource&& other) noexcept {
        if (this != &other) {
            delete data;
            data = other.data;
            other.data = nullptr;
        }
        std::cout << "Move Assignment Operator Called" << std::endl;
        return *this;
    }

    ~Resource() {
        delete data;
    }
};

int main() {
    Resource res1(10);
    Resource res2(20);
    res2 = std::move(res1); // Move assignment operator is called
    return 0;
}
```

## Best Practices

1. **Encapsulation**: Keep data members private and expose them through public methods.
2. **Const Correctness**: Use `const` where applicable to indicate immutability.
3. **Use Initialization Lists**: Prefer initialization lists in constructors for better performance.
4. **Resource Management**: Use RAII (Resource Acquisition Is Initialization) to manage resources.
5. **Avoid Raw Pointers**: Use smart pointers (`std::unique_ptr`, `std::shared_ptr`) to manage dynamic memory.
6. **Use Move Semantics**: Leverage move semantics to optimize performance, especially in classes managing resources.

## Conclusion

Classes in C++ are the building blocks of object-oriented programming, providing a powerful mechanism to encapsulate data and functionality. Understanding and effectively utilizing classes is essential for creating robust, maintainable, and efficient software. Advanced concepts like inheritance, polymorphism, operator overloading, and proper resource management enable developers to write sophisticated and high-performing applications.