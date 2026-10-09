# Lossy UDP Chat

A terminal chat between two machines over UDP. UDP doesn't guarantee delivery, so messages can be lost, arrive out of order, or arrive twice. This chat numbers every message, can simulate a lossy network with `--drop`, and reports which messages were lost, late, or duplicated.

> Work in progress: the chat is still being written.

## Stack

- **C++20** with POSIX UDP sockets
- **poll()** event loop over stdin and the socket
- **CMake** + **CTest**, with **GitHub Actions** CI

## Getting started

```sh
cmake -S . -B build
cmake --build build
```

Run one side in each terminal:

```sh
./build/udpchat --port 9000 --peer 127.0.0.1:9001   # alice
./build/udpchat --port 9001 --peer 127.0.0.1:9000   # bob
```

Add `--drop 10` to skip 10% of sent messages and simulate a bad network.

Run the tests:

```sh
ctest --test-dir build --output-on-failure
```

## Example output

```
[bob] #3 testing loss
[warn] gap: #4 missing
[bob] #5 did #4 make it?
[warn] duplicate: #5 already received
```

## How it works

Every message gets a sequence number (1, 2, 3, …). The receiver compares each number to the ones it has already seen:

- **Skipped a number**: a message was lost (`gap`)
- **Smaller than the last one**: it arrived out of order (`late`)
- **Already seen**: it arrived twice (`duplicate`)

Each packet is a 4-byte sequence number followed by the message text.

## Repo layout

```
src/            Source code
tests/          Tests
cmake/          Shared CMake settings
.github/        CI workflow
CMakeLists.txt  Build definition
```
