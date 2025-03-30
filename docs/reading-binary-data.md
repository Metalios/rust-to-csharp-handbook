# 🔢 Reading Binary Data: Rust vs C#

Reading binary data is a common task in both systems programming (Rust) and application development (C#). This guide maps syntax, patterns, and techniques between the two languages.

---

## 📄 File Reading Setup

| Task           | Rust                                  | C#                                  |
|----------------|---------------------------------------|-------------------------------------|
| Open a file    | `let file = File::open(path)?;`       | `var stream = new FileStream(path, FileMode.Open);` |
| Buffered read  | `let mut reader = BufReader::new(file);` | `var reader = new BinaryReader(stream);` |
| Traits needed  | `T: Read + Seek`                      | `Stream`/`BinaryReader` supports all |

---

## 🔢 Reading Primitive Types

### 📦 Rust (with `byteorder` or `binread`)
```rust
use byteorder::{ReadBytesExt, LittleEndian};

let val = reader.read_u32::<LittleEndian>()?;
let val = reader.read_i16::<LittleEndian>()?;
```

### 🧠 'C#'
```csharp
uint val = reader.ReadUInt32();
short val = reader.ReadInt16();
```

---

## 📏 Endianness

| Rust                                      | C#                                            |
|-------------------------------------------|-----------------------------------------------|
| `LittleEndian`, `BigEndian` from `byteorder` | No built-in: use `BinaryPrimitives`, `BitConverter` |
| Specify endianness per read              | Must swap bytes manually                      |

### 📦 'C#' Manual Example (BigEndian)
```csharp
byte[] bytes = reader.ReadBytes(4);
int val = BitConverter.ToInt32(bytes.Reverse().ToArray());
```

---

## 🧵 Reading Strings

### 📦 Rust
```rust
// Null-terminated string
let mut buf = Vec::new();
reader.read_until(0, &mut buf)?;
let s = String::from_utf8_lossy(&buf[..buf.len()-1]).to_string();
```

### 🧠 'C#'
```csharp
// Null-terminated string
List<byte> bytes = new();
byte b;
while ((b = reader.ReadByte()) != 0)
    bytes.Add(b);
string s = Encoding.UTF8.GetString(bytes.ToArray());
```

---

## 🧱 Reading Arrays and Structs

### 📦 Rust
```rust
let mut arr = [0u8; 16];
reader.read_exact(&mut arr)?;
```

### 🧠 'C#'
```csharp
byte[] arr = reader.ReadBytes(16);
```

### Reading a Struct Manually

#### Rust
```rust
let x = reader.read_u32::<LittleEndian>()?;
let y = reader.read_f32::<LittleEndian>()?;
```

### C#
```csharp
uint x = reader.ReadUInt32();
float y = reader.ReadSingle();
```

---

## 🧩 Seeking in Streams

| Rust                             | C#                                  |
|----------------------------------|-------------------------------------|
| `reader.seek(SeekFrom::Start(n))`| `stream.Seek(n, SeekOrigin.Begin);` |
| `SeekFrom::Current(n)`           | `SeekOrigin.Current`                |

---

## 🧠 Binary Parsing Tips

| Task                          | Rust                             | C#                                |
|-------------------------------|----------------------------------|-----------------------------------|
| Validate struct size          | Manual or `binread`              | Use offset math or span validation |
| Skip bytes                    | `reader.seek(SeekFrom::Current(n))` | `reader.BaseStream.Seek(n, SeekOrigin.Current);` |
| Read into model               | Field-by-field assignment        | Use method or custom parser class |

---

## 🔁 Reusable Binary Readers

### Rust Trait-Based

```rust
pub trait BinReadable {
    fn read(reader: &mut impl Read) -> Result<Self, Error> where Self: Sized;
}
```

### C# Interface-Based

```csharp
public interface IBinaryReadable {
    void ReadFrom(BinaryReader reader);
}
```

---

## 🧪 Example: Reading a Custom Header

### Rust
```rust
let magic = reader.read_u32::<LittleEndian>()?;
let version = reader.read_u16::<LittleEndian>()?;
```

### C#
```csharp
uint magic = reader.ReadUInt32();
ushort version = reader.ReadUInt16();
```

---

## ✅ Summary

| Concept           | Rust                          | C#                              |
|-------------------|-------------------------------|---------------------------------|
| Binary Reader     | `Read + Seek`                 | `BinaryReader`                 |
| Endianness        | `byteorder`, `binread`        | Manual or `BitConverter`       |
| Strings           | `read_until(0)`               | Loop until byte == 0           |
| Arrays            | `read_exact()`                | `ReadBytes(n)`                 |
| Structs           | Manual or macro-derived       | Manual or `IBinaryReadable`    |

This page serves as a reference for building binary file readers, game data parsers, and stream-based processing across Rust and C#.