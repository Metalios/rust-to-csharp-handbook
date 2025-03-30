# 🧭 Modules & Namespaces

## 🧱 Structure

| Rust                     | C#                        |
|--------------------------|---------------------------|
| `mod foo;`               | file-based or namespace   |
| `use crate::foo::bar;`   | `using Foo.Bar;`          |

### 🧪 Example

```rust
mod math {
    pub fn add(x: i32, y: i32) -> i32 {
        x + y
    }
}
```

```csharp
namespace Math {
    public static class Operations {
        public static int Add(int x, int y) => x + y;
    }
}
```