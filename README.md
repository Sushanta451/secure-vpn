# udp-chat

A lossy UDP chat in C++20: UDP sockets, a `poll()` event loop, and sequence numbers to detect dropped and out-of-order messages.

## Build

```sh
cmake -S . -B build
cmake --build build
./build/udpchat
```

## Test

```sh
ctest --test-dir build --output-on-failure
```
