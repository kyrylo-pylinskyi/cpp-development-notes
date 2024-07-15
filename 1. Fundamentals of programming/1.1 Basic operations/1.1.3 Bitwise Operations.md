# Bitwise Operations

Bitwise operations allow manipulation of individual bits within binary representations of integers. These operations are fundamental in systems programming, cryptography, and performance-critical code where direct bit manipulation is required.

#### Bitwise Operators
C++ provides several bitwise operators to manipulate bits directly:

1. **AND (`&`)**: Performs a bitwise AND operation.
   ```cpp
   int result = a & b;  // Each bit in the result is 1 if the corresponding bits in both a and b are 1
   ```

2. **OR (`|`)**: Performs a bitwise OR operation.
   ```cpp
   int result = a | b;  // Each bit in the result is 1 if the corresponding bit in either a or b is 1
   ```

3. **XOR (`^`)**: Performs a bitwise XOR (exclusive OR) operation.
   ```cpp
   int result = a ^ b;  // Each bit in the result is 1 if the corresponding bits in a and b are different
   ```

4. **NOT (`~`)**: Performs a bitwise NOT (complement) operation.
   ```cpp
   int result = ~a;  // Each bit in the result is the inverse of the corresponding bit in a
   ```

5. **Left Shift (`<<`)**: Shifts bits to the left by a specified number of positions.
   ```cpp
   int result = a << 2;  // Shifts the bits in a to the left by 2 positions (equivalent to multiplying by 4)
   ```

6. **Right Shift (`>>`)**: Shifts bits to the right by a specified number of positions.
   ```cpp
   int result = a >> 2;  // Shifts the bits in a to the right by 2 positions (equivalent to dividing by 4)
   ```

#### Examples
**Bitwise AND:**
```cpp
int a = 5;  // Binary: 0101
int b = 3;  // Binary: 0011
int result = a & b;  // Binary: 0001, result is 1
```

**Bitwise OR:**
```cpp
int result = a | b;  // Binary: 0111, result is 7
```

**Bitwise XOR:**
```cpp
int result = a ^ b;  // Binary: 0110, result is 6
```

**Bitwise NOT:**
```cpp
int result = ~a;  // Binary: 1010 (inverting each bit), result is -6 (due to two's complement representation)
```

**Left Shift:**
```cpp
int result = a << 1;  // Binary: 1010, result is 10
```

**Right Shift:**
```cpp
int result = a >> 1;  // Binary: 0010, result is 2
```

#### Applications of Bitwise Operations

1. **Bit Masks:**
   Bit masks are used to extract, set, or clear specific bits within a binary number.
   ```cpp
   int mask = 0x0F;  // Binary: 00001111
   int value = 0xF0; // Binary: 11110000
   int result = value & mask;  // Extracts the lower 4 bits, result is 0
   ```

2. **Setting a Bit:**
   ```cpp
   int n = 5;  // Binary: 0101
   int pos = 1;
   n |= (1 << pos);  // Sets the bit at position 1, result is 7 (Binary: 0111)
   ```

3. **Clearing a Bit:**
   ```cpp
   n &= ~(1 << pos);  // Clears the bit at position 1, result is 5 (Binary: 0101)
   ```

4. **Toggling a Bit:**
   ```cpp
   n ^= (1 << pos);  // Toggles the bit at position 1, result is 7 if initially 5 and vice versa
   ```

5. **Checking a Bit:**
   ```cpp
   bool bit = n & (1 << pos);  // Checks if the bit at position 1 is set
   ```

6. **Swapping Two Numbers Without Temporary Variable:**
   ```cpp
   int x = 5;
   int y = 3;
   x ^= y;
   y ^= x;
   x ^= y;
   // Now x is 3 and y is 5
   ```

7. **Counting Set Bits (Hamming Weight):**
   ```cpp
   int countSetBits(int n) {
       int count = 0;
       while (n) {
           count += n & 1;
           n >>= 1;
       }
       return count;
   }
   ```

#### Performance Considerations
Bitwise operations are often more efficient than arithmetic operations because they operate directly on the binary representation of numbers, typically translating to fewer machine instructions. They are useful in performance-critical applications, such as graphics processing, cryptographic algorithms, and low-level system programming.

#### Summary
Bitwise operations provide powerful tools for efficient manipulation of individual bits in an integer's binary representation. Mastery of these operations is essential for advanced programming tasks requiring direct hardware manipulation, performance optimization, and compact data representation.
