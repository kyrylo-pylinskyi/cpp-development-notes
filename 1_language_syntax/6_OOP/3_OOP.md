# Object Oriented Programming

Object-Oriented Programming (OOP) is a paradigm in programming that emphasizes the use of objects and classes to structure software. This approach promotes code reusability, modularity, and scalability. C++ is a powerful language for OOP, providing rich features to implement and utilize this paradigm effectively.

## Core Concepts of OOP

### 1. Classes and Objects

**Classes** are blueprints for creating objects. They encapsulate data for the object and methods to manipulate that data.

**Objects** are instances of classes. They hold data and provide functionalities defined by the class.

### 2. Encapsulation

Encapsulation is the concept of bundling the data (variables) and the methods (functions) that operate on the data into a single unit, the class. It restricts direct access to some of the object's components, which is a means of preventing unintended interference and misuse of the data.

### 3. Inheritance

Inheritance allows a class to inherit properties and behavior from another class. The class that inherits is called the derived class, and the class from which it inherits is called the base class. Inheritance promotes code reusability and establishes a natural hierarchy between classes.

### 4. Polymorphism

Polymorphism means "many shapes" and it allows objects of different classes to be treated as objects of a common base class. There are two types of polymorphism in C++:

- **Compile-time Polymorphism (Static Binding)**: Achieved through function overloading and operator overloading.
- **Runtime Polymorphism (Dynamic Binding)**: Achieved through virtual functions.

### 5. Abstraction

Abstraction is the concept of hiding the complex implementation details and showing only the necessary features of an object. It helps to reduce complexity and increase efficiency.

## Detailed Concepts

### Classes and Objects

```cpp
class Car {
public:
    // Constructor
    Car(const std::string& model, int year) : model(model), year(year) {}

    // Method to display car details
    void display() const {
        std::cout << "Model: " << model << ", Year: " << year << std::endl;
    }

private:
    std::string model;
    int year;
};

int main() {
    Car car1("Toyota", 2020);
    car1.display();  // Output: Model: Toyota, Year: 2020
    return 0;
}
```

### Inheritance

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

int main() {
    Dog myDog;
    myDog.eat();  // Inherited method
    myDog.bark(); // Dog's own method
    return 0;
}
```

### Polymorphism

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

void drawShape(const Shape& shape) {
    shape.draw();
}

int main() {
    Circle circle;
    Square square;

    drawShape(circle); // Output: Drawing Circle
    drawShape(square); // Output: Drawing Square
    return 0;
}
```

### Abstraction

```cpp
class AbstractShape {
public:
    virtual void draw() const = 0; // Pure virtual function
};

class Triangle : public AbstractShape {
public:
    void draw() const override {
        std::cout << "Drawing Triangle" << std::endl;
    }
};

int main() {
    Triangle triangle;
    triangle.draw(); // Output: Drawing Triangle
    return 0;
}
```

## Advanced Topics

### Copy and Move Semantics

In modern C++, understanding copy and move semantics is essential, especially when dealing with resource management.

#### Copy Constructor and Copy Assignment Operator

```cpp
class Resource {
public:
    Resource(const std::string& name) : name(new std::string(name)) {}

    // Copy constructor
    Resource(const Resource& other) : name(new std::string(*other.name)) {}

    // Copy assignment operator
    Resource& operator=(const Resource& other) {
        if (this != &other) {
            delete name;
            name = new std::string(*other.name);
        }
        return *this;
    }

    ~Resource() {
        delete name;
    }

private:
    std::string* name;
};
```

#### Move Constructor and Move Assignment Operator

```cpp
class Resource {
public:
    Resource(const std::string& name) : name(new std::string(name)) {}

    // Move constructor
    Resource(Resource&& other) noexcept : name(other.name) {
        other.name = nullptr;
    }

    // Move assignment operator
    Resource& operator=(Resource&& other) noexcept {
        if (this != &other) {
            delete name;
            name = other.name;
            other.name = nullptr;
        }
        return *this;
    }

    ~Resource() {
        delete name;
    }

private:
    std::string* name;
};
```

### Rule of Zero, Three, and Five

- **Rule of Zero**: If a class does not manage resources, there is no need to define custom destructors, copy, or move operations.
- **Rule of Three**: If a class needs a custom destructor, copy constructor, or copy assignment operator, it likely needs all three.
- **Rule of Five**: If a class needs a custom destructor, copy constructor, copy assignment operator, move constructor, or move assignment operator, it likely needs all five.

### Multiple Inheritance and the Diamond Problem

C++ supports multiple inheritance, but it can introduce complexities such as the diamond problem. The diamond problem occurs when a class inherits from two classes that both inherit from a common base class. This leads to ambiguity and redundancy issues because the derived class will have two separate instances of the base class.

## The Diamond Problem Explained

Consider the following example without virtual inheritance:

```cpp
#include <iostream>

class A {
public:
    void display() {
        std::cout << "Class A" << std::endl;
    }
};

class B : public A {};
class C : public A {};
class D : public B, public C {};

int main() {
    D d;
    // d.display(); // This line will cause a compilation error due to ambiguity
    d.B::display(); // Output: Class A
    d.C::display(); // Output: Class A
    return 0;
}
```

### Ambiguity and Redundancy

In this example:

- `class D` inherits from both `class B` and `class C`.
- Both `class B` and `class C` inherit from `class A`.

Without virtual inheritance, `class D` ends up with two separate instances of `class A`, one through `class B` and one through `class C`. This creates ambiguity because the compiler doesn't know which `display` method to call. This ambiguity forces you to specify which path to take (`d.B::display()` or `d.C::display()`).

### Virtual inheritance

Virtual inheritance is a solution to this problem.

```cpp
class A {
public:
    void display() {
        std::cout << "Class A" << std::endl;
    }
};

class B : virtual public A {};

class C : virtual public A {};

class D : public B, public C {};

int main() {
    D d;
    d.display(); // Output: Class A
    return 0;
}
```

If you don't use virtual inheritance when dealing with multiple inheritance in C++, you can encounter the diamond problem.
## Conclusion

Object-Oriented Programming in C++ provides a robust framework for building complex software systems. Understanding the core concepts and advanced features of OOP allows developers to create efficient, maintainable, and scalable code. By mastering classes, inheritance, polymorphism, encapsulation, and other OOP principles, you can leverage the full power of C++ in your projects.