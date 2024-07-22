# Standard Exceptions

C++ provides a rich set of standard exceptions to handle different error conditions effectively. Here's a detailed overview of these exceptions:

### Logic Errors

- **logic_error**: Base class for logic errors, indicating a violation of logical preconditions or assumptions.
- **invalid_argument**: Thrown to indicate invalid arguments passed to a function.
- **domain_error**: Thrown when a mathematical function receives arguments outside its domain.
- **length_error**: Thrown when attempting to create a container larger than its maximum size.
- **out_of_range**: Thrown when attempting to access elements outside the valid range of a container.

### Future Error (since C++11)

- **future_error**: Thrown by operations on `std::future` and `std::promise` when they fail.

### Runtime Errors

- **runtime_error**: Base class for runtime errors, representing problems that can only be detected during runtime.
- **range_error**: Thrown to indicate errors in computations resulting in values outside the range of representable values.
- **overflow_error**: Thrown when a computation produces a result that cannot be represented due to overflow.
- **underflow_error**: Thrown when a computation produces a result that is too small to be represented due to underflow.

### Regular Expression Error (since C++11)

- **regex_error**: Thrown to report errors in the construction, evaluation, and execution of regular expressions.

### System Error (since C++11)

- **system_error**: Represents errors from system calls and other low-level operations.
- **ios_base::failure**: Thrown to report I/O stream errors. Before C++11, it was used generally for I/O errors.

### Filesystem Error (since C++17)

- **filesystem::filesystem_error**: Thrown to report errors from filesystem operations.

### Transactional Memory Exception

- **tx_exception**: Used in Transactional Memory (TM) Technical Specification to report transaction-related errors.

### Time Zone Exceptions (since C++20)

- **nonexistent_local_time**: Thrown when attempting to convert a nonexistent local time to a valid time.
- **ambiguous_local_time**: Thrown when attempting to convert an ambiguous local time to a valid time.

### Format Error (since C++20)

- **format_error**: Thrown when a format string or its arguments are invalid.

### Type and Casting Errors

- **bad_typeid**: Thrown when using `typeid` on a null pointer to a polymorphic type.
- **bad_cast**: Thrown when a dynamic_cast to a reference type fails.
- **bad_any_cast**: Thrown when an `std::any_cast` to an incorrect type is performed (since C++17).
- **bad_optional_access**: Thrown when accessing the value of an empty `std::optional` (since C++17).
- **bad_expected_access**: Thrown when accessing the value of an erroneous `std::expected` (since C++23).
- **bad_weak_ptr**: Thrown when attempting to access an expired `std::weak_ptr` (since C++11).
- **bad_function_call**: Thrown when calling an empty `std::function` (since C++11).

### Memory Management Errors

- **bad_alloc**: Thrown by `new` when memory allocation fails.
- **bad_array_new_length**: Thrown when attempting to allocate an array with `new[]` using a negative size or an excessively large size (since C++11).

### Exception Handling Errors

- **bad_exception**: Thrown when a dynamic exception specification is violated.
- **ios_base::failure**: Used before C++11 to report errors in I/O operations, but now primarily used as a more specific system error.

### Variant Access Error (since C++17)

- **bad_variant_access**: Thrown when accessing a value from an inactive member of `std::variant`.

#### Resources
en.cppreference.com/w/cpp/error/exception
