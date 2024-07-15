# `new` and `delete` Operators

In C++, dynamic memory allocation is managed using the `new` and `delete` operators. These operators allow programmers to allocate and deallocate memory manually, giving precise control over memory usage.

## Key Features of `new` and `delete`

### 1. `new` Operator

The `new` operator is used to allocate memory dynamically on the heap. It returns a pointer to the allocated memory. 

#### Syntax

```cpp
type* pointer = new type;
type* pointer = new type(initializer);
type* pointer = new type[size];
```

#### Examples

- **Single Object Allocation**:

  ```cpp
  int* ptr = new int;          // Allocates memory for an integer
  int* ptr = new int(10);      // Allocates and initializes the integer to 10
  ```

- **Array Allocation**:

  ```cpp
  int* arr = new int[5];       // Allocates memory for an array of 5 integers
  ```

### 2. `delete` Operator

The `delete` operator is used to deallocate memory that was previously allocated with `new`. It ensures that the memory is freed and can be reused by the system.

#### Syntax

```cpp
delete pointer;
delete[] pointer;
```

#### Examples

- **Single Object Deallocation**:

  ```cpp
  int* ptr = new int(10);
  delete ptr;                  // Deallocates the memory for the integer
  ```

- **Array Deallocation**:

  ```cpp
  int* arr = new int[5];
  delete[] arr;                // Deallocates the memory for the array
  ```

### 3. Important Points

- **Initialization**: Memory allocated with `new` is uninitialized unless an initializer is provided.
- **Null Pointer Safety**: Deleting a null pointer is safe and has no effect.
- **Memory Leaks**: Failing to use `delete` after `new` leads to memory leaks.
- **Dangling Pointers**: Using a pointer after `delete` leads to undefined behavior (dangling pointer).

### 4. Custom `new` and `delete` Operators

C++ allows overloading the `new` and `delete` operators for custom behavior, such as logging allocations or using a custom memory pool.

#### Example

```cpp
#include <iostream>

void* operator new(size_t size) {
    std::cout << "Allocating " << size << " bytes\n";
    return malloc(size);
}

void operator delete(void* ptr) noexcept {
    std::cout << "Deallocating memory\n";
    free(ptr);
}

int main() {
    int* ptr = new int(10);    // Uses the custom new operator
    delete ptr;                // Uses the custom delete operator
    return 0;
}
```

## Conclusion

The `new` and `delete` operators are fundamental for dynamic memory management in C++. Proper use of these operators is crucial for resource management and avoiding issues like memory leaks and dangling pointers. Understanding their behavior and best practices is essential for effective C++ programming.