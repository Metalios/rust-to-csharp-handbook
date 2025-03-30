# 📦 Dependency Management: Rust Crates vs C# NuGet

Both Rust and C# use package managers to handle third-party libraries, dependencies, and tooling.

---

## 📦 Rust: Cargo & crates.io

### Add a Dependency

Modify `Cargo.toml`:

```toml
[dependencies]
serde = "1.0"
```

Then run:

```bash
cargo build
```

### Update All

```bash
cargo update
```

### Search for a Crate

```bash
cargo search json
```

Or visit: [https://crates.io](https://crates.io)

---

## 📦 C#: NuGet & dotnet CLI

### Add a Dependency

```bash
dotnet add package Newtonsoft.Json
```

This modifies your `.csproj` file:

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="13.0.1" />
</ItemGroup>
```

### Update All Packages

```bash
dotnet list package --outdated
dotnet outdated
```

(use `dotnet-outdated` tool)

### Search for a Package

- Use [https://nuget.org](https://nuget.org)
- Or: `dotnet search Newtonsoft.Json` (experimental)

---

## 🔁 Feature Comparison

| Feature               | Rust (Cargo)                    | C# (.NET + NuGet)              |
|------------------------|----------------------------------|--------------------------------|
| Package Registry       | [crates.io](https://crates.io)   | [nuget.org](https://nuget.org) |
| CLI Tool               | `cargo`                         | `dotnet`                       |
| Versioning Format      | Semver + optional ranges        | Semver + ranges/constraints   |
| Workspace Support      | ✅ Native via `[workspace]`     | ✅ Supported via `.sln`        |
| Lockfile               | `Cargo.lock`                    | `packages.lock.json` (opt-in) |
| Dependency Groups      | `[dependencies]`, `[dev-dependencies]` | TargetFrameworks / Conditionals |

---

## 🛠 Tooling Differences

| Task                    | Cargo                          | .NET CLI                      |
|-------------------------|--------------------------------|-------------------------------|
| Add dependency          | `cargo add serde`              | `dotnet add package Foo`      |
| Remove dependency       | `cargo remove serde`           | Manually edit `.csproj`       |
| Dependency graph        | `cargo tree`                   | `dotnet list package`         |
| Audit dependencies      | `cargo audit`                  | `dotnet list package --vulnerable` (preview) |

---

## 📝 Summary

| Area               | Rust               | C# (.NET)        |
|--------------------|--------------------|------------------|
| Registry           | crates.io          | nuget.org        |
| Tool               | Cargo              | dotnet CLI       |
| Lockfile           | Cargo.lock         | packages.lock.json |
| Dependency groups  | `[dependencies]` + `[dev-dependencies]` | Conditional ItemGroups |

Rust’s package manager is tightly integrated and consistent, while .NET benefits from rich IDE tooling and a large package ecosystem.