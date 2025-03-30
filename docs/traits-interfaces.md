# 🧩 Traits vs Interfaces

## 🧩 Interface Definition

| Rust                      | C#                      |
|---------------------------|-------------------------|
| `trait Drawable { ... }`  | `interface IDrawable {}`|

### 🧪 Example

```rust
trait Drawable {
    fn draw(&self);
}
```

```csharp
public interface IDrawable {
    void Draw();
}
```

---

## 🛠 Implementation

| Rust                            | C#                             |
|---------------------------------|--------------------------------|
| `impl Drawable for Circle {}`   | `class Circle : IDrawable {}` |

### 🧪 Example

```rust
struct Circle;

impl Drawable for Circle {
    fn draw(&self) {
        println!("Drawing circle!");
    }
}
```

```csharp
public class Circle : IDrawable {
    public void Draw() {
        Console.WriteLine("Drawing circle!");
    }
}
```