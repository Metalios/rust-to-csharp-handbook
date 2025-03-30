# 💥 Error Handling

## ✅ Result / Option

| Rust                     | C#                                 |
|--------------------------|------------------------------------|
| `Result<T, E>`           | `Result<T>` or try/catch           |
| `Option<T>`              | Nullable types / Optional<T>       |

### 🧪 Example

```rust
fn divide(x: i32, y: i32) -> Result<i32, String> {
    if y == 0 {
        Err("division by zero".to_string())
    } else {
        Ok(x / y)
    }
}
```

```csharp
int Divide(int x, int y) {
    if (y == 0) throw new DivideByZeroException();
    return x / y;
}
```

---

## 🚨 Panic vs Exception

```rust
panic!("Unexpected error!");
```

```csharp
throw new Exception("Unexpected error!");
```