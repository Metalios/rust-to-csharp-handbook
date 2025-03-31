# 🎭 Pattern Matching: Rust vs C#

Rust and C# both support powerful pattern matching, but with very different syntax and paradigms.

---

## 🔁 Basic `match` vs `switch`

### Rust

```rust
let value = 3;
match value {
    1 => println!("One"),
    2 | 3 => println!("Two or Three"),
    4..=10 => println!("Between four and ten"),
    _ => println!("Something else"),
}
```

### C#  

```csharp
int value = 3;
switch (value)
{
    case 1:
        Console.WriteLine("One");
        break;
    case 2 or 3:
        Console.WriteLine("Two or Three");
        break;
    case >= 4 and <= 10:
        Console.WriteLine("Between four and ten");
        break;
    default:
        Console.WriteLine("Something else");
        break;
}
```

---

## 🧩 Matching Enums

### Rust

```rust
enum Message {
    Quit,
    Move { x: i32, y: i32 },
}

let msg = Message::Move { x: 5, y: 10 };

match msg {
    Message::Quit => println!("Quit"),
    Message::Move { x, y } => println!("Move to ({}, {})", x, y),
}
```

### C#  

```csharp
public record Message;

public record Quit : Message;
public record Move(int X, int Y) : Message;

Message msg = new Move(5, 10);

switch (msg)
{
    case Quit:
        Console.WriteLine("Quit");
        break;
    case Move(var x, var y):
        Console.WriteLine($"Move to ({x}, {y})");
        break;
}
```

---

## ❓ Matching with `if` Conditions

### Rust

```rust
let number = Some(7);

if let Some(x) = number {
    println!("Found: {}", x);
}
```

### C#  

```csharp
int? number = 7;

if (number is int x) {
    Console.WriteLine($"Found: {x}");
}
```

---

## 🧠 `when` Clauses in C#  

```csharp
switch (value)
{
    case int x when x % 2 == 0:
        Console.WriteLine("Even");
        break;
    case int x:
        Console.WriteLine("Odd");
        break;
}
```

Rust doesn’t have this built-in, but you can use guards:

```rust
match value {
    x if x % 2 == 0 => println!("Even"),
    _ => println!("Odd"),
}
```

---

## ✅ Summary

| Concept                 | Rust (`match`)                   | C# (`switch` + `is` + `when`)         |
|-------------------------|----------------------------------|----------------------------------------|
| Pattern Matching        | `match` expression               | `switch` statement                     |
| Range Patterns          | `4..=10`                         | `>= 4 and <= 10`                       |
| Enum Destructuring      | `Enum::Variant { fields }`       | `record` matching with properties      |
| Condition Matching      | `x if condition`                 | `when` clause                          |
| Nullable Matching       | `if let Some(x)`                 | `if (obj is T x)`                      |

Pattern matching is deeply embedded into Rust’s design, while C# is catching up with modern pattern features in .NET 8.