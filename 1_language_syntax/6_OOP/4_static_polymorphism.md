# Static Polymorphism

Static polymorphism, also known as compile-time polymorphism, is a form of polymorphism that is resolved during compile time. It is typically achieved through [[5_method_overloading|method overloading]], operator overloading, and template metaprogramming. Static polymorphism contrasts with [[6_dynamic_polymorphism|dynamic polymorphism]], which is resolved at runtime using mechanisms such as [[7_virtual_methods|virtual methods]].

## Key Concepts

### Method Overloading

[[5_method_overloading|Method overloading]] allows multiple functions to have the same name but different parameter lists. The correct method is selected based on the arguments provided during the method call.

#### Example:

```cpp
#include <iostream>

class Printer{
public:
	void print(int i) {
	    std::cout << "Integer: " << i << std::endl;
	}
	
	void print(double f) {
	    std::cout << "Double: " << f << std::endl;
	}
	
	void print(const std::string& s) {
	    std::cout << "String: " << s << std::endl;
	}
}


int main() {
	Printer p;

    p.print(10);           // Calls Printers print(int)
    p.print(3.14);         // Calls Printers print(double)
    p.print("Hello");      // Calls Printers print(std::string)
    return 0;
}
```

### Operator Overloading

Operator overloading allows you to redefine the meaning of an operator for user-defined types (such as [[2_classes|classes]]). This enables the use of operators like `+`, `-`, `*`, and others with custom classes.

#### Example:

```cpp
#include <iostream>

class Complex {
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}

    // Overload the + operator
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }

    void print() const {
        std::cout << "Complex number: " << real << " + " << imag << "i" << std::endl;
    }

private:
    double real, imag;
};

int main() {
    Complex c1(3.0, 4.0);
    Complex c2(1.0, 2.0);
    Complex c3 = c1 + c2; // Uses overloaded + operator
    c3.print();           // Output: Complex number: 4 + 6i
    return 0;
}
```

### Template Metaprogramming

[[1_Templates|Templates]] in C++ allow you to write generic and reusable code. Template metaprogramming uses templates to perform computations at compile time, enabling static polymorphism. 

#### Example: Function Template

```cpp
#include <iostream>

// Function template
template <typename T>
T add(T a, T b) {
    return a + b;
}

int main() {
    std::cout << "Sum of integers: " << add(2, 3) << std::endl;           // Output: 5
    std::cout << "Sum of doubles: " << add(2.5, 3.5) << std::endl;       // Output: 6
    std::cout << "Sum of strings: " << add(std::string("Hello"), std::string(" World")) << std::endl; // Output: Hello World
    return 0;
}
```

### CRTP (Curiously Recurring Template Pattern)

[[7_CRTP|CRTP]] is a technique used to achieve static polymorphism where a class template derives from a specialization of itself. This pattern is often used to implement compile-time polymorphic behavior without the overhead of virtual functions.

#### Example:

```cpp
#include <iostream>

// Base template class
template <typename Derived>
class Base {
public:
    void interface() {
        // Call the derived class implementation
        static_cast<Derived*>(this)->implementation();
    }
};

// Derived class
class Derived : public Base<Derived> {
public:
    void implementation() {
        std::cout << "Derived class implementation." << std::endl;
    }
};

int main() {
    Derived d;
    d.interface();  // Output: Derived class implementation.
    return 0;
}
```

### Pros and Cons

#### Pros:
- **Performance**: Static polymorphism can lead to more efficient code as it avoids the runtime overhead of dynamic polymorphism (such as virtual function calls).
- **Type Safety**: Errors can be caught at compile time, improving type safety.
- **Inline Expansion**: Since the compiler knows the exact types involved, it can inline functions, potentially improving performance.

#### Cons:
- **Code Bloat**: Templates can lead to code bloat as the compiler generates code for each type instantiation.
- **Complexity**: Template metaprogramming can be complex and difficult to debug.
- **Reduced Flexibility**: Static polymorphism requires all types to be known at compile time, reducing flexibility compared to [[6_dynamic_polymorphism|dynamic polymorphism]].

## Conclusion

Static polymorphism in C++ offers powerful tools for creating efficient and type-safe code through function overloading, operator overloading, and templates. Understanding and leveraging these concepts can lead to more robust and high-performance applications. However, it is essential to balance these benefits with the potential downsides, such as increased complexity and code bloat.