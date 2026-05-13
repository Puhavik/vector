# Vector (Header-only C++ Dynamic Array)

A lightweight educational implementation of a dynamic array container in modern C++.

This repository provides a templated `Vector<T>` class in a single header file (`vector.h`) with core functionality similar to `std::vector`, including:

- Dynamic storage management
- Element access via `operator[]`
- Capacity management (`reserve`, `shrink_to_fit`)
- Modifiers (`push_back`, `pop_back`, `insert`, `erase`, `clear`)
- Forward iteration with custom `Iterator` and `ConstIterator`
- Stream output via `operator<<`

> **Note:** This project is best suited for learning and experimentation. It is not a drop-in replacement for `std::vector` in production code.

---

## Repository structure

```text
.
├── vector.h    # Full implementation of Vector<T>
└── README.md
```

---

## Requirements

- C++ compiler with C++11 (or newer) support
  - `g++`, `clang++`, or MSVC

---

## Quick start

Create a file `main.cpp`:

```cpp
#include <iostream>
#include "vector.h"

int main() {
    Vector<int> v{1, 2, 3};

    v.push_back(4);
    auto it = v.begin();
    ++it;
    v.insert(it, 99);
    v.erase(v.begin());

    std::cout << "Vector: " << v;
    std::cout << "Size: " << v.size() << "\n";
    std::cout << "Capacity: " << v.capacity() << "\n";

    for (const auto& x : v) {
        std::cout << x << ' ';
    }
    std::cout << '\n';
}
```

Compile and run:

```bash
g++ -std=c++11 -O2 -Wall -Wextra -pedantic main.cpp -o app
./app
```

---

## API overview

### Constructors

- `Vector()`
- `Vector(size_t n)`
- `Vector(std::initializer_list<T>)`
- `Vector(const Vector&)`

### Capacity / state

- `size() const`
- `capacity() const`
- `empty() const`
- `clear()`
- `reserve(size_t n)`
- `shrink_to_fit()`

### Element access

- `operator[](size_t)`
- `operator[](size_t) const`

### Modifiers

- `push_back(T)`
- `pop_back()`
- `insert(const_iterator pos, const T& value)`
- `erase(const_iterator pos)`

### Iteration

- `begin()`, `end()`
- `begin() const`, `end() const`

### Output

- `operator<<(std::ostream&, const Vector<T>&)`

---

## Design notes

- **Header-only:** no build system is required.
- **Template-based:** works with any type that supports the used operations.
- **Manual memory management:** educational visibility into dynamic allocation mechanics.

---

## Known caveats

As this is an educational implementation, there are behavioral differences from `std::vector` and edge cases to consider:

- `vector.h` uses `using namespace std;`, which is generally discouraged in headers.
- Bounds checks and capacity behavior differ from standard-library semantics.
- Exception safety and allocator customizability are limited.
- Some iterator and growth behavior may vary by compiler and usage patterns.

If you need full standards-compliant behavior, prefer `std::vector`.

---

## Suggested improvements

If you want to evolve this project, good next steps include:

1. Remove `using namespace std;` from the header.
2. Rework reallocation logic and growth strategy.
3. Add move constructor / move assignment.
4. Add `at()` with strict bounds checks.
5. Improve exception safety (copy-and-swap, strong guarantees where possible).
6. Add unit tests (e.g., with Catch2 or GoogleTest).

---

## License

No license file is currently included.
If you plan to share or reuse this code publicly, add an explicit license (for example, MIT or Apache-2.0).
