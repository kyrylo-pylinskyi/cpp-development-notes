
# Multiple Inheritance

Multiple inheritance is a feature in C++ that allows a class to inherit from more than one base class. While this can be a powerful tool, it introduces complexities that require careful management, such as ambiguity and the diamond problem.

## Basics of Multiple Inheritance

### Syntax

The syntax for multiple inheritance is straightforward. You list all the base classes in the class definition.

```cpp
class Father {
public:
    void playSports() {
        std::cout << "Father likes to play sports." << std::endl;
    }
};

class Mother {
public:
    void cook() {
        std::cout << "Mother likes to cook." << std::endl;
    }
};

class Son : public Father, public Mother {
};
```

In this example, `Son` inherits from both `Father` and `Mother`. As a result, `Son` objects have access to members of both base classes.

### Accessing Base Class Members

A derived class can access the members of its base classes directly if there are no name conflicts.

```cpp
int main() {
    Son son;
    son.playSports(); // Calls Father::playSports
    son.cook(); // Calls Mother::cook
    return 0;
}
```

## Ambiguity in Multiple Inheritance

When two or more base classes have members with the same name, ambiguity arises. The compiler cannot determine which member to call.

### Example of Ambiguity

```cpp
class Father {
public:
    void speak() {
        std::cout << "Father speaks." << std::endl;
    }
};

class Mother {
public:
    void speak() {
        std::cout << "Mother speaks." << std::endl;
    }
};

class Son : public Father, public Mother {
};

int main() {
    Son son;
    son.speak(); // Error: ambiguous
    return 0;
}
```

To resolve this ambiguity, you need to specify the base class explicitly.

```cpp
int main() {
    Son son;
    son.Father::speak(); // Calls Father::speak
    son.Mother::speak(); // Calls Mother::speak
    return 0;
}
```

## The Diamond Problem

The [[13_diamond_problem|diamond problem]] occurs when a class inherits from two classes that both inherit from a common base class. This creates ambiguity and redundancy in the inheritance hierarchy.

### Example of the Diamond Problem

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

In this example, `Son` has two copies of `GrandMother`, one through `Father` and one through `Mother`. This leads to ambiguity when accessing members of `GrandMother`.

```cpp
int main() {
    Son son;
    son.tellStories(); // Error: ambiguous
    return 0;
}
```

### Solution: Virtual Inheritance

[[15_virtual_inheritance|Virtual inheritance]] solves the diamond problem by ensuring that there is only one instance of the common base class.

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

With virtual inheritance, `Son` only has one instance of `GrandMother`.

```cpp
int main() {
    Son son;
    son.tellStories(); // Calls GrandMother::tellStories without ambiguity
    return 0;
}
```

## Best Practices for Multiple Inheritance

1. **Avoid if Possible**: Use composition or interfaces (pure virtual classes) instead of multiple inheritance where feasible.
2. **Use Virtual Inheritance**: When dealing with shared base classes to avoid the diamond problem.
3. **Explicit Qualification**: Clearly specify the base class when accessing inherited members to resolve ambiguity.
4. **Clear Design**: Ensure that the design justifies the use of multiple inheritance and does not introduce unnecessary complexity.

## Summary

Multiple inheritance in C++ allows a class to inherit from more than one base class, providing flexibility and power. However, it introduces complexities such as ambiguity and the diamond problem. By using explicit qualification and virtual inheritance, you can manage these complexities effectively. When designing your classes, carefully consider whether multiple inheritance is necessary and whether alternative designs might be simpler and more maintainable.