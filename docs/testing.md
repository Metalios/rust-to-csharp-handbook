# 🧪 Testing

## 🔍 Unit Tests

| Rust                     | C#                            |
|--------------------------|-------------------------------|
| `#[test]`                | `[TestMethod]` or `[Fact]`    |
| `assert_eq!(a, b)`       | `Assert.AreEqual(a, b)`       |

### 🧪 Example

```rust
#[test]
fn it_adds() {
    assert_eq!(2 + 2, 4);
}
```

```csharp
[TestMethod]
public void ItAdds() {
    Assert.AreEqual(4, 2 + 2);
}
```

---

## 🧪 Exception Testing

### Rust

```rust
#[test]
#[should_panic(expected = "division by zero")]
fn it_panics() {
    let _ = 1 / 0;
}
```

### C#

```csharp
[Fact]
public void ItPanics() {
    Assert.Throws<DivideByZeroException>(() => {
        var x = 1 / 0;
    });
}
```

## 🔍 Capturing Output in Rust

```bash
cargo test -- --nocapture
```