# Rule of Zero-Three-Five

In C++, the Rule of Zero-Three-Five is a guideline that helps developers manage resource ownership and object lifetime effectively. It provides a systematic way to ensure that classes handle resource management correctly, especially when dealing with dynamic memory, file handles, sockets, or other resources that require explicit management.

## Rule of Zero

The Rule of Zero states that a class should not explicitly declare any of the following special member functions if it doesn’t manage any resources:

1. Destructor
2. Copy constructor
3. Copy assignment operator
4. Move constructor
5. Move assignment operator

By adhering to the Rule of Zero, you can rely on the compiler-generated implementations of these functions, which are typically sufficient for classes that do not manage resources. This simplifies the code and reduces the risk of errors.

### Example

```cpp
class NonResourceClass {
public:
    int x;
    double y;
    // No need to define special member functions
};
```

In this example, `NonResourceClass` does not manage any resources, so it doesn’t need to define any special member functions. The compiler-generated versions are sufficient.

## Rule of Three

The Rule of Three applies when a class manages a resource. It states that if a class needs to define any one of the following special member functions, it should probably explicitly define all three:

1. Destructor
2. Copy constructor
3. Copy assignment operator

### Example

```cpp
class ResourceClass {
private:
    int* data;

public:
    // Constructor
    ResourceClass(size_t size) : data(new int[size]) {}

    // Destructor
    ~ResourceClass() {
        delete[] data;
    }

    // Copy constructor
    ResourceClass(const ResourceClass& other) : data(new int[*other.data]) {}

    // Copy assignment operator
    ResourceClass& operator=(const ResourceClass& other) {
        if (this != &other) {
            delete[] data;
            data = new int[*other.data];
        }
        return *this;
    }
};
```

In this example, `ResourceClass` manages a dynamic array of integers. Since it needs a custom destructor to release the memory, it also defines a copy constructor and a copy assignment operator to ensure correct copying of the resource.

## Rule of Five

The Rule of Five extends the Rule of Three to include move semantics. It states that if a class defines any one of the following special member functions, it should probably explicitly define all five:

1. Destructor
2. Copy constructor
3. Copy assignment operator
4. Move constructor
5. Move assignment operator

### Example

```cpp
class ResourceClass {
private:
    int* data;

public:
    // Constructor
    ResourceClass(size_t size) : data(new int[size]) {}

    // Destructor
    ~ResourceClass() {
        delete[] data;
    }

    // Copy constructor
    ResourceClass(const ResourceClass& other) : data(new int[*other.data]) {}

    // Copy assignment operator
    ResourceClass& operator=(const ResourceClass& other) {
        if (this != &other) {
            delete[] data;
            data = new int[*other.data];
        }
        return *this;
    }

    // Move constructor
    ResourceClass(ResourceClass&& other) noexcept : data(other.data) {
        other.data = nullptr;
    }

    // Move assignment operator
    ResourceClass& operator=(ResourceClass&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            other.data = nullptr;
        }
        return *this;
    }
};
```

In this example, `ResourceClass` manages a dynamic array of integers and defines all five special member functions. The move constructor and move assignment operator are used to transfer ownership of the resource, making the class more efficient when used with temporary objects.

## Summary

- **Rule of Zero**: If your class does not manage any resources, avoid defining special member functions. The compiler-generated versions are typically sufficient.
- **Rule of Three**: If your class manages resources and needs to define a destructor, it should also define the copy constructor and copy assignment operator.
- **Rule of Five**: If your class manages resources and needs to define a destructor, it should also define the copy constructor, copy assignment operator, move constructor, and move assignment operator.

Following these rules ensures that your classes handle resource management correctly, avoiding common pitfalls such as resource leaks and double deletions. By adhering to the Rule of Zero-Three-Five, you can write safer and more maintainable C++ code.