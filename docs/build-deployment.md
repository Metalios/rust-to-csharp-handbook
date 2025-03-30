# 🚀 Build & Deployment Pipelines: Rust vs C#

This section compares how Rust and C# handle project builds, CI/CD pipelines, and multi-target packaging.

---

## 🛠️ Project Structure

| Feature             | Rust                        | C# (.NET)                  |
|---------------------|-----------------------------|----------------------------|
| Build Tool          | `cargo`                     | `dotnet`                   |
| Solution Format     | N/A (workspaces in TOML)    | `.sln` + `.csproj`         |
| Config File         | `Cargo.toml`                | `.csproj`, `.sln`          |
| Test Target         | `cargo test`                | `dotnet test`              |
| Publish Target      | `cargo build --release`     | `dotnet publish`           |

---

## 📦 Building a Release Binary

### Rust

```bash
cargo build --release
```

Output:
- `target/release/your_app`

### C#

```bash
dotnet publish -c Release -r win-x64 --self-contained
```

Output:
- `bin/Release/net8.0/win-x64/publish/`

---

## 🧪 Running Tests

### Rust

```bash
cargo test
```

### C#

```bash
dotnet test
```

---

## 🔁 Watch for Changes

### Rust

```bash
cargo watch -x run
```

Install with:

```bash
cargo install cargo-watch
```

### C#

```bash
dotnet watch run
```

---

## 🧱 Multi-Project Setup

### Rust

```toml
[workspace]
members = ["core", "utils", "cli"]
```

### C#

```bash
dotnet new sln
dotnet sln add src/Core/Core.csproj
dotnet sln add src/CLI/CLI.csproj
```

---

## ⚙️ CI/CD Example: GitHub Actions

### Rust

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Install Rust
      uses: actions-rs/toolchain@v1
      with:
        toolchain: stable
    - run: cargo build --release
```

### C#

```yaml
jobs:
  build:
    runs-on: windows-latest
    steps:
    - uses: actions/checkout@v3
    - name: Setup .NET
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: '8.0.x'
    - run: dotnet restore
    - run: dotnet build --configuration Release
```

---

## 🧪 Static Analysis & Linting

| Tool Type         | Rust                   | C# (.NET)             |
|-------------------|------------------------|------------------------|
| Linter            | `cargo clippy`         | Roslyn analyzers       |
| Format Code       | `cargo fmt`            | `dotnet format`        |
| Audit Packages    | `cargo audit`          | `dotnet list package --vulnerable` |

---

## 📝 Summary

| Action               | Rust                          | C#                         |
|----------------------|-------------------------------|----------------------------|
| Build                | `cargo build`                 | `dotnet build`             |
| Test                 | `cargo test`                  | `dotnet test`              |
| Release              | `cargo build --release`       | `dotnet publish -c Release`|
| CI Tooling           | GitHub Actions, CLI           | GitHub Actions, Azure DevOps |
| Static Analysis      | `clippy`, `fmt`, `audit`      | Roslyn, `dotnet format`    |

Rust’s `cargo` provides a unified workflow, while .NET’s ecosystem is more modular but deeply integrated with IDEs and enterprise pipelines.