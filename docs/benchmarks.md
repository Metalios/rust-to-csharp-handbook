# ⏱️ Benchmarks & Performance Testing: Rust vs C#

Both Rust and C# support benchmarking frameworks to help you measure performance accurately and reproducibly.

---

## 🦀 Rust: `cargo bench` with Criterion

### Setup with Criterion

Add to `Cargo.toml`:

```toml
[dev-dependencies]
criterion = "0.5"
```

### Example

```rust
use criterion::{criterion_group, criterion_main, Criterion};

fn fibonacci(n: u64) -> u64 {
    match n {
        0 => 1,
        1 => 1,
        n => fibonacci(n - 1) + fibonacci(n - 2),
    }
}

fn bench_fib(c: &mut Criterion) {
    c.bench_function("fib 20", |b| b.iter(|| fibonacci(20)));
}

criterion_group!(benches, bench_fib);
criterion_main!(benches);
```

Run with:

```bash
cargo bench
```

---

## 💻 C#: BenchmarkDotNet

### Setup

Add NuGet package:

```bash
dotnet add package BenchmarkDotNet
```

### Example

```csharp
using BenchmarkDotNet.Attributes;
using BenchmarkDotNet.Running;

public class FibonacciBenchmarks
{
    [Benchmark]
    public int Fibonacci20() => Fibonacci(20);

    public int Fibonacci(int n) =>
        n switch
        {
            0 => 1,
            1 => 1,
            _ => Fibonacci(n - 1) + Fibonacci(n - 2)
        };
}

BenchmarkRunner.Run<FibonacciBenchmarks>();
```

Run with:

```bash
dotnet run -c Release
```

---

## 📊 Output Comparison

| Feature              | Rust (`criterion`)     | C# (`BenchmarkDotNet`)   |
|----------------------|------------------------|---------------------------|
| CLI Command          | `cargo bench`          | `dotnet run -c Release`  |
| Baseline Support     | ✅ Yes                 | ✅ Yes                    |
| Histogram Output     | ✅ Yes                 | ✅ Yes                    |
| HTML Reports         | ✅ Yes (optional)      | ✅ Yes                    |
| Statistical Analysis | ✅ Built-in             | ✅ Built-in               |
| Async Benchmarks     | Limited support         | ✅ Yes                    |

---

## 📝 Summary

| Task                      | Rust                         | C#                            |
|---------------------------|------------------------------|-------------------------------|
| Add dependency            | `criterion` in dev-deps      | `BenchmarkDotNet` via NuGet   |
| Define benchmark function | `fn` with `c.bench_function` | `[Benchmark]` attribute       |
| Execute benchmark         | `cargo bench`                | `dotnet run -c Release`       |
| Output                    | CLI + charts (optional)      | Console + charts + markdown   |

Both ecosystems provide high-quality benchmarking tools — Rust focuses on precision and minimalism, while C# offers rich reports and IDE integration.