
# Dynamic Typing

Dynamic typing refers to a programming feature where variable types are determined at runtime rather than compile-time. In C++, while the language primarily supports static typing, certain features and paradigms allow for dynamic behavior. Understanding dynamic typing is crucial for implementing flexible and robust code.

## Key Concepts of Dynamic Typing

### 1. What is Dynamic Typing?

In dynamically typed languages, a variable can hold values of different types during execution. This allows for more flexibility but can lead to runtime errors if type mismatches occur. In contrast, statically typed languages, like C++, require that variable types be known at compile time.

### 2. Dynamic Typing in C++

Although C++ is statically typed, you can achieve dynamic typing through the use of:

- **Pointers**
- **References**
- **Dynamic Memory Allocation**
- **Base and Derived Classes with Polymorphism**

### 3. Pointers and Dynamic Memory

Using pointers, you can create variables that can reference different types at runtime. This is commonly used with base classes and derived classes.

```cpp
class Base {
public:
    virtual void display() { std::cout << "Base\n"; }
};

class Derived : public Base {
public:
    void display() override { std::cout << "Derived\n"; }
};

void show(Base* b) {
    b->display(); // Dynamic dispatch
}
```

### 4. Dynamic Memory Allocation

Using `new` and `delete`, you can allocate and deallocate memory for objects at runtime.

```cpp
Base* obj = new Derived(); // obj points to a Derived object
show(obj);
delete obj; // Clean up
```

### 5. Polymorphism and Virtual Functions

Polymorphism allows functions to operate on objects of different types through a common interface. This is achieved using virtual functions.

```cpp
class Base {
public:
    virtual void display() { std::cout << "Base\n"; }
};

class Derived : public Base {
public:
    void display() override { std::cout << "Derived\n"; }
};

void demonstrate(Base* b) {
    b->display(); // Calls the appropriate display method
}
```

### 6. Type Identification with RTTI

[[7_RTTI|Runtime Type Information]] allows you to determine the type of an object at runtime using the `typeid` operator and `dynamic_cast`.

```cpp
Base* base = new Derived();
if (Derived* derived = dynamic_cast<Derived*>(base)) {
    // Safe downcast
}
```

## Advantages of Dynamic Typing

1. **Flexibility**: You can write more generic and reusable code.
2. **Ease of Use**: It simplifies code when dealing with polymorphic types or collections of mixed types.

## Disadvantages of Dynamic Typing

1. **Runtime Errors**: Type-related errors can occur at runtime, making debugging more challenging.
2. **Performance Overhead**: Dynamic type checking can introduce performance penalties compared to static typing.

## Conclusion

While C++ is fundamentally a statically typed language, it provides features that allow for dynamic behavior through pointers, polymorphism, and dynamic memory allocation. Understanding these concepts enables developers to write flexible and robust code while maintaining the advantages of static type safety.
