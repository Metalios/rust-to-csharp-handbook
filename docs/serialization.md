# 🧾 Serialization & Deserialization: Rust vs C#

Both Rust and C# provide flexible ways to serialize and deserialize data into formats like JSON, binary, and more.

---

## 🦀 Rust: `serde` Crate

### Add Dependencies

```toml
[dependencies]
serde = { version = "1.0", features = ["derive"] }
serde_json = "1.0"
```

### JSON Example

```rust
use serde::{Serialize, Deserialize};

#[derive(Serialize, Deserialize, Debug)]
struct Person {
    name: String,
    age: u8,
}

let json = r#"{"name":"Alice","age":30}"#;
let person: Person = serde_json::from_str(json)?;
println!("{:?}", person);

let output = serde_json::to_string(&person)?;
println!("{}", output);
```

---

## 💻 C#: System.Text.Json / Newtonsoft.Json

### With `System.Text.Json` (built-in since .NET Core 3.0)

```csharp
using System.Text.Json;

public class Person {
    public string Name { get; set; }
    public byte Age { get; set; }
}

var json = "{"Name":"Alice","Age":30}";
var person = JsonSerializer.Deserialize<Person>(json);
Console.WriteLine(person.Name);

var output = JsonSerializer.Serialize(person);
Console.WriteLine(output);
```

---

### With `Newtonsoft.Json` (popular library)

```bash
dotnet add package Newtonsoft.Json
```

```csharp
using Newtonsoft.Json;

var person = JsonConvert.DeserializeObject<Person>(json);
var output = JsonConvert.SerializeObject(person);
```

---

## 🧬 Binary Formats

### Rust: `bincode`

```toml
[dependencies]
bincode = "1.3"
```

```rust
let encoded: Vec<u8> = bincode::serialize(&person)?;
let decoded: Person = bincode::deserialize(&encoded)?;
```

### C#: Binary Serialization

```csharp
using System.Runtime.Serialization.Formatters.Binary;

// ⚠️ Obsolete: use protobuf, MessagePack, etc. for modern binary
```

---

## 🧠 Advanced Features

| Feature               | Rust (`serde`)       | C# (`System.Text.Json`)   |
|------------------------|----------------------|----------------------------|
| Custom field rename   | `#[serde(rename = "...")]` | `[JsonPropertyName("...")]` |
| Skipping fields       | `#[serde(skip)]`     | `[JsonIgnore]`            |
| Conditional logic     | `with`, `skip_serializing_if` | Converters / Conditionals |
| Binary formats        | `bincode`, `postcard` | `protobuf`, `MessagePack` |
| Field defaults        | `#[serde(default)]`  | `[JsonIgnore(Condition = ...)]` |

---

## ✅ Summary

| Task                 | Rust                     | C#                          |
|----------------------|--------------------------|-----------------------------|
| JSON support         | `serde_json`             | `System.Text.Json` or `Newtonsoft.Json` |
| Binary support       | `bincode`, `postcard`    | `BinaryFormatter`, `protobuf`, etc.     |
| Field annotations    | `#[serde(...)]`          | `[JsonPropertyName]`, `[JsonIgnore]`    |
| Common usage         | `derive(Serialize)`      | POCO classes, `JsonSerializer` API      |

Rust gives you fine-grained control through macros and derive annotations, while C# offers integrated JSON support with attribute-driven customization.