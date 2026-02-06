# Building from Source

This guide covers building botserver from source, including dependencies, feature flags, and platform-specific considerations.

## Prerequisites

### System Requirements

- **Operating System**: Linux, macOS, or Windows
- **Rust**: 1.90 or later (2021 edition)
- **Memory**: 4GB RAM minimum (8GB recommended)
- **Disk Space**: 8GB for development environment

### Install Git

Git is required to clone the repository and manage submodules.

#### Linux

```bash
sudo apt install git
```

#### macOS

```bash
brew install git
```

#### Windows

Download and install from: https://git-scm.com/download/win

Or use winget:

```powershell
winget install Git.Git
```

### Install Rust

If you don't have Rust installed:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```

Verify installation:

```bash
rustc --version
cargo --version
```

### System Dependencies

#### Linux (Ubuntu/Debian)

**Critical: Install clang linker first** (fixes "linker `clang` not found" error):

```bash
sudo apt update
sudo apt install -y \
    clang \
    lld \
    build-essential \
    pkg-config \
    libssl-dev \
    libpq-dev \
    cmake \
    git
```

Configure Rust to use clang as the linker:

```bash
mkdir -p ~/.cargo
cat >> ~/.cargo/config.toml << EOF
[target.x86_64-unknown-linux-gnu]
linker = "clang"
rustflags = ["-C", "link-arg=-fuse-ld=lld"]
EOF
```

#### Linux (Fedora/RHEL)

```bash
sudo dnf install -y \
    clang \
    lld \
    gcc \
    gcc-c++ \
    make \
    pkg-config \
    openssl-devel \
    postgresql-devel \
    cmake \
    git
```

Configure Rust to use clang as the linker:

```bash
mkdir -p ~/.cargo
cat >> ~/.cargo/config.toml << EOF
[target.x86_64-unknown-linux-gnu]
linker = "clang"
rustflags = ["-C", "link-arg=-fuse-ld=lld"]
EOF
```

#### macOS

```bash
brew install postgresql openssl cmake git
xcode-select --install
```

#### Windows

Install Visual Studio Build Tools with C++ support from:
https://visualstudio.microsoft.com/downloads/

Select "Desktop development with C++" workload during installation.

Then install PostgreSQL manually from:
https://www.postgresql.org/download/windows/

## Clone Repository

```bash
git clone --recursive https://github.com/GeneralBots/gb.git
cd gb
```

If you cloned without `--recursive`, initialize submodules:

```bash
git submodule update --init --recursive
```

## Build Cache with sccache

sccache (Shared Compilation Cache) dramatically speeds up rebuilds by caching compilation artifacts. Highly recommended for development.

### Install sccache

#### Linux

```bash
cargo install sccache
```

#### macOS

```bash
brew install sccache
```

#### Windows

```powershell
cargo install sccache
```

### Configure Cargo to Use sccache

Add to `~/.cargo/config.toml`:

```toml
[build]
compiler = "sccache"
```

### Verify sccache is Working

```bash
export RUSTC_WRAPPER=sccache
cargo build --release
sccache --show-stats
```

Expected output shows cache hits/misses:

```
Compile requests                    45
Compile requests executed           12
Cache hits                           8
Cache misses                         4
Cache hit rate                    66.67%
```

### Clear sccache

If you need to clear the cache:

```bash
sccache --zero-stats
```

## Build Configurations

### Standard Build

Build with default features (includes desktop support):

```bash
cargo build --release
```

The compiled binary will be at `target/release/botserver`.

### Minimal Build

Build without any optional features:

```bash
cargo build --release --no-default-features
```

This excludes:
- Desktop GUI (Tauri)
- Vector database (Qdrant)
- Email integration (IMAP)

### Feature-Specific Builds

#### With Vector Database

Enable Qdrant vector database support:

```bash
cargo build --release --features vectordb
```

#### With Email Support

Enable IMAP email integration:

```bash
cargo build --release --features email
```

#### Desktop Application

Build as desktop app with Tauri (default):

```bash
cargo build --release --features desktop
```

#### All Features

Build with all optional features:

```bash
cargo build --release --all-features
```

## Feature Flags

botserver supports the following features defined in `Cargo.toml`:

```toml
[features]
default = ["desktop"]
vectordb = ["qdrant-client"]
email = ["imap"]
desktop = ["dep:tauri", "dep:tauri-plugin-dialog", "dep:tauri-plugin-opener"]
```

### Feature Details

| Feature | Dependencies | Purpose |
|---------|--------------|---------|
| `desktop` | tauri, tauri-plugin-dialog, tauri-plugin-opener | Native desktop application with system integration |
| `vectordb` | qdrant-client | Semantic search with Qdrant vector database |
| `email` | imap | IMAP email integration for reading emails |

## Build Profiles

### Debug Build

For development with debug symbols and no optimizations:

```bash
cargo build
```

Binary location: `target/debug/botserver`

### Release Build

Optimized for production with LTO and size optimization:

```bash
cargo build --release
```

Binary location: `target/release/botserver`

The release profile in `Cargo.toml` uses aggressive optimization:

