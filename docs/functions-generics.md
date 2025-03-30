# 📦 Functions & Generics

## 🛠 Functions

| Rust Function                      | C# Equivalent                |
|------------------------------------|------------------------------|
| `fn add(x: i32, y: i32) -> i32`    | `int Add(int x, int y)`     |

### 🧪 Example

```rust
fn add(x: i32, y: i32) -> i32 {
    x + y
}
```

```csharp
int Add(int x, int y) {
    return x + y;
}
```

---

## 🔣 Generics

| Rust                          | C#                          |
|-------------------------------|-----------------------------|
| `fn generic<T>(x: T)`         | `void Generic<T>(T x)`      |

### 🧪 Example

```rust
fn echo<T: std::fmt::Debug>(x: T) {
    println!("{:?}", x);
}
```

```csharp
void Echo<T>(T x) {
    Console.WriteLine(x);
}
```

---

## 📏 Trait Bounds in Generics

### Rust

```rust
fn print_debug<T: std::fmt::Debug>(x: T) {
    println!("{:?}", x);
}
```

### C#

```csharp
void Print<T>(T x) where T : IFormattable {
    Console.WriteLine(x);
}
```

---

## 🔁 Functional Equivalents

### C# Delegates

```csharp
Func<int, int> square = x => x * x;
Action<string> shout = msg => Console.WriteLine(msg);
```