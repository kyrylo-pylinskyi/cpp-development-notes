# Internationalization

Internationalization (i18n) in C++ is the process of designing and preparing software so that it can be easily adapted to various languages and regions without engineering changes. This involves handling multiple character sets, date and time formats, currency formats, and other locale-specific data.

## Localization and Internationalization

### Key Concepts

- **Internationalization (i18n)**: The process of designing software so it can be adapted to various languages and regions.
- **Localization (l10n)**: The process of adapting software for a specific region or language by translating text and adjusting locale-specific settings.

### Character Sets and Encodings

C++ supports multiple character sets and encodings. UTF-8 is widely used for international applications.

```cpp
#include <iostream>
#include <locale>
#include <codecvt>

int main() {
    std::wstring_convert<std::codecvt_utf8_utf16<wchar_t>> converter;
    std::string utf8_str = "Hello, 世界!";
    std::wstring wide_str = converter.from_bytes(utf8_str);

    std::wcout.imbue(std::locale("en_US.UTF-8"));
    std::wcout << wide_str << std::endl;

    return 0;
}
```

### Locales

A locale is a set of parameters that defines the user's language, country, and any special variant preferences. The C++ Standard Library provides locale support through the `<locale>` header.

```cpp
#include <iostream>
#include <locale>

int main() {
    std::locale::global(std::locale("en_US.UTF-8"));
    std::wcout.imbue(std::locale());

    std::wcout << 1234567.89 << std::endl;

    return 0;
}
```

### Internationalized I/O

C++ streams can be imbued with a locale to handle internationalized input and output.

```cpp
#include <iostream>
#include <iomanip>
#include <locale>

int main() {
    std::locale::global(std::locale("fr_FR.UTF-8"));
    std::wcout.imbue(std::locale());

    std::wcout << std::showbase << std::put_money(12345.67) << std::endl; // Output: 12 345,67 €

    return 0;
}
```

## Handling Dates and Times

The `<chrono>` library in C++20 provides extensive support for dates and times, including formatting and parsing in a locale-aware manner.

```cpp
#include <iostream>
#include <chrono>
#include <iomanip>

int main() {
    using namespace std::chrono;
    auto now = system_clock::now();
    auto in_time_t = system_clock::to_time_t(now);

    std::locale::global(std::locale("de_DE.UTF-8"));
    std::wcout.imbue(std::locale());

    std::wcout << std::put_time(std::localtime(&in_time_t), L"%A, %d %B %Y %H:%M:%S") << std::endl;

    return 0;
}
```

## Message Translation

Message translation involves extracting strings from the source code, translating them, and then integrating them back into the application.

### GNU `gettext`

The GNU `gettext` library is commonly used for managing translations in C++ applications.

1. **Extracting Strings**:
   Mark translatable strings with the `_` macro.

    ```cpp
    #include <libintl.h>
    #define _(STRING) gettext(STRING)

    int main() {
        setlocale(LC_ALL, "");
        bindtextdomain("myapp", "/path/to/my/locale");
        textdomain("myapp");

        std::cout << _("Hello, World!") << std::endl;
        return 0;
    }
    ```

2. **Creating Translation Files**:
   Extract strings using `xgettext`, translate them, and compile them into binary `.mo` files.

## Conclusion

Internationalization in C++ involves a comprehensive approach to handle different locales, character sets, date and time formats, and message translations. By leveraging the standard library and tools like GNU `gettext`, you can create applications that are flexible and easily adaptable to various regions and languages. This not only broadens the potential user base but also ensures that your software is more inclusive and accessible.