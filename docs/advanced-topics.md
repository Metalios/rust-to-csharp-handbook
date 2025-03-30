# ⚙️ Advanced Topics

## 🔒 Unsafe Code

| Rust             | C#             |
|------------------|----------------|
| `unsafe {}`      | `unsafe {}`    |
| `*const T`       | `T*`           |

### 🧪 Example

```rust
unsafe {
    let ptr = &10 as *const i32;
    println!("{}", *ptr);
}
```

```csharp
unsafe {
    int x = 10;
    int* ptr = &x;
    Console.WriteLine(*ptr);
}
```

---

## 🧠 Macros

Rust:
```rust
macro_rules! say_hello {
    () => { println!("Hello!") };
}
```

C#: use Roslyn source generators or code snippets.