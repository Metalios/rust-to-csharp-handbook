# 🚀 Async & Concurrency

## 🔁 async/await

| Rust                         | C#                        |
|------------------------------|---------------------------|
| `async fn foo()`             | `async Task Foo()`        |
| `.await`                     | `.Await()`                |

### 🧪 Example

```rust
async fn say_hi() {
    println!("Hi!");
}
```

```csharp
async Task SayHi() {
    Console.WriteLine("Hi!");
}
```

---

## 🧵 Spawning Tasks

```rust
tokio::spawn(async {
    do_work().await;
});
```

```csharp
Task.Run(async () => await DoWork());
```