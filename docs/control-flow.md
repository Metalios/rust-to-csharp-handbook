# 🔁 Control Flow

Compare how conditional logic and loops are expressed in Rust vs C#.

## 🔍 Conditionals

| Rust                     | C#                   |
|--------------------------|----------------------|
| `if x > 5 {}`            | `if (x > 5) {}`      |

### 🧪 Example

```rust
if x > 5 {
    println!("x is large!");
}
```

```csharp
if (x > 5)
{
    Console.WriteLine("x is large!");
}
```

---

## 🔁 Loops

| Rust                       | C#                           |
|----------------------------|------------------------------|
| `for i in 0..10 {}`        | `for (int i = 0; i < 10; i++)`|

### 🧪 Example

```rust
for i in 0..3 {
    println!("{}", i);
}
```

```csharp
for (int i = 0; i < 3; i++) {
    Console.WriteLine(i);
}
```

---

## 🔁 Additional Control Flow

### 🧪 `while` Loop

```rust
let mut i = 0;
while i < 5 {
    println!("{}", i);
    i += 1;
}
```

```csharp
int i = 0;
while (i < 5) {
    Console.WriteLine(i);
    i++;
}
```

### 🧪 Infinite Loop

```rust
loop {
    println!("looping forever");
}
```

```csharp
while (true) {
    Console.WriteLine("looping forever");
}
```