# Tulis

> Fast concurrent file writer, similar to [steno](https://github.com/typicode/steno)

## Features

- Fast, uses `Bun.write` (Node currently not supported)
- Type safe, written in TypeScript
- Lightweight (Haven't checked the size)
- Handles race condition and unnecessary writes

## Usage

```typescript
import { Writer } from "tulis";

// Creates a new writer instance
const writer = new Writer("file.txt");

// Also supports file URL
const writerUrl = new Writer("file://file.txt");

// tulis will handle the race condition
// Writes are always in order
const promises = Array(1000)
  .fill(0)
  .map((_, i) => tulis.write(`${data}${i}`));

await Promise.all(promises);
```

## Benchmark

`bun run benchmark` (see `scripts/benchmark.ts`)

```plaintext
(IN PROGRESS)
```

## FAQ

**Comparison with steno**
Please write an issue if missed something

| Feature            | tulis | steno |
| ------------------ | ----- | ----- |
| TypeScript         | ✓     | ✓     |
| No Race Conditions | ✓     | ✓     |
| Atomic Writes      | ✗     | ✓     |
| Automatic Retry    | ✗     | ✓     |

**Will Node.js get supported?**
Yes, when Bun supports [polyfilling `bun:` modules for Node](https://bun.sh/docs/bundler#target)

**Why this instead of steno?**
tulis uses `Bun.write` instead of Node's `writeFile`, which is faster. See [benchmarks](#benchmark)

## Credits

Heavily inspired by [steno](https://github.com/typicode/steno) by [typicode](https://github.com/typicode)
