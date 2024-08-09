# STL Fixed-Width Integer Types in C++

The STL provides a set of fixed-width integer types to ensure consistent integer sizes across different platforms. These types are defined in the `<cstdint>` header and provide a standardized way to declare integers of specific sizes.

## Fixed-Width Integer Types

These types are defined to have a specific number of bits, making them portable and predictable.

### Exact-Width Integer Types

Exact-width types guarantee the integer will have the specified number of bits.

- **`int8_t`**: 8-bit signed integer.
- **`uint8_t`**: 8-bit unsigned integer.
- **`int16_t`**: 16-bit signed integer.
- **`uint16_t`**: 16-bit unsigned integer.
- **`int32_t`**: 32-bit signed integer.
- **`uint32_t`**: 32-bit unsigned integer.
- **`int64_t`**: 64-bit signed integer.
- **`uint64_t`**: 64-bit unsigned integer.

### Minimum-Width Integer Types

Minimum-width types guarantee at least the specified number of bits.

- **`int_least8_t`**: At least 8-bit signed integer.
- **`uint_least8_t`**: At least 8-bit unsigned integer.
- **`int_least16_t`**: At least 16-bit signed integer.
- **`uint_least16_t`**: At least 16-bit unsigned integer.
- **`int_least32_t`**: At least 32-bit signed integer.
- **`uint_least32_t`**: At least 32-bit unsigned integer.
- **`int_least64_t`**: At least 64-bit signed integer.
- **`uint_least64_t`**: At least 64-bit unsigned integer.

### Fastest Minimum-Width Integer Types

Fastest minimum-width types are the fastest types available with at least the specified number of bits.

- **`int_fast8_t`**: Fastest at least 8-bit signed integer.
- **`uint_fast8_t`**: Fastest at least 8-bit unsigned integer.
- **`int_fast16_t`**: Fastest at least 16-bit signed integer.
- **`uint_fast16_t`**: Fastest at least 16-bit unsigned integer.
- **`int_fast32_t`**: Fastest at least 32-bit signed integer.
- **`uint_fast32_t`**: Fastest at least 32-bit unsigned integer.
- **`int_fast64_t`**: Fastest at least 64-bit signed integer.
- **`uint_fast64_t`**: Fastest at least 64-bit unsigned integer.

### Pointer-Sized Integer Types

Pointer-sized types are integers that can hold a pointer.

- **`intptr_t`**: Signed integer type capable of holding a pointer.
- **`uintptr_t`**: Unsigned integer type capable of holding a pointer.

### Greatest-Width Integer Types

Greatest-width types represent the largest supported integer type.

- **`intmax_t`**: Largest signed integer type.
- **`uintmax_t`**: Largest unsigned integer type.

## Usage Examples

### Example: Using Exact-Width Types

```cpp
#include <cstdint>
#include <iostream>

int main() {
    int8_t smallNumber = 100;         // 8-bit signed integer
    uint16_t mediumNumber = 50000;    // 16-bit unsigned integer
    int32_t largeNumber = 1000000000; // 32-bit signed integer
    uint64_t hugeNumber = 1000000000000000000ULL; // 64-bit unsigned integer

    std::cout << "Small Number: " << static_cast<int>(smallNumber) << std::endl;
    std::cout << "Medium Number: " << mediumNumber << std::endl;
    std::cout << "Large Number: " << largeNumber << std::endl;
    std::cout << "Huge Number: " << hugeNumber << std::endl;

    return 0;
}
```

### Example: Using Pointer-Sized Types

```cpp
#include <cstdint>
#include <iostream>

int main() {
    intptr_t ptrValue = reinterpret_cast<intptr_t>(malloc(sizeof(int)));
    uintptr_t uptrValue = reinterpret_cast<uintptr_t>(malloc(sizeof(int)));

    std::cout << "Pointer Value: " << ptrValue << std::endl;
    std::cout << "Unsigned Pointer Value: " << uptrValue << std::endl;

    free(reinterpret_cast<void*>(ptrValue));
    free(reinterpret_cast<void*>(uptrValue));

    return 0;
}
```

## Summary

The STL fixed-width integer types defined in `<cstdint>` provide a portable and consistent way to declare integers of specific sizes. Using these types ensures that your code behaves predictably across different platforms, which is especially important for low-level programming and cross-platform development.