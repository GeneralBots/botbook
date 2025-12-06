# Testing

General Bots uses a comprehensive testing framework including unit tests, integration tests, and end-to-end (E2E) tests to ensure platform reliability and quality.

## Overview

The testing strategy covers:

- **Unit Tests** - Individual component testing
- **Integration Tests** - Service interaction testing  
- **E2E Tests** - Complete user journey validation

## Test Structure

All tests are organized in the `bottest` package:

```
bottest/
├── src/              # Test utilities and harness
├── tests/
│   ├── unit/         # Unit tests
│   ├── integration/  # Integration tests
│   └── e2e/          # End-to-end tests
├── benches/          # Performance benchmarks
└── Cargo.toml
```

## Running Tests

### All Tests
```bash
cd gb/bottest
cargo test
```

### Specific Test Types
```bash
# Unit tests
cargo test --lib

# Integration tests
cargo test --test integration

# E2E tests
cargo test --test e2e -- --nocapture
```

## Test Harness

The test harness provides utilities for setting up test environments:

```rust
use bottest::prelude::*;

#[tokio::test]
async fn my_test() {
    let ctx = TestHarness::full().await.unwrap();
    // Test code here
    ctx.cleanup().await.unwrap();
}
```

## Continuous Integration

Tests run automatically on:
- Pull requests
- Commits to main branch
- Pre-release checks

See the repository's CI/CD configuration for details.

## Next Steps

- [End-to-End Testing](./e2e-testing.md) - Browser automation and user flow testing
- [Performance Testing](./performance.md) - Benchmarking and profiling
- [Test Architecture](./architecture.md) - Design patterns and best practices