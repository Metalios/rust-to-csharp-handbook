# 🧪 Real Project Examples

This section contains real-world Rust and C# code patterns side-by-side for common application scenarios.

---

## 1️⃣ Binary File Parsing

### Rust

```rust
use std::fs::File;
use std::io::{Read, BufReader};

fn read_header(path: &str) -> std::io::Result<[u8; 4]> {
    let file = File::open(path)?;
    let mut reader = BufReader::new(file);
    let mut buffer = [0u8; 4];
    reader.read_exact(&mut buffer)?;
    Ok(buffer)
}
```

### C#  

```csharp
using var reader = new BinaryReader(File.OpenRead("file.bin"));
byte[] buffer = reader.ReadBytes(4);
```

---

## 2️⃣ Async HTTP Client

### Rust with `reqwest`

```rust
let res = reqwest::get("https://api.example.com/data").await?;
let body = res.text().await?;
```

### C# with `HttpClient`

```csharp
var response = await httpClient.GetAsync("https://api.example.com/data");
var body = await response.Content.ReadAsStringAsync();
```

---

## 3️⃣ Command-Line App

### Rust

```rust
fn main() {
    let args: Vec<String> = std::env::args().collect();
    println!("Hello, {}", args.get(1).unwrap_or(&"World".to_string()));
}
```

### C#  

```csharp
Console.WriteLine($"Hello, {args.ElementAtOrDefault(0) ?? "World"}");
```

---

## 4️⃣ Configuration File (JSON)

### Rust

```rust
let config: Config = serde_json::from_str(&fs::read_to_string("config.json")?)?;
```

### C#  

```csharp
var config = JsonSerializer.Deserialize<Config>(File.ReadAllText("config.json"));
```

---

## 5️⃣ Background Worker / Task

### Rust

```rust
tokio::spawn(async {
    println!("Running in background...");
});
```

### C#  

```csharp
Task.Run(() => Console.WriteLine("Running in background..."));
```

---

## 🔚 Summary

| Scenario                | Rust                          | C#                              |
|-------------------------|-------------------------------|----------------------------------|
| File Parsing            | `std::fs`, `BufReader`        | `BinaryReader`, `FileStream`    |
| HTTP Client             | `reqwest`                     | `HttpClient`                    |
| CLI Args                | `std::env::args()`            | `args[]`                        |
| JSON Config             | `serde_json`                  | `System.Text.Json`              |
| Background Task         | `tokio::spawn`                | `Task.Run()`                    |

These patterns cover 80% of use cases in CLI tools, parsers, services, and utilities across both ecosystems.