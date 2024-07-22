# Dynamic Polymorphism

Dynamic polymorphism, also known as runtime polymorphism, is a core concept in object-oriented programming that allows a program to decide which method to execute at runtime rather than compile time. This is primarily achieved through the use of [[7_virtual_methods|virtual methods]] and inheritance in C++.

## Key Concepts

### Virtual Methods

A [[7_virtual_methods|virtual methods]] is a member methods in a base class that you expect to override in derived classes. When you use a base class pointer or reference to point to a derived class object, the call to the virtual method will invoke the derived class's implementation.

#### Example:

```cpp
#include <iostream>

class Base {
public:
    virtual void show() {
        std::cout << "Base class show method called." << std::endl;
    }

    virtual ~Base() {} // Virtual destructor
};

class Derived : public Base {
public:
    void show() override {
        std::cout << "Derived class show method called." << std::endl;
    }
};

int main() {
    Base* b = new Derived();
    b->show(); // Calls Derived's show()
    delete b;
    return 0;
}
```

### The Role of Pointers and References

Dynamic polymorphism typically relies on pointers or references to base class types. This allows you to invoke derived class methods even when using base class references or pointers.

#### Example:

```cpp
#include <iostream>

class Shape {
public:
    virtual void draw() {
        std::cout << "Drawing a shape." << std::endl;
    }
};

class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a circle." << std::endl;
    }
};

class Square : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a square." << std::endl;
    }
};

void renderShape(Shape* shape) {
    shape->draw(); // Calls the appropriate draw method at runtime
}

int main() {
    Shape* circle = new Circle();
    Shape* square = new Square();

    renderShape(circle); // Output: Drawing a circle.
    renderShape(square); // Output: Drawing a square.
    return 0;
}
```

### Virtual Destructors

To ensure proper cleanup of derived class resources, base classes that declare virtual functions should also declare a virtual destructor. This ensures that the derived class's destructor is called when an object is deleted through a base class pointer.

#### Example:

```cpp
#include <iostream>

class Base {
public:
    virtual ~Base() {
        std::cout << "Base destructor called." << std::endl;
    }
};

class Derived : public Base {
public:
    ~Derived() {
        std::cout << "Derived destructor called." << std::endl;
    }
};

int main() {
    Base* b = new Derived();
    delete b; // Calls Derived's destructor, then Base's destructor
    return 0;
}
```

## Advantages of Dynamic Polymorphism

1. **Flexibility**: Allows for flexible and extensible code. You can introduce new derived classes without modifying existing code.
2. **Code Reusability**: Promotes the use of base class interfaces, enabling code to work with any derived class.
3. **Loose Coupling**: Reduces dependencies between components, making the code easier to maintain and modify.

## Disadvantages of Dynamic Polymorphism

1. **Performance Overhead**: Virtual function calls have a slight overhead compared to non-virtual calls due to the additional level of indirection.
2. **Complexity**: Increases complexity due to the need for careful design of class hierarchies and interfaces.

## Use Cases

### Shape Hierarchy

Dynamic polymorphism is often used in graphic applications where different shapes are handled uniformly through a base class.

```cpp
#include <iostream>
#include <vector>

class Shape {
public:
    virtual void draw() = 0; // Pure virtual function
};

class Circle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a circle." << std::endl;
    }
};

class Square : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a square." << std::endl;
    }
};

void drawShapes(const std::vector<Shape*>& shapes) {
    for (const auto& shape : shapes) {
        shape->draw(); // Calls the appropriate draw method
    }
}

int main() {
    Shape* circle = new Circle();
    Shape* square = new Square();
    std::vector<Shape*> shapes = { circle, square };

    drawShapes(shapes); // Output: Drawing a circle. Drawing a square.
    return 0;
}
```

## Conclusion

Dynamic polymorphism is a powerful feature of C++ that enhances the flexibility and maintainability of code. By leveraging virtual functions and inheritance, developers can create robust applications that can easily accommodate future changes and extensions. Understanding dynamic polymorphism is crucial for designing effective object-oriented systems in C++.