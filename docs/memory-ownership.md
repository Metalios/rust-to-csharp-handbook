# 🧠 Memory and Ownership

## 🔁 Ownership & Borrowing

| Rust                       | C#                     |
|----------------------------|------------------------|
| Ownership model enforced   | GC handles memory      |
| `&T`, `&mut T` (borrows)   | `ref`, `out`, `in`     |

### 🧪 Example

```rust
fn print_length(s: &String) {
    println!("{}", s.len());
}
```

```csharp
void PrintLength(in string s) {
    Console.WriteLine(s.Length);
}
```

---

## 🗑 Drop vs Dispose

| Rust          | C#               |
|---------------|------------------|
| `Drop` trait  | `IDisposable`    |

### 🧪 Example

```rust
impl Drop for MyResource {
    fn drop(&mut self) {
        println!("Cleaning up!");
    }
}
```

```csharp
public class MyResource : IDisposable {
    public void Dispose() {
        Console.WriteLine("Cleaning up!");
    }
}
```