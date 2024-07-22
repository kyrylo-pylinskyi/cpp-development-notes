# Diamond Problem

The diamond problem is a common issue in [[11_multiple_inheritance|multiple inheritance]] in C++. It arises when a derived class inherits from two classes that both inherit from a common base class, leading to ambiguity and potential redundancy.

## Understanding the Diamond Problem

### Example of the Diamond Problem

Consider the following example where `Son` inherits from both `Father` and `Mother`, which in turn inherit from `GrandMother`.

```cpp
class GrandMother {
public:
    void tellStories() {
        std::cout << "GrandMother tells stories." << std::endl;
    }
};

class Father : public GrandMother {
};

class Mother : public GrandMother {
};

class Son : public Father, public Mother {
};
```

In this example, `Son` inherits from both `Father` and `Mother`. Each of these classes inherits from `GrandMother`. Consequently, `Son` has two copies of `GrandMother`: one through `Father` and one through `Mother`. This creates ambiguity when accessing members of `GrandMother`.
#### Memory model of 'Diamond Problem' `Son`

```
+--------------------------+
|        GrandMother       |     // First GrandMother
|--------------------------|
| grandmotherData          |
+--------------------------+
|        Father            |
|--------------------------|
| fatherData               |
+--------------------------+
|        GrandMother       |     // Second GrandMother
|--------------------------|
| grandmotherData          |
+--------------------------+
|        Mother            |
|--------------------------|
| motherData               |
+--------------------------+
|        Son               |
|--------------------------|
| sonData                  |
+--------------------------+
```

### Ambiguity in Member Access

```cpp
int main() {
    Son son;
    son.tellStories(); // Error: ambiguous
    return 0;
}
```

The compiler cannot determine which `tellStories` function to call because `Son` has two `tellStories` functions: one from `Father`'s `GrandMother` and one from `Mother`'s `GrandMother`.

## Solution: Virtual Inheritance

[[15_virtual_inheritance|Virtual inheritance]] is used to solve the diamond problem by ensuring that there is only one instance of the common base class, even if it is inherited multiple times.

### Implementing Virtual Inheritance

Modify the inheritance of `Father` and `Mother` to use virtual inheritance.

```cpp
class GrandMother {
public:
    void tellStories() {
        std::cout << "GrandMother tells stories." << std::endl;
    }
};

class Father : public virtual GrandMother {
};

class Mother : public virtual GrandMother {
};

class Son : public Father, public Mother {
};
```

With virtual inheritance, `Son` only has one instance of `GrandMother`, eliminating the ambiguity.

#### Memory model of `Son` with virtual inherited `GrandMother`

```
+--------------------------+
|        GrandMother       |
|--------------------------|
| grandmotherData          |
+--------------------------+
|        Father            |
|--------------------------|
| fatherData               |
| Pointer to GrandMother   |
+--------------------------+
|        Mother            |
|--------------------------|
| motherData               |
| Pointer to GrandMother   |
+--------------------------+
|        Son               |
|--------------------------|
| sonData                  |
+--------------------------+

```
### Accessing Members with Virtual Inheritance

```cpp
int main() {
    Son son;
    son.tellStories(); // Calls GrandMother::tellStories without ambiguity
    return 0;
}
```

Now, `tellStories` is called unambiguously because there is only one instance of `GrandMother`.

## Detailed Explanation of Virtual Inheritance

### Memory Layout

Virtual inheritance changes the memory layout of the derived class to ensure that only one instance of the base class is shared among all the derived classes. This is achieved by maintaining a virtual table (vtable) to keep track of the base class instance.

### Constructor Invocation

When using virtual inheritance, the most derived class (the furthest down the inheritance chain) is responsible for calling the constructor of the virtual base class. This ensures that the base class is properly initialized only once.

```cpp
class GrandMother {
public:
    GrandMother() {
        std::cout << "GrandMother constructor called." << std::endl;
    }
    void tellStories() {
        std::cout << "GrandMother tells stories." << std::endl;
    }
};

class Father : public virtual GrandMother {
public:
    Father() : GrandMother() {
        std::cout << "Father constructor called." << std::endl;
    }
};

class Mother : public virtual GrandMother {
public:
    Mother() : GrandMother() {
        std::cout << "Mother constructor called." << std::endl;
    }
};

class Son : public Father, public Mother {
public:
    Son() : GrandMother(), Father(), Mother() {
        std::cout << "Son constructor called." << std::endl;
    }
};

int main() {
    Son son;
    son.tellStories();
    return 0;
}
```

### Constructor Output

```
GrandMother constructor called.
Father constructor called.
Mother constructor called.
Son constructor called.
GrandMother tells stories.
```

This output demonstrates that `GrandMother`'s constructor is called only once, even though both `Father` and `Mother` inherit from it, solving the diamond problem.

## Summary

The diamond problem in C++ arises when a derived class inherits from multiple base classes that share a common ancestor, leading to ambiguity and redundancy. Virtual inheritance solves this problem by ensuring a single instance of the common base class is shared among all derived classes. By carefully using virtual inheritance, you can avoid the complexities and ambiguities introduced by multiple inheritance in C++.