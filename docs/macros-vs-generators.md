# 🧱 Macros vs Source Generators: Rust vs C#

Rust macros and C# source generators both provide **compile-time code generation**, but they operate differently and serve different use cases.

---

## 🦀 Rust Macros

### Declarative Macros (`macro_rules!`)

```rust
macro_rules! say_hello {
    () => {
        println!("Hello!");
    };
}

say_hello!();
```

### Procedural Macros

```rust
#[derive(Debug)]
struct Point {
    x: i32,
    y: i32,
}
```

Uses a `#[proc_macro_derive(Debug)]` in an external crate.

---

## 💻 C# Source Generators (Roslyn)

Introduced in .NET 5+, these allow generating code **during compilation**.

### Simple Example

```csharp
[MyAutoNotify]
public partial class Person
{
    private string name;
}
```

This uses a source generator that emits:

```csharp
public string Name
{
    get => name;
    set => SetProperty(ref name, value);
}
```

---

## ⚙️ Comparison Table

| Feature                    | Rust                           | C#                                  |
|----------------------------|--------------------------------|-------------------------------------|
| Declarative Macros         | `macro_rules!`                 | N/A                                 |
| Procedural Macros          | `#[proc_macro]`, `#[derive]`   | `ISourceGenerator`                  |
| Scope                      | File/crate level               | Assembly level                      |
| Runtime Use?               | No (compile-time only)         | No (compile-time only)              |
| IDE Support                | Often limited                  | Full IntelliSense + preview         |
| Use Cases                  | DSLs, Derive, function wrappers| Auto-properties, DTOs, validations  |

---

## 🔧 Use Cases

| Scenario                        | Rust                           | C#                                   |
|----------------------------------|----------------------------------|--------------------------------------|
| Auto Traits                     | `#[derive(Debug)]`               | `[AutoGenerateToString]`             |
| DSL Construction                | `macro_rules! html {}`          | ✖ (Manual or external tooling)       |
| Reflection-free serialization   | `serde::Serialize`              | `System.Text.Json.SourceGenerator`   |
| Compile-time code validation    | `proc_macro_attribute`          | `ISourceGenerator` + analyzer        |

---

## 🚧 Limitations

- Rust macros are more **flexible**, but harder to debug and IDEs may struggle
- C# source generators are more **structured**, but limited to supported APIs

---

## 📝 Summary

| Rust                     | C#                                  |
|--------------------------|--------------------------------------|
| `macro_rules!`           | Not available                        |
| `#[derive()]`, `#[proc_macro]` | `[Attribute]` + `partial class` + `ISourceGenerator` |
| Compile-time only        | ✅                                    | ✅                                    |

Both systems aim to reduce boilerplate and increase code clarity, but Rust takes a more syntax-level metaprogramming approach, while C# leans on structured Roslyn APIs.