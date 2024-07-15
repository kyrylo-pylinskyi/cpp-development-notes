# Arithmetic Operations

Arithmetic operations are fundamental to many programming tasks, involving the manipulation and calculation of numerical data. In C++, these operations are performed using arithmetic operators.

#### Basic Arithmetic Operators
- **Addition (`+`)**: Adds two operands.
  ```cpp
  int a = 5;
  int b = 3;
  int sum = a + b;  // sum is 8
  ```
- **Subtraction (`-`)**: Subtracts the second operand from the first.
  ```cpp
  int difference = a - b;  // difference is 2
  ```
- **Multiplication (`*`)**: Multiplies two operands.
  ```cpp
  int product = a * b;  // product is 15
  ```
- **Division (`/`)**: Divides the first operand by the second. Note that integer division truncates the result.
  ```cpp
  int quotient = a / b;  // quotient is 1
  float fquotient = 5.0 / 3.0;  // fquotient is approximately 1.6667
  ```
- **Modulus (`%`)**: Returns the remainder of integer division.
  ```cpp
  int remainder = a % b;  // remainder is 2
  ```

#### Compound Assignment Operators
These operators combine an arithmetic operation with assignment, simplifying expressions.
- **Addition Assignment (`+=`)**:
  ```cpp
  a += b;  // equivalent to a = a + b
  ```
- **Subtraction Assignment (`-=`)**:
  ```cpp
  a -= b;  // equivalent to a = a - b
  ```
- **Multiplication Assignment (`*=`)**:
  ```cpp
  a *= b;  // equivalent to a = a * b
  ```
- **Division Assignment (`/=`)**:
  ```cpp
  a /= b;  // equivalent to a = a / b
  ```
- **Modulus Assignment (`%=`)**:
  ```cpp
  a %= b;  // equivalent to a = a % b
  ```

#### Increment and Decrement Operators
- **Increment (`++`)**: Increases an integer's value by one.
  ```cpp
  int x = 1;
  x++;  // x is now 2
  ++x;  // x is now 3
  ```
- **Decrement (`--`)**: Decreases an integer's value by one.
  ```cpp
  x--;  // x is now 2
  --x;  // x is now 1
  ```

#### Order of Operations
C++ follows the standard mathematical order of operations, also known as BODMAS/BIDMAS (Brackets, Orders (i.e., powers and square roots, etc.), Division and Multiplication, Addition and Subtraction). Parentheses can be used to explicitly define the order of operations.
```cpp
int result = (a + b) * (c - d);  // operations inside parentheses are evaluated first
```

Understanding and effectively using arithmetic operations is crucial for performing calculations and developing algorithms in C++.
