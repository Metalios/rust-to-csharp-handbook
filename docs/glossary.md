# 📘 Glossary & Quick Reference: Rust → C#

This section provides a fast lookup table for translating Rust concepts, syntax, and types into their C# equivalents.

---

## 🔤 Types

| Rust               | C#                       |
|--------------------|--------------------------|
| `i32`, `u32`       | `int`, `uint`            |
| `i64`, `u64`       | `long`, `ulong`          |
| `f32`, `f64`       | `float`, `double`        |
| `bool`             | `bool`                   |
| `char`             | `char` (Unicode scalar)  |
| `String` / `&str`  | `string`                 |
| `Option<T>`        | `T?`, `Nullable<T>`      |
| `Result<T, E>`     | `try/catch`, custom types|
| `Vec<T>`           | `List<T>`                |
| `HashMap<K, V>`    | `Dictionary<K, V>`       |

---

## 🧱 Structs & Enums

| Rust                     | C#                          |
|--------------------------|-----------------------------|
| `struct`                 | `class` or `struct`         |
| `enum` (algebraic types) | `record`, `discriminated union` (manual) |
| `#[derive(Debug)]`       | `ToString()` or source generator |
| `impl Struct`            | C# methods in class         |

---

## 🧩 Traits & Interfaces

| Rust               | C#                      |
|--------------------|-------------------------|
| `trait`            | `interface`             |
| `impl Trait for T` | `class : Interface`     |
| `Default`, `Clone` | `IDisposable`, `ICloneable`, etc. |
| Trait bounds       | `where T : Interface`   |

---

## 🧮 Collections

| Rust                   | C#                         |
|------------------------|----------------------------|
| `Vec<T>`               | `List<T>`                  |
| `HashMap<K, V>`        | `Dictionary<K, V>`         |
| `.iter().map()`        | `.Select()` (LINQ)         |
| `.filter()`            | `.Where()` (LINQ)          |
| `.collect()`           | `.ToList()`, `.ToArray()`  |

---

## 🔁 Control Flow

| Rust           | C#                     |
|----------------|------------------------|
| `if`, `else`   | `if`, `else`           |
| `match`        | `switch`               |
| `loop {}`      | `while (true)`         |
| `for x in y`   | `foreach (var x in y)` |
| `while`, `break`, `continue` | same     |

---

## 🧠 Error Handling

| Rust                 | C#                         |
|----------------------|----------------------------|
| `Result<T, E>`       | `try/catch` or `OneOf<T,E>`|
| `?` operator         | `throw;` / unwrap pattern  |
| `panic!()`           | `throw Exception`          |

---

## 📦 Project Structure & Tooling

| Rust (Cargo)     | C# (.NET CLI)         |
|------------------|------------------------|
| `Cargo.toml`     | `.csproj`, `.sln`      |
| `cargo build`    | `dotnet build`         |
| `cargo test`     | `dotnet test`          |
| `cargo run`      | `dotnet run`           |
| `cargo fmt`      | `dotnet format`        |

---

## 🚀 Async & Threads

| Rust                  | C#                          |
|-----------------------|-----------------------------|
| `async fn`, `.await`  | `async Task`, `await`       |
| `tokio::spawn`        | `Task.Run(...)`             |
| `thread::spawn`       | `new Thread(...).Start()`   |
| `Arc<Mutex<T>>`       | `lock`, `SemaphoreSlim`, etc. |

---

## 📝 Summary Cheat Sheet

| Rust Concept       | C# Equivalent             |
|--------------------|---------------------------|
| `trait`            | `interface`               |
| `Option<T>`        | `T?` or `Nullable<T>`     |
| `Result<T, E>`     | `try/catch` or wrapper    |
| `match`            | `switch` with patterns    |
| `macro_rules!`     | Source Generator / Helper |
| `Cargo.toml`       | `.csproj` / NuGet         |

Use this glossary for quick reference while translating or porting code from Rust to C#.