```toml
[profile.release]
lto = true              # Link-time optimization
opt-level = "z"         # Optimize for size
strip = true            # Strip symbols
panic = "abort"         # Abort on panic (smaller binary)
codegen-units = 1       # Better optimization (slower build)
```

## Platform-Specific Builds

### Linux

Standard build works on most distributions:

```bash
cargo build --release
```

For static linking (portable binary):

```bash
RUSTFLAGS='-C target-feature=+crt-static' cargo build --release --target x86_64-unknown-linux-gnu
```

### macOS

Build for current architecture:

```bash
cargo build --release
```

Build universal binary (Intel + Apple Silicon):

```bash
rustup target add x86_64-apple-darwin aarch64-apple-darwin
cargo build --release --target x86_64-apple-darwin
cargo build --release --target aarch64-apple-darwin
lipo -create \
    target/x86_64-apple-darwin/release/botserver \
    target/aarch64-apple-darwin/release/botserver \
    -output botserver-universal
```

### Windows

Build with MSVC toolchain:

```bash
cargo build --release
```

Binary location: `target\release\botserver.exe`

## Cross-Compilation

### Install Cross-Compilation Tools

```bash
cargo install cross
```

### Build for Linux from macOS/Windows

```bash
cross build --release --target x86_64-unknown-linux-gnu
```

### Build for Windows from Linux/macOS

```bash
cross build --release --target x86_64-pc-windows-gnu
```

## Troubleshooting

### Linker Errors (Linux)

**Error: `linker 'clang' not found`**

This occurs when clang/lld is not installed:

```bash
sudo apt install clang lld
```

Then configure Rust to use clang:

```bash
mkdir -p ~/.cargo
cat >> ~/.cargo/config.toml << EOF
[target.x86_64-unknown-linux-gnu]
linker = "clang"
rustflags = ["-C", "link-arg=-fuse-ld=lld"]
EOF
```

### OpenSSL Errors

If you encounter OpenSSL linking errors:

**Linux:**
```bash
sudo apt install libssl-dev
```

**macOS:**
```bash
export OPENSSL_DIR=$(brew --prefix openssl)
cargo build --release
```

**Windows:**
```powershell
# Use vcpkg
vcpkg install openssl:x64-windows
$env:OPENSSL_DIR="C:\vcpkg\installed\x64-windows"
cargo build --release
```

### PostgreSQL Library Errors

If libpq is not found:

**Linux:**
```bash
sudo apt install libpq-dev
```

**macOS:**
```bash
brew install postgresql
export PQ_LIB_DIR=$(brew --prefix postgresql)/lib
```

**Windows:**
```powershell
# Ensure PostgreSQL is in PATH
$env:PQ_LIB_DIR="C:\Program Files\PostgreSQL\15\lib"
```

### Out of Memory During Build

Use sccache to cache compilations:

```bash
cargo install sccache
export RUSTC_WRAPPER=sccache
cargo build --release
```

Or reduce parallel jobs:

```bash
cargo build --release -j 2
```

Or limit memory per job:

```bash
CARGO_BUILD_JOBS=2 cargo build --release
```

### Linker Errors

Ensure you have a C/C++ compiler:

**Linux:**
```bash
sudo apt install build-essential
```

**macOS:**
```bash
xcode-select --install
```

**Windows:**
Install Visual Studio Build Tools with C++ support.

## Common Build Errors

### Error: `linker 'clang' not found`

**Cause:** The C/C++ toolchain is missing or not configured.

**Solution (Linux):**

1. Install clang and lld:
```bash
sudo apt update
sudo apt install -y clang lld build-essential
```

2. Configure Rust to use clang:
```bash
mkdir -p ~/.cargo
cat > ~/.cargo/config.toml << 'EOF'
[build]
rustflags = ["-C", "linker=clang", "-C", "link-arg=-fuse-ld=lld"]

[target.x86_64-unknown-linux-gnu]
linker = "clang"
EOF
```

3. Clean and rebuild:
```bash
cargo clean
cargo build --release
```

**Solution (macOS):**

```bash
xcode-select --install
```

**Solution (Windows):**

Install Visual Studio Build Tools with "Desktop development with C++" workload.

### Error: `could not find native library pq`

**Cause:** PostgreSQL development libraries are missing.

**Solution:**

**Linux:**
```bash
sudo apt install libpq-dev
```

**macOS:**
```bash
brew install postgresql
export PQ_LIB_DIR=$(brew --prefix postgresql)/lib
```

**Windows:** Install PostgreSQL from postgresql.org

### Error: `openssl-sys` build failures

**Cause:** OpenSSL headers are missing.

**Solution:**

**Linux:**
```bash
sudo apt install libssl-dev pkg-config
```

**macOS:**
```bash
brew install openssl
export OPENSSL_DIR=$(brew --prefix openssl)
export OPENSSL_LIB_DIR=$(brew --prefix openssl)/lib
export OPENSSL_INCLUDE_DIR=$(brew --prefix openssl)/include
```

### Error: Out of memory during build

**Cause:** Too many parallel compilation jobs.

**Solution:**

Reduce parallel jobs:
```bash
CARGO_BUILD_JOBS=2 cargo build --release
```

Or limit memory:
```bash
ulimit -v 4000000  # Limit to 4GB
cargo build --release
```

### Error: Submodule references not found

**Cause:** Submodules not initialized.

**Solution:**

```bash
git submodule update --init --recursive
```

Or re-clone with submodules:
```bash
git clone --recursive https://github.com/GeneralBots/gb.git
```

## Verify Build

After building, verify the binary works:

```bash
./target/release/botserver --version
```

Expected output: `botserver 6.2.0` or similar.

## Development Builds

### Watch Mode

Auto-rebuild on file changes:

```bash
cargo install cargo-watch
cargo watch -x 'build --release'
```

### Check Without Building

Fast syntax and type checking:

```bash
cargo check
```

With specific features:

```bash
cargo check --features vectordb,email
```

## Testing

### Run All Tests

```bash
cargo test
```

### Run Tests for Specific Module

```bash
cargo test --package botserver --lib bootstrap::tests
```

### Run Integration Tests

```bash
cargo test --test '*'
```

## Code Quality

### Format Code

```bash
cargo fmt
```

### Lint Code

```bash
cargo clippy -- -D warnings
```

### Check Dependencies

```bash
cargo tree
```

Find duplicate dependencies:

```bash
cargo tree --duplicates
```

### Security Audit

Run security audit to check for known vulnerabilities in dependencies:

```bash
cargo install cargo-audit
cargo audit
```

This should be run regularly during development to ensure dependencies are secure.

### Quick Build Check

Check if everything compiles without building:

```bash
cargo check --all-features
```

This is much faster than a full build and catches most errors.

## Build Artifacts

After a successful release build, you'll have:

- `target/release/botserver` - Main executable
- `target/release/build/` - Build script outputs
- `target/release/deps/` - Compiled dependencies

## Size Optimization

The release profile already optimizes for size. To further reduce:

### Strip Binary Manually

```bash
strip target/release/botserver
```

### Use UPX Compression

```bash
upx --best --lzma target/release/botserver
```

Note: UPX may cause issues with some systems. Test thoroughly.

## Clean Build

Remove all build artifacts:

```bash
cargo clean
```

## CI/CD Builds

For automated builds in CI/CD pipelines:

### GitHub Actions

```yaml
name: Build

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: recursive
      
      - name: Install Rust
        uses: dtolnay/rust-toolchain@stable
      
      - name: Install Dependencies
        run: |
          sudo apt update
          sudo apt install -y clang lld build-essential pkg-config libssl-dev libpq-dev cmake
      
      - name: Cache sccache
        uses: actions/cache@v3
        with:
          path: ~/.cache/sccache
          key: ${{ runner.os }}-sccache-${{ hashFiles('**/Cargo.lock') }}
      
      - name: Build
        run: cargo build --release --all-features
```

### LXC Build

Build inside LXC container:

```bash
# Create build container
lxc-create -n botserver-build -t download -- -d ubuntu -r jammy -a amd64

# Configure container with build resources
cat >> /var/lib/lxc/botserver-build/config << EOF
lxc.cgroup2.memory.max = 4G
lxc.cgroup2.cpu.max = 400000 100000
EOF

# Start container
lxc-start -n botserver-build

# Install build dependencies
lxc-attach -n botserver-build -- bash -c "
apt-get update
apt-get install -y clang lld build-essential pkg-config libssl-dev libpq-dev cmake curl git
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
source \$HOME/.cargo/env
"

# Build botserver
lxc-attach -n botserver-build -- bash -c "
git clone --recursive https://github.com/GeneralBots/gb.git /build
cd /build
source \$HOME/.cargo/env
cargo build --release --no-default-features
"

# Copy binary from container
lxc-attach -n botserver-build -- cat /build/target/release/botserver > /usr/local/bin/botserver
chmod +x /usr/local/bin/botserver
```

## Installation

After building, install system-wide:

```bash
sudo install -m 755 target/release/botserver /usr/local/bin/
```

Or create a symlink:

```bash
ln -s $(pwd)/target/release/botserver ~/.local/bin/botserver
```

Verify installation:

```bash
botserver --version
```

Expected output: `botserver 6.2.0` or similar.

## Quick Reference

| Command | Purpose |
|---------|---------|
| `cargo build --release` | Optimized production build |
| `cargo build --release -j 2` | Build with limited parallelism |
| `cargo check` | Fast syntax/type checking |
| `cargo test` | Run all tests |
| `cargo clippy` | Lint code |
| `cargo clean` | Remove build artifacts |
| `CARGO_BUILD_JOBS=2 cargo build` | Limit build jobs |
| `RUSTC_WRAPPER=sccache cargo build` | Use compilation cache |

## Next Steps

After building:

1. Run the bootstrap process to install dependencies
2. Configure `.env` file with database credentials
3. Start botserver and access web interface
4. Create your first bot from templates

See [Chapter 01: Run and Talk](../chapter-01/README.md) for next steps.