# 📚 Collections & Iterators

## 📦 Common Types

| Rust             | C#                 |
|------------------|--------------------|
| `Vec<T>`         | `List<T>`          |
| `HashMap<K, V>`  | `Dictionary<K,V>`  |

---

## 🔁 Iterators

| Rust                      | C#                   |
|---------------------------|----------------------|
| `vec.iter()`              | `list.Select(...)`   |
| `filter()`, `map()`       | `Where()`, `Select()`|

### 🧪 Example

```rust
let nums = vec![1, 2, 3];
let doubled: Vec<i32> = nums.iter().map(|x| x * 2).collect();
```

```csharp
var nums = new List<int> { 1, 2, 3 };
var doubled = nums.Select(x => x * 2).ToList();
```