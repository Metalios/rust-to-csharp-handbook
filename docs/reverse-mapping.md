# 🔁 From C# to Rust: Reverse Concept Mapping

This section helps .NET developers understand how to translate familiar C# constructs into idiomatic Rust.

---

## 🧠 Primitives & Types

| C#            | Rust               |
|---------------|--------------------|
| `int`         | `i32`              |
| `long`        | `i64`              |
| `float`       | `f32`              |
| `double`      | `f64`              |
| `string`      | `String`, `&str`   |
| `bool`        | `bool`             |
| `List<T>`     | `Vec<T>`           |
| `Dictionary<K,V>` | `HashMap<K,V>` |

---

## 🧱 Classes, Structs, Enums

| C#                        | Rust                        |
|---------------------------|-----------------------------|
| `class`                   | `struct` or `enum`          |
| `struct` (value type)     | `#[derive(...)] struct`     |
| `record`                  | `enum` or `struct` with traits |
| `readonly struct`         | `Copy` + `Clone` trait      |

---

## 🧩 Interfaces and Inheritance

| C#                         | Rust                     |
|----------------------------|--------------------------|
| `interface`                | `trait`                  |
| `implements`               | `impl Trait for Struct`  |
| Multiple interfaces        | Multiple trait impls     |
| Virtual methods            | Trait + default method   |

---

## 🔁 Control Flow

| C#                        | Rust                   |
|---------------------------|------------------------|
| `switch`, `when`          | `match`                |
| `if`, `else`              | `if`, `else`           |
| `foreach`                 | `for x in y`           |
| `while`                   | `while`                |
| `try`, `catch`, `finally` | `Result<T, E>`, `?` operator |

---

## 🧮 Nullable & Optionals

| C#                  | Rust            |
|---------------------|-----------------|
| `T?`                | `Option<T>`     |
| `null`              | `None`          |
| `HasValue` / `.Value` | `is_some()`, `.unwrap()` |

---

## 🧠 Exceptions and Errors

| C#                         | Rust                       |
|----------------------------|----------------------------|
| `try/catch`                | `Result<T, E>` + `?`       |
| `throw new Exception()`    | `panic!()` or `Err(...)`   |
| `using` or `IDisposable`   | `Drop` trait               |

---

## 🚀 Async and Concurrency

| C#                     | Rust                          |
|------------------------|-------------------------------|
| `async Task<T>`        | `async fn -> T`               |
| `await`                | `.await`                      |
| `Task.Run()`           | `tokio::spawn()`              |
| `lock(obj)`            | `Arc<Mutex<T>>`               |
| `Thread t = new()`     | `std::thread::spawn()`        |

---

## ⚙️ Project & Build System

| C# (.NET)              | Rust                    |
|------------------------|--------------------------|
| `.csproj`              | `Cargo.toml`             |
| `dotnet build`         | `cargo build`            |
| `dotnet test`          | `cargo test`             |
| `dotnet run`           | `cargo run`              |
| NuGet                  | `crates.io`              |

---

## 📝 Summary

| C# Concept         | Rust Equivalent         |
|--------------------|--------------------------|
| `interface`        | `trait`                  |
| `List<T>`          | `Vec<T>`                 |
| `T?`               | `Option<T>`              |
| `try/catch`        | `Result<T, E>`           |
| `Task<T>`          | `async fn -> T`          |
| `DllImport`        | `extern "C"` + `#[no_mangle]` |

This reverse map is ideal for .NET developers starting their Rust journey.