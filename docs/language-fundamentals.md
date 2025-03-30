# 🔤 Language Fundamentals

This section compares core variable declarations, constants, and types in Rust and C#.

## 🔧 Variables

| Rust           | C#                  |
|----------------|---------------------|
| `let x = 5;`   | `var x = 5;`        |
| `let mut x = 5;` | `int x = 5;`      |

### 🧪 Example

```rust
let x = 10;
let y = x + 5;
```

```csharp
var x = 10;
var y = x + 5;
```

---

## 🔐 Constants

| Rust                             | C#                           |
|----------------------------------|------------------------------|
| `const MAX: usize = 100;`        | `const int MAX = 100;`       |

---

## 🧠 Type Annotations

| Rust               | C#                     |
|--------------------|------------------------|
| `let x: f32 = 5.0;`| `float x = 5.0f;`      |

---

---

## 📝 Extra Notes

- Rust allows **shadowing**, meaning you can `let x = 1; let x = x + 1;`
- You can use suffixes in Rust like `5.0f32`, `42u32` to specify type literals directly