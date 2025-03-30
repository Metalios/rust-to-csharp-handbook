# 📝 Writing Binary Data: Rust vs C#

This guide compares techniques for writing binary data to files and streams in Rust and C#, including primitives, arrays, strings, and structs.

---

## 🗂 File Writer Setup

| Rust                                | C#                                 |
|-------------------------------------|------------------------------------|
| `let file = File::create(path)?;`   | `var stream = new FileStream(path, FileMode.Create);` |
| `let mut writer = BufWriter::new(file);` | `var writer = new BinaryWriter(stream);` |

---

## 🔢 Writing Primitive Types

### 🦀 Rust

```rust
use byteorder::{WriteBytesExt, LittleEndian};

writer.write_u32::<LittleEndian>(42)?;
writer.write_f32::<LittleEndian>(3.14)?;
```

### 💻 'C#'

```csharp
writer.Write((uint)42);
writer.Write(3.14f);
```

---

## 📏 Writing With Endianness

| Rust                         | C#                            |
|------------------------------|-------------------------------|
| Uses `byteorder` crate       | Must reverse bytes manually   |

### 💡 'C#' BigEndian Example

```csharp
byte[] bytes = BitConverter.GetBytes(42);
Array.Reverse(bytes); // BigEndian
writer.Write(bytes);
```

---

## 🧵 Writing Strings

| Format              | Rust                      | C#                          |
|---------------------|---------------------------|-----------------------------|
| Null-terminated     | Write UTF-8 then `0` byte | Encode + Write + WriteByte |
| Pascal-style        | Prefix length (u8/u16)    | Write length + bytes       |

### 🦀 Rust (null-terminated)

```rust
writer.write_all("Hello".as_bytes())?;
writer.write_u8(0)?;
```

### 💻 'C#' (null-terminated)

```csharp
writer.Write(Encoding.UTF8.GetBytes("Hello"));
writer.Write((byte)0);
```

---

## 🧱 Writing Arrays and Structs

### 🦀 Rust

```rust
let data = [1u8, 2, 3, 4];
writer.write_all(&data)?;
```

### 💻 'C#'

```csharp
byte[] data = { 1, 2, 3, 4 };
writer.Write(data);
```

---

## 🧩 Writing a Custom Struct

### Rust

```rust
struct Header {
    id: u32,
    version: u16,
}

impl Header {
    fn write_to(&self, w: &mut impl Write) -> std::io::Result<()> {
        w.write_u32::<LittleEndian>(self.id)?;
        w.write_u16::<LittleEndian>(self.version)?;
        Ok(())
    }
}
```

### C#

```csharp
struct Header {
    public uint Id;
    public ushort Version;

    public void WriteTo(BinaryWriter writer) {
        writer.Write(Id);
        writer.Write(Version);
    }
}
```

---

## 🧪 Full Example

### Rust

```rust
let mut file = BufWriter::new(File::create("data.bin")?);
file.write_u32::<LittleEndian>(0xDEADBEEF)?;
file.write_all(b"DATA")?;
file.write_u8(0)?;
```

### C#

```csharp
using var fs = new FileStream("data.bin", FileMode.Create);
using var writer = new BinaryWriter(fs);
writer.Write(0xDEADBEEF);
writer.Write(Encoding.ASCII.GetBytes("DATA"));
writer.Write((byte)0);
```

---

## ✅ Summary

| Task               | Rust                                | C#                                 |
|--------------------|-------------------------------------|-------------------------------------|
| Create writer      | `BufWriter::new(File::create(...))` | `new BinaryWriter(FileStream)`      |
| Write primitive    | `write_u32::<LE>(val)`              | `writer.Write(val)`                 |
| Endianness         | `byteorder` crate                   | Manual byte swap                    |
| Write string       | `write_all() + 0`                   | `Write(bytes) + Write((byte)0)`     |
| Write struct       | Implement `write_to()`              | Define `WriteTo(BinaryWriter)`      |

This section helps you build binary file serializers, network packets, or game data writers across Rust and C#.