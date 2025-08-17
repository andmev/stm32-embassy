
# STM32 Embassy

A minimal Embedded Rust project targeting STM32 microcontrollers using the Embassy async framework. This repository includes a linker script (`memory.x`) and a simple `build.rs` to wire things up for `no_std` firmware builds.

## Prerequisites

- **Rust toolchain**: stable
- **Target**: `thumbv7em-none-eabihf` (configure your exact MCU features in `Cargo.toml`)
- **Optional**: `mise` for toolchain management, `probe-rs` or your preferred flashing/debugging tooling

### Quick start

- **Install tools with mise** (recommended):
  - `mise install`
- **Build**:
  - `cargo build --release --target thumbv7em-none-eabihf`
- **Flash/Run** (example options):
  - Using `probe-rs`: see `probe-rs` docs to select your exact STM32 chip and run the built ELF
  - Alternatively use OpenOCD/STM32CubeProgrammer with the ELF from the target directory

### Project layout

- `src/main.rs`: application entry point
- `memory.x`: linker script describing flash/RAM regions
- `build.rs`: passes the linker script to the build

### Tool versions and targets (.mise.toml)

For reproducible tool setup, this project includes a `.mise.toml`. Running `mise install` will install the specified toolchain and target.

```toml
[tools]
rust = { version = "stable", components = "rustfmt", targets = "thumbv7em-none-eabihf" }
```

### Notes

- Adjust MCU features and HAL/board support crates in `Cargo.toml` to match your exact STM32 part.
- The final ELF will be in `target/thumbv7em-none-eabihf/{debug,release}/`.
