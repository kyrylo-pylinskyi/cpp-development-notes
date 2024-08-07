
# RTTI (Runtime Type Information)

Runtime Type Information (RTTI) is a mechanism in C++ that provides information about the types of objects at runtime. RTTI is essential for working with polymorphism, particularly in scenarios involving base and derived class relationships.

## Key Concepts of RTTI

### 1. What is RTTI?

RTTI enables the identification of object types during execution, allowing programs to safely cast and manage polymorphic objects. This is particularly useful when you need to determine an object's actual type when working with base class pointers or references.

### 2. How RTTI Works

RTTI uses two primary features:

- **`typeid` Operator**: This operator retrieves the type information of an expression.
- **`dynamic_cast` Operator**: This operator safely casts pointers and references to base or derived classes.

### 3. Using `typeid`

The `typeid` operator can be used to obtain type information at runtime. It returns a reference to a `std::type_info` object.

#### Example

```cpp
#include <iostream>
#include <typeinfo>

class Base {
    virtual void dummy() {} // Need a virtual function for RTTI
};

class Derived : public Base {};

int main() {
    Base* b = new Derived();
    
    std::cout << "Type of b: " << typeid(*b).name() << std::endl; // Outputs Derived
    delete b;
    return 0;
}
```

### 4. Using `dynamic_cast`

`dynamic_cast` is used to safely cast pointers or references to base or derived classes. It returns a null pointer for failed casts when used with pointers, or throws a `std::bad_cast` exception when used with references.

#### Example

```cpp
#include <iostream>

class Base {
    virtual void dummy() {} // Necessary for RTTI
};

class Derived : public Base {};

int main() {
    Base* b = new Derived();

    // Safe downcast
    if (Derived* d = dynamic_cast<Derived*>(b)) {
        std::cout << "Successfully cast to Derived!" << std::endl;
    } else {
        std::cout << "Cast failed." << std::endl;
    }

    delete b;
    return 0;
}
```

### 5. Limitations of RTTI

- **Performance Overhead**: RTTI introduces some runtime overhead, which can affect performance in time-sensitive applications.
- **Not Available for Non-Polymorphic Types**: RTTI only works with classes that have at least one virtual function. Non-polymorphic types do not have RTTI.

### 6. Disabling RTTI

In some cases, you might want to disable RTTI to reduce the binary size or improve performance. This can be done using compiler options:

```bash
g++ -fno-rtti myfile.cpp
```

### 7. Practical Use Cases

RTTI is commonly used in:

- **Dynamic Object Handling**: In scenarios where the actual object type must be known at runtime.
- **Implementing Visitor Patterns**: When working with polymorphic class hierarchies.
- **Serialization and Deserialization**: To determine the type of objects being serialized or deserialized.

## Conclusion

RTTI is a powerful feature of C++ that enhances the language's support for polymorphism. By enabling safe type identification and dynamic casting, RTTI allows developers to write more flexible and robust code. However, it should be used judiciously due to potential performance implications and its reliance on polymorphism. Understanding RTTI is essential for effectively working with object-oriented programming in C++.