
# Non-Virtual Methods Overriding 

In C++, if you attempt to override a non-virtual method in a derived class, the method in the derived class will **not** actually override the base class method. Instead, it hides the base class method. This can lead to unexpected behavior, as calls to the base class method will not use the derived class's implementation, even if the derived class is instantiated.

## Example of Hiding Non-Virtual Methods

```cpp
#include <iostream>

class Base {
public:
    void show() { // Non-virtual method
        std::cout << "Base class show method called." << std::endl;
    }
};

class Derived : public Base {
public:
    void show() { // Hides Base's show method
        std::cout << "Derived class show method called." << std::endl;
    }
};

int main() {
    Base b;
    Derived d;

    b.show(); // Calls Base's show
    d.show(); // Calls Derived's show

    Base* ptr = &d;
    ptr->show(); // Calls Base's show, NOT Derived's
    return 0;
}
```

### Output:
```
Base class show method called.
Derived class show method called.
Base class show method called.
```

## The `override` Keyword

The `override` keyword in C++ is used to indicate that a method in a derived class is intended to override a virtual method in a base class. This keyword serves several purposes:

1. **Compile-Time Check**: The compiler checks that there is a corresponding virtual method in the base class that is being overridden. If there is no matching base method, the compiler will generate an error.

3. **Code Clarity**: It makes the programmer's intention explicit, improving code readability and maintainability.

To override the virtual method in a derived class `override` keyword is not necessary.
The `override` keyword serves to explicitly indicate that you are intentionally overriding a virtual method from a base class, promoting clarity and preventing accidental method signature mismatches.

### Example of Using `override`

```cpp
class Base {
public:
    virtual void show() {
        std::cout << "Base class show method called." << std::endl;
    }
};

class Derived : public Base {
public:
    void show() override { // Correctly overrides Base's show method
        std::cout << "Derived class show method called." << std::endl;
    }
};
```

### Conclusion

- **Non-Virtual Method Hiding**: If you override a non-virtual method, the base class method will still exist and will not be overridden. Instead, it will be hidden by the derived class method.
- **Use of `override`**: The `override` keyword is crucial for indicating intent and ensuring that you are correctly overriding a virtual method. It helps prevent bugs and enhances code clarity by making your intentions clear to both the compiler and other developers.