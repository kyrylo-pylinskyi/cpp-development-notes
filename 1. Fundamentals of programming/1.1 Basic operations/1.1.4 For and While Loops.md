# For and While Loops

Loops are essential constructs in programming, enabling repetitive execution of a block of code. In C++, the two primary types of loops are `for` and `while` loops. These loops are used to iterate over data structures, execute a block of code multiple times, and manage control flow efficiently.

#### For Loops
A `for` loop is generally used when the number of iterations is known beforehand. It consists of three parts: initialization, condition, and increment/decrement, all in one line.

**Syntax:**
```cpp
for (initialization; condition; increment) {
    // Code to be executed
}
```

**Example:**
```cpp
for (int i = 0; i < 10; i++) {
    std::cout << "Iteration: " << i << std::endl;
}
```

**Explanation:**
- **Initialization**: Sets up a loop control variable (`int i = 0`).
- **Condition**: The loop continues as long as this condition is true (`i < 10`).
- **Increment**: Updates the control variable after each iteration (`i++`).

##### Advanced Usage
- **Nested Loops**: A loop inside another loop. Useful for multi-dimensional data structures.
  ```cpp
  for (int i = 0; i < 5; i++) {
      for (int j = 0; j < 5; j++) {
          std::cout << "(" << i << ", " << j << ") ";
      }
      std::cout << std::endl;
  }
  ```

- **Range-Based For Loop**: Simplifies iteration over arrays or containers.
  ```cpp
  std::vector<int> numbers = {1, 2, 3, 4, 5};
  for (int num : numbers) {
      std::cout << num << std::endl;
  }
  ```

#### While Loops
A `while` loop is used when the number of iterations is not known beforehand and depends on a condition.

**Syntax:**
```cpp
while (condition) {
    // Code to be executed
}
```

**Example:**
```cpp
int i = 0;
while (i < 10) {
    std::cout << "Iteration: " << i << std::endl;
    i++;
}
```

**Explanation:**
- **Condition**: The loop continues as long as this condition is true (`i < 10`).
- **Increment**: Needs to be manually included within the loop (`i++`).

##### Advanced Usage
- **Infinite Loops**: A loop that runs indefinitely until an external condition breaks it.
  ```cpp
  while (true) {
      // Infinite loop
      if (someCondition) break;  // Use break to exit
  }
  ```

- **Input Validation**: Useful in scenarios where user input needs to be validated.
  ```cpp
  int number;
  std::cout << "Enter a number between 1 and 10: ";
  std::cin >> number;
  while (number < 1 || number > 10) {
      std::cout << "Invalid input. Try again: ";
      std::cin >> number;
  }
  ```

#### Do-While Loop
A variation of the `while` loop that guarantees at least one execution of the loop body.

**Syntax:**
```cpp
do {
    // Code to be executed
} while (condition);
```

**Example:**
```cpp
int i = 0;
do {
    std::cout << "Iteration: " << i << std::endl;
    i++;
} while (i < 10);
```

**Explanation:**
- The loop body is executed once before the condition is tested (`i < 10`).

#### Control Statements in Loops
- **Break**: Exits the loop immediately.
  ```cpp
  for (int i = 0; i < 10; i++) {
      if (i == 5) break;  // Loop terminates when i equals 5
      std::cout << i << std::endl;
  }
  ```

- **Continue**: Skips the rest of the loop iteration and proceeds with the next iteration.
  ```cpp
  for (int i = 0; i < 10; i++) {
      if (i % 2 == 0) continue;  // Skips even numbers
      std::cout << i << std::endl;
  }
  ```

- **Return**: Exits the loop and the function immediately.
  ```cpp
  void checkNumbers() {
      for (int i = 0; i < 10; i++) {
          if (i == 5) return;  // Function terminates when i equals 5
          std::cout << i << std::endl;
      }
  }
  ```

Understanding and using `for` and `while` loops efficiently is crucial for controlling the flow of a C++ program, optimizing performance, and writing clean, maintainable code.

[[1. Fundamentals of Programming/Functions and Expressions|Next topic (Functions and Expressions)]]
