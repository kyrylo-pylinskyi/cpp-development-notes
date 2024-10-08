
# Raw Pointers

Raw pointers are the fundamental pointer type in C++ that directly reference memory addresses. Unlike smart pointers, raw pointers do not manage memory automatically, making them powerful but also potentially dangerous if mismanaged.

## Key Features of Raw Pointers

### 1. Basic Syntax

A raw pointer is declared using the `*` operator:

```cpp
int* ptr; // A pointer to an integer
```

### 2. Dynamic Memory Management

Raw pointers can be used to allocate and deallocate memory manually using `new` and `delete`.
[[4_new_and_delete]]
#### Example

```cpp
int* ptr = new int(10); // Allocate memory for an integer
delete ptr;             // Free the allocated memory
```

### 3. No Automatic Memory Management

Unlike [[6_smart_pointers|smart pointer]], raw pointers do not automatically manage the memory they point to. This can lead to issues like memory leaks or dangling pointers if not handled carefully.

### 4. Pointer Arithmetic

Raw pointers support pointer arithmetic, allowing developers to navigate through arrays or dynamically allocated memory blocks.

#### Example

```cpp
int arr[] = {1, 2, 3};
int* ptr = arr; // Pointing to the first element
ptr++;          // Now points to the second element
```

### 5. Ownership Semantics

Raw pointers do not enforce ownership semantics. This means that multiple raw pointers can point to the same memory without any indication of who is responsible for managing it.

### 6. Null Pointers

A raw pointer can be assigned a `nullptr` value to indicate that it does not point to any object.

#### Example

```cpp
int* ptr = nullptr; // Safe initialization
```

### 7. Use Cases

Raw pointers are often used in low-level programming, performance-critical sections, or legacy code where manual memory management is required.

## Risks of Using Raw Pointers

### 1. Memory Leaks

Failing to deallocate memory allocated with `new` leads to [[5_memory_leaks|memory leaks]].

```cpp
int* ptr = new int(10);
// Forgetting to delete ptr causes a memory leak
```

### 2. Dangling Pointers

If a pointer references memory that has already been freed, it results in a dangling pointer, leading to undefined behavior.

```cpp
int* ptr = new int(10);
delete ptr;
// ptr is now a dangling pointer
```

### 3. Double Deletion

Attempting to delete the same pointer twice can lead to undefined behavior.

```cpp
int* ptr = new int(10);
delete ptr;
delete ptr; // Error: double deletion
```

## Conclusion

Raw pointers are a fundamental part of C++ programming that provide flexibility and direct memory manipulation capabilities. However, their use comes with risks such as memory leaks and dangling pointers. Understanding when and how to use raw pointers effectively is essential for writing safe and efficient C++ code. In many cases, smart pointers are recommended to manage memory automatically and avoid common pitfalls associated with raw pointers.