# Abstract Classes and Interfaces

Abstract classes and interfaces are fundamental concepts in object-oriented programming (OOP) that allow for the design of flexible and reusable software. In C++, these concepts are implemented using pure virtual functions and inheritance.

## Abstract Classes

An abstract class is a class that cannot be instantiated on its own and is designed to be a base class for other classes. It typically contains one or more pure virtual functions. A pure virtual function is a function that has no implementation in the abstract class and must be overridden by derived classes.

### Defining an Abstract Class

To define an abstract class, you declare one or more functions as pure virtual functions using the `= 0` syntax.

```cpp
class Animal {
private:
	std::string _name;
public:
	Animal(const std::sting& name) : _name(name)
    virtual void makeSound() = 0; // Pure virtual function
    virtual std::string getName() inline { return _name; }
    virtual ~AbstractBase() = default; // Virtual destructor
};
```

In this example, `pureVirtualFunction` is a pure virtual function, making `AbstractBase` an abstract class. The `normalVirtualFunction` is a virtual function with an implementation, and it can optionally be overridden by derived classes.

### Deriving from an Abstract Class

Derived classes must override all pure virtual functions of the base abstract class to be instantiable.

```cpp
class Dog : public Animal {
public:
    void makeSound() override {
        std::cout << "Bark!" << std::endl;
    }
};

int main() {
    Animal abstarctAnimal; // Error: Cannot instantiate an abstract class
    Dog dog;
    dog.makeSound(); // Output: Implementation of pure virtual function in Derived.
    std::cout << dog.getName() << std::endl; // This is a virtual function with                                                      // implementation in AbstractBase.
    return 0;
}
```

In this example, `Derived` provides an implementation for the `pureVirtualFunction`, allowing it to be instantiated.

## Interfaces

In C++, interfaces are typically represented by abstract classes that contain only pure virtual functions and no data members or implemented functions. This is different from languages like Java or C# that have explicit `interface` keywords.

### Defining an Interface

An interface in C++ is simply an abstract class with only pure virtual functions.

```cpp
class IAnimal {
public:
    virtual void makeSound() = 0;
    virtual void jump() = 0;
    virtual ~IAnimal() = default;
};
```

### Implementing an Interface

A class that implements an interface must provide implementations for all the pure virtual functions defined in the interface.

```cpp
class Wolf : public IAnimal {
public:
    void makeSound() override {
        std::cout << "Woof!" << std::endl;
    }

    void jump() override {
        std::cout << "Wolf jump" << std::endl;
    }
};

int main() {
    IAnimal* wolf = new Wolf();
    wolf->makeSound(); // Output: Woof!
    wolf->jump(); // Output: Wolf jump
    return 0;
}
```

### Multiple Inheritance with Interfaces

One of the powerful features of interfaces is that a class can implement multiple interfaces, allowing for flexible and modular design.

```cpp
class IPet {
public:
    virtual void feed(const std::string& food) = 0;
    virtual ~IPet() = default;
};

class Dog : public IAnimal, public IPet {
public:
    void makeSound() override {
        std::cout << "Bark!" << std::endl;
    }

    void jump() override {
        std::cout << "Dog jump" << std::endl;
    }

    void feed(const std::string& food) override {
        std::cout << "Feeding the dog " << food << std::endl;
    }
};

int main() {
    Dog dog;
    dog.makeSound();    // Output: Bark!
    dog.jump();         // Output: Dog jump
    dog.feed("Sousage") // Output: Feeding the dog Sousage
    return 0;
}
```

### Summary

- **Abstract Classes**: Used to provide a common interface for derived classes, including some common behavior. They can contain both pure virtual functions (forcing derived classes to implement them) and non-virtual functions.
- **Interfaces**: Special kinds of abstract classes that contain only pure virtual functions, forcing any implementing class to provide all the required functionality. This approach allows for multiple inheritance without the complexities associated with regular multiple inheritance.

Abstract classes and interfaces are key tools in C++ for achieving polymorphism, code reuse, and flexible design patterns. By leveraging these concepts, you can design robust and maintainable software systems.