# Targets (target triples)

There are several triples that you can build for, list of the oficially supported ones is below.

## Supported

- `x86_64-unknown-linux-gnu` (default)
  - Glibc dynamically linked -> required on machine running the built binary
- `x86_64-unknown-linux-musl`
  - Musl dynamically linked -> required on machine running the built binary
- `x86_64-w64-mingw32`
  - mingw required on the maching building the binary
- `xtensa-esp32-elf`
  - ESP-IDF tools required on the machine building the binary
