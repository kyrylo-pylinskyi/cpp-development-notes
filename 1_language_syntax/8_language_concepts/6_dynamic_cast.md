# `dynamic_cast` in C++

`dynamic_cast` is a type casting operator used in C++ to safely convert pointers and references to classes up, down, and sideways along the inheritance hierarchy. It is primarily used for safe downcasting, where you convert a base class pointer to a derived class pointer. Unlike `static_cast`, `dynamic_cast` includes runtime type checking to ensure that the cast is valid.

## Usage

### Basic Syntax

```cpp
dynamic_cast<new_type>(expression)
```

Where `new_type` is the target type you want to convert to, and `expression` is the pointer or reference you are converting.

### Example

#### Safe Downcasting

```cpp
class Base {
public:
    virtual void show() { std::cout << "Base" << std::endl; }
};

class Derived : public Base {
public:
    void show() override { std::cout << "Derived" << std::endl; }
};

int main() {
    Base* basePtr = new Derived();
    Derived* derivedPtr = dynamic_cast<Derived*>(basePtr);
    if (derivedPtr) {
        derivedPtr->show(); // Output: Derived
    } else {
        std::cout << "Cast failed" << std::endl;
    }
    delete basePtr;
    return 0;
}
```

### Use Cases

#### 1. Safe Downcasting in Inheritance Hierarchies

`dynamic_cast` is primarily used for safely downcasting from a base class pointer to a derived class pointer.

```cpp
Base* basePtr = new Derived();
Derived* derivedPtr = dynamic_cast<Derived*>(basePtr);
if (derivedPtr) {
    derivedPtr->show(); // Output: Derived
}
```

#### 2. Checking Object Type at Runtime

`dynamic_cast` can be used to check the actual type of an object at runtime, ensuring that the cast is safe and valid.

```cpp
void processBase(Base* basePtr) {
    if (Derived* derivedPtr = dynamic_cast<Derived*>(basePtr)) {
        derivedPtr->specialFunction();
    } else {
        std::cout << "Not a Derived object" << std::endl;
    }
}
```

### Limitations and Safety

- **Requires Polymorphic Base Classes**: The base class must have at least one virtual function to use `dynamic_cast`. This ensures that the object has a runtime type information (RTTI) that `dynamic_cast` can check.

```cpp
class NonPolymorphic {
public:
    void show() { std::cout << "NonPolymorphic" << std::endl; }
};

NonPolymorphic* npPtr = new NonPolymorphic();
Derived* derivedPtr = dynamic_cast<Derived*>(npPtr); // Error: Cannot dynamic_cast 'npPtr' (of type 'class NonPolymorphic*') to type 'class Derived*' (target is not pointer or reference to a polymorphic type)
```

- **Null Pointer Result**: When casting pointers, if the cast is not valid, `dynamic_cast` returns a `nullptr`.

```cpp
Base* basePtr = new Base();
Derived* derivedPtr = dynamic_cast<Derived*>(basePtr);
if (derivedPtr == nullptr) {
    std::cout << "Cast failed" << std::endl; // Output: Cast failed
}
delete basePtr;
```

- **Throws Exception for References**: When casting references, if the cast is not valid, `dynamic_cast` throws a `std::bad_cast` exception.

```cpp
try {
    Base base;
    Derived& derivedRef = dynamic_cast<Derived&>(base);
} catch (const std::bad_cast& e) {
    std::cout << "Bad cast: " << e.what() << std::endl; // Output: Bad cast: std::bad_cast
}
```

### Summary

`dynamic_cast` is a powerful and safe casting operator in C++ that should be used for:

1. **Safe Downcasting**: Ensuring that the conversion from a base class pointer to a derived class pointer is valid at runtime.
2. **Runtime Type Checking**: Verifying the actual type of an object during runtime.

By using `dynamic_cast`, you can avoid unsafe type conversions and potential undefined behavior, making your C++ code more robust and maintainable.