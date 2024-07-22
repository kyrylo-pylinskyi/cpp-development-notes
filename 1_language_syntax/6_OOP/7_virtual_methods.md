# Virtual Methods

Virtual methods are a fundamental concept in object-oriented programming, particularly in C++. They enable [[7_virtual_methods|dynamic polymorphism]], allowing derived classes to provide specific implementations of methods declared in a base class. This mechanism is essential for creating flexible and extensible code architectures.

## Key Concepts

### Definition

A **virtual method** is a member function declared in a base class that is intended to be overridden in derived classes. When called through a base class pointer or reference, the derived class's version of the method is executed, enabling dynamic behavior.

### Syntax

To declare a virtual method, use the `virtual` keyword in the base class:

```cpp
class Base {
public:
    virtual void show() {
        // Base class implementation
    }
};
```

### Example of Virtual Methods

Here's a simple example illustrating how virtual methods work:

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
    b->show(); // Calls Derived's show method
    delete b; // Proper cleanup due to virtual destructor
    return 0;
}
```

## Characteristics of Virtual Methods

### Late Binding

Virtual methods utilize **late binding** or **dynamic binding**, meaning the decision about which method to invoke is made at runtime based on the type of the object being pointed to, rather than the type of the pointer/reference.

### Virtual Table (VTable)

C++ implements virtual methods through a mechanism called the **[[9_VMT|virtual table]] (VTable)**. Each class with virtual methods has its own VTable, which holds pointers to the virtual methods of that class. When a virtual method is called, the corresponding pointer in the VTable is used to invoke the appropriate method.

### Virtual Destructors

To ensure proper resource cleanup, it's crucial to declare a destructor as virtual in the base class if it has virtual methods. This allows derived class destructors to be called when an object is deleted through a base class pointer.

```cpp
class Base {
public:
    virtual ~Base() {
        // Cleanup code
    }
};
```

## Advantages of Using Virtual Methods

1. **Flexibility**: Allows the implementation of interfaces that can be extended without modifying existing code.
2. **Polymorphism**: Supports dynamic polymorphism, enabling the use of base class references/pointers to invoke derived class methods.
3. **Loose Coupling**: Promotes loose coupling between components, making systems easier to manage and extend.

## Disadvantages of Using Virtual Methods

1. **Performance Overhead**: Virtual method calls incur a slight performance penalty due to the indirection involved in using the VTable.
2. **Increased Complexity**: The use of inheritance and virtual methods can complicate code design and understanding.

## Examples

### Overriding Virtual Methods

Derived classes can override virtual methods to provide specific functionality:

```cpp
class Animal {
public:
    virtual void sound() {
        std::cout << "Animal makes a sound." << std::endl;
    }
};

class Dog : public Animal {
public:
    void sound() override {
        std::cout << "Dog barks." << std::endl;
    }
};

class Cat : public Animal {
public:
    void sound() override {
        std::cout << "Cat meows." << std::endl;
    }
};

void makeSound(Animal* animal) {
    animal->sound(); // Calls the appropriate sound method
}
```

### Pure Virtual Methods

A pure virtual method is a virtual method that has no implementation in the base class and is declared by assigning `0` in its declaration. This makes the class [[10_abstract_classes_and_interfaces|abstract]], preventing instantiation.

```cpp
class AbstractShape {
public:
    virtual void draw() = 0; // Pure virtual method
};

class Circle : public AbstractShape {
public:
    void draw() override {
        std::cout << "Drawing a circle." << std::endl;
    }
};
```

### Example with Multiple Derived Classes

Using virtual methods allows handling various derived classes through a common base class interface:

```cpp
#include <iostream>
#include <vector>

class Shape {
public:
    virtual void draw() = 0; // Pure virtual function
};

class Triangle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a triangle." << std::endl;
    }
};

class Rectangle : public Shape {
public:
    void draw() override {
        std::cout << "Drawing a rectangle." << std::endl;
    }
};

void renderShapes(const std::vector<Shape*>& shapes) {
    for (const auto& shape : shapes) {
        shape->draw(); // Calls the appropriate draw method
    }
}

int main() {
    Triangle triangle;
    Rectangle rectangle;

    std::vector<Shape*> shapes = { &triangle, &rectangle };
    renderShapes(shapes); // Outputs the specific shapes being drawn
    return 0;
}
```

## Conclusion

Virtual methods are a cornerstone of object-oriented programming in C++, facilitating dynamic polymorphism and enhancing code flexibility and maintainability. Understanding how to effectively use virtual methods is essential for designing robust, extensible systems. By leveraging virtual methods and the underlying mechanisms, developers can create powerful applications that can adapt to changes with minimal effort.