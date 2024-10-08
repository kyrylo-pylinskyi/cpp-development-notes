# Operators

Operators in C++ are special symbols that perform operations on variables and values. Understanding operators is essential for effective programming, as they enable the implementation of various algorithms and data manipulations.

## Types of Operators

### 1. Arithmetic Operators

Arithmetic operators perform basic mathematical operations.

| Operator | Description          | Example          |
|----------|----------------------|-------------------|
| `+`      | Addition             | `a + b`           |
| `-`      | Subtraction          | `a - b`           |
| `*`      | Multiplication       | `a * b`           |
| `/`      | Division             | `a / b`           |
| `%`      | Modulus (Remainder) | `a % b`           |

### 2. Relational Operators

Relational operators compare two values and return a boolean result.

| Operator | Description               | Example     |
|----------|---------------------------|-------------|
| `==`     | Equal to                  | `a == b`    |
| `!=`     | Not equal to              | `a != b`    |
| `>`      | Greater than              | `a > b`     |
| `<`      | Less than                 | `a < b`     |
| `>=`     | Greater than or equal to  | `a >= b`    |
| `<=`     | Less than or equal to     | `a <= b`    |

### 3. Logical Operators

Logical operators are used to combine conditional statements.

| Operator | Description | Example  |
| -------- | ----------- | -------- |
| `&&`     | Logical AND | `a && b` |
| \|\|     | Logical OR  | a \|\| b |
| `!`      | Logical NOT | `!a`     |

### 4. Bitwise Operators

Bitwise operators perform operations on bits and are commonly used in low-level programming.

| Operator | Description | Example  |
| -------- | ----------- | -------- |
| `&`      | Bitwise AND | `a & b`  |
| \|       | Bitwise OR  | a \| b   |
| `^`      | Bitwise XOR | `a ^ b`  |
| `~`      | Bitwise NOT | `~a`     |
| `<<`     | Left shift  | `a << 2` |
| `>>`     | Right shift | `a >> 2` |

### 5. Assignment Operators

Assignment operators are used to assign values to variables.

| Operator  | Description                      | Example        |
|-----------|----------------------------------|-----------------|
| `=`       | Assigns value                   | `a = b`         |
| `+=`      | Add and assign                  | `a += b`        |
| `-=`      | Subtract and assign             | `a -= b`        |
| `*=`      | Multiply and assign             | `a *= b`        |
| `/=`      | Divide and assign               | `a /= b`        |
| `%=`      | Modulus and assign              | `a %= b`        |

### 6. Unary Operators

Unary operators operate on a single operand.

| Operator | Description              | Example     |
|----------|--------------------------|-------------|
| `++`     | Increment                | `++a` or `a++` |
| `--`     | Decrement                | `--a` or `a--` |
| `-`      | Unary negation           | `-a`        |
| `+`      | Unary plus (identity)   | `+a`        |

### 7. Conditional (Ternary) Operator

The conditional operator is a shorthand for `if-else` statements.

| Operator | Description                    | Example              |
|----------|--------------------------------|----------------------|
| `? :`    | Ternary conditional            | `condition ? a : b` |

### 8. Sizeof Operator

The `sizeof` operator returns the size, in bytes, of a data type or variable.

```cpp
sizeof(int) // Returns the size of int
```

### 9. Pointer Operators

Pointer operators are used with pointer variables.

| Operator | Description               | Example       |
|----------|---------------------------|---------------|
| `*`      | Dereference operator      | `*ptr`        |
| `&`      | Address-of operator       | `&var`        |

## Operator Precedence and Associativity

Understanding operator precedence and associativity is crucial for writing correct expressions.

### Operator Precedence

Operators have a hierarchy that determines the order in which operations are performed. For example:

1. Parentheses `()`
2. Unary operators `++`, `--`, `!`
3. Multiplication/Division/Modulus `*`, `/`, `%`
4. Addition/Subtraction `+`, `-`
5. Relational operators `<`, `>`, `<=`, `>=`
6. Equality operators `==`, `!=`
7. Logical AND `&&`
8. Logical OR `||`

### Associativity

Associativity defines the direction in which operators of the same precedence level are evaluated. Most operators are left-to-right associative, while the assignment operator (`=`) is right-to-left associative.

## Summary

Operators are fundamental components of C++ programming, enabling various operations on data types. Mastering operators and their precedence is essential for writing efficient and clear code. Understanding how to overload operators further extends the power of C++, allowing developers to create intuitive interfaces for user-defined types.
