# 🔌 FFI & Interop: Rust ↔ C#

Rust and C# can interoperate with each other and with C libraries using FFI (Foreign Function Interface) and platform interop mechanisms.

---

## 🦀 Rust: Exposing a C-compatible API

### Exporting Functions from Rust

```rust
#[no_mangle]
pub extern "C" fn add(x: i32, y: i32) -> i32 {
    x + y
}
```

- `#[no_mangle]` disables Rust name mangling
- `extern "C"` uses the C calling convention

### Compiling as a Dynamic Library

```toml
[lib]
crate-type = ["cdylib"]
```

Build with:

```bash
cargo build --release
```

This produces `.dll`, `.so`, or `.dylib` depending on platform.

---

## 💻 C#: Importing from Rust DLL

```csharp
using System.Runtime.InteropServices;

class NativeMethods {
    [DllImport("mylib.dll", CallingConvention = CallingConvention.Cdecl)]
    public static extern int add(int x, int y);
}
```

Call it:

```csharp
Console.WriteLine(NativeMethods.add(2, 3)); // Outputs: 5
```

---

## 🔁 Passing Strings

### Rust: Exporting a Function with a String

```rust
#[no_mangle]
pub extern "C" fn greet(ptr: *const u8, len: usize) {
    let slice = unsafe { std::slice::from_raw_parts(ptr, len) };
    let input = std::str::from_utf8(slice).unwrap();
    println!("Hello, {}", input);
}
```

### C#: Marshaling a UTF-8 String

```csharp
var bytes = Encoding.UTF8.GetBytes("Rusty");
unsafe {
    fixed (byte* ptr = bytes) {
        greet((IntPtr)ptr, bytes.Length);
    }
}
```

---

## 🧠 Interop Tips

| Concept              | Rust                          | C#                                |
|----------------------|-------------------------------|------------------------------------|
| Basic Function       | `extern "C" fn`               | `[DllImport(...)]`                 |
| Structs              | `#[repr(C)] struct`           | `[StructLayout(LayoutKind.Sequential)]` |
| String Passing       | `*const u8` + length          | `IntPtr` + `byte[]`                |
| Arrays               | Raw pointers (`*const T`)     | `Span<T>`, `IntPtr`, `fixed`       |
| Cleanup              | Manual free required          | `Marshal.FreeHGlobal` or manual    |

---

## 📤 Calling C# from Rust (via C)

This is harder and usually involves:
- Creating a C ABI from C#
- Calling via COM interop, C++/CLI, or hosting CLR manually

For most use cases, Rust → C# is easier than the reverse.

---

## 🔒 Memory Safety Warnings

- You must **manage memory manually** across the FFI boundary.
- Rust can **safely handle** `unsafe` code, but you must enforce it yourself.
- Avoid allocating or deallocating across boundaries unless both sides agree.

---

## 📝 Summary

| Direction     | Method                              |
|---------------|--------------------------------------|
| Rust → C#     | Export Rust as `cdylib`, use `DllImport` in C# |
| C# → Rust     | Much harder — via C wrapper or COM   |
| Safe Types    | Integers, structs, pointers, UTF-8   |
| Avoid         | Passing heap-allocated strings or objects directly |

FFI is powerful but sharp — test thoroughly and use stable interfaces across language boundaries.