# Ritzen

> Fast concurrent file writer, similar to [steno](https://github.com/typicode/steno)

## Installation

```bash
bun install ritzen
```

## Features

- Fast, uses `Bun.write` (Node currently not supported)
- Type safe, written in TypeScript
- Lightweight (~4kB)
- Handles race condition and unnecessary writes

## Usage

```typescript
import { Writer } from "ritzen";

// Creates a new writer instance
const writer = new Writer("file.txt");

// Also supports file URL
const writerUrl = new Writer("file://file.txt");

// ritzen will handle the race condition
// Writes are always in order
const promises = Array(1000)
  .fill(0)
  .map((_, i) => ritzen.write(`${data}${i}`));

await Promise.all(promises);
```

## Benchmark

`bun run benchmark` (see `scripts/benchmark.ts`)

```plaintext
Write 1KB data to the same file x 1000
[85.90ms] fs
[5.22ms] ritzen

Write 1MB data to the same file x 1000
[722.67ms] fs
[5.40ms] ritzen

Write 10MB data to the same file x 1000
[5.71s] fs
[35.41ms] ritzen

Check if the files are identical:  ✓
```

## FAQ

**Comparison with steno**
Please write an issue if missed something

| Feature            | ritzen | steno |
| ------------------ | ----- | ----- |
| TypeScript         | ✓     | ✓     |
| No Race Conditions | ✓     | ✓     |
| Atomic Writes      | ✗     | ✓     |
| Automatic Retry    | ✗     | ✓     |
| Package Size       | 4kB   | 6kB   |

**Will Node.js get supported?**
Yes, when Bun supports [polyfilling `bun:` modules for Node](https://bun.sh/docs/bundler#target)

**Why this instead of steno?**
ritzen uses `Bun.write` instead of Node's `writeFile`, which is faster. See [benchmarks](#benchmark)

## Credits

Heavily inspired by [steno](https://github.com/typicode/steno)
