
# 🧠 Node.js Streams - A Complete Guide

## 🔄 What Are Streams?

Streams are **event-based interfaces** in Node.js used to **handle streaming data**. Instead of reading/writing the entire data at once (which can be memory-heavy), streams allow **chunk-by-chunk** processing — perfect for files, network sockets, and more.

---

## 📚 Four Types of Streams in Node.js

| Stream Type     | Purpose                                | Methods Used            |
|------------------|----------------------------------------|--------------------------|
| `Readable`       | Read data from a source                | `.on('data')`, `.read()` |
| `Writable`       | Write data to a destination            | `.write()`, `.end()`     |
| `Duplex`         | Both readable and writable             | `.read()` + `.write()`   |
| `Transform`      | Modify or transform data while streaming | `.transform()`           |

---

## ✅ 1. Readable Stream Example

```js
const fs = require('fs');
const readable = fs.createReadStream('input.txt', 'utf8');

readable.on('data', chunk => {
    console.log('Received chunk:', chunk);
});

readable.on('end', () => {
    console.log('Read complete.');
});

readable.on('error', err => {
    console.error('Error received:', err);
});
```

✅ **Use Case**: Reading large files, video/audio streams

---

## ✅ 2. Writable Stream Example

```js
const fs = require('fs');
const writable = fs.createWriteStream('output.txt', 'utf8');

writable.write('First line\n');
writable.write('Second line');
writable.end('Final line');

writable.on('finish', () => {
    console.log('Write complete.');
});
```

✅ **Use Case**: Writing logs, files, responses

---

## ✅ 3. Duplex Stream Example

```js
const { Duplex } = require('stream');

const duplex = new Duplex({
    read(size) {
        this.push('Hello from Duplex Read\n');
        this.push(null);
    },
    write(chunk, encoding, callback) {
        console.log('Duplex Write:', chunk.toString());
        callback();
    }
});

duplex.write('Neo sending data\n');
duplex.on('data', chunk => console.log('Duplex Read:', chunk.toString()));
```

✅ **Use Case**: TCP sockets, real-time messaging systems

---

## ✅ 4. Transform Stream Example

```js
const { Transform } = require('stream');

const upperCaseTransform = new Transform({
    transform(chunk, encoding, callback) {
        this.push(chunk.toString().toUpperCase());
        callback();
    }
});

process.stdin.pipe(upperCaseTransform).pipe(process.stdout);
```

✅ **Use Case**: Compression, encryption, data formatting

---

## 🔄 Why Duplex Stream Runs First in Your Code

Duplex methods like `.write()` and `.on('data')` run **synchronously** because they're defined **inside your own code**. In contrast, `fs.createReadStream()` and `fs.createWriteStream()` wait for the **file system**, which is asynchronous.

---

## ❓ What is `process`?

Node.js global object that gives info/control over the current process.

```js
console.log(process.pid);       // Process ID
console.log(process.version);  // Node.js version
console.log(process.argv);     // CLI arguments
```

---

## ❓ What is Encoding?

Encoding defines **how binary is converted to string**.

| Encoding | Description             |
|----------|-------------------------|
| utf-8    | Default text encoding   |
| base64   | Image & binary-friendly |
| hex      | Hexadecimal             |
| ascii    | Basic English only      |

---

## ❓ Why Do We Use `callback()` in Streams?

Manual `callback()` is required in streams to **signal completion** of a `write()` or `transform()`.

```js
write(chunk, encoding, callback) {
    // process chunk
    callback(); // Let Node know you're done
}
```

If you **forget to call `callback()`**, the stream may **stall or leak memory**.

---

## 💡 Modern Alternative to Callbacks

You can use `Promise`, `async/await`, or `stream.pipeline()` instead of handling callbacks manually.

```js
const fs = require('fs').promises;

async function readFile() {
    try {
        const data = await fs.readFile('input.txt', 'utf8');
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
readFile();
```

---

## 🛡️ Best Practices for Streams

- Always handle `'error'` events
- Use `.pipe()` for chaining
- Use `stream.pipeline()` for clean, managed flow
- Avoid blocking operations inside streams
- Always call `callback()` in custom write/transform streams

---

## ✅ Summary Table

| Concept         | Purpose                                       |
|------------------|-----------------------------------------------|
| `process`        | Info & control of current Node.js process     |
| `encoding`       | Format for converting binary ↔ text           |
| `callback()`     | Used in async/stream APIs to signal done      |
| `readable`       | Pull data chunk-by-chunk                      |
| `writable`       | Send data chunk-by-chunk                      |
| `duplex`         | Both read and write in same stream            |
| `transform`      | Modify data as it passes through              |

---

## 🧪 Run Example

1. Create `input.txt` with some content.
2. Copy code into a `.js` file and run it:
```bash
node yourscript.js
```

---

## Why pipe is used in the Streams ?
    const fs = require('fs');
    
    const readable = fs.createReadStream('input.txt');
    const writable = fs.createWriteStream('output.txt');
    
    readable.pipe(writable); // ✅ Direct piping


Need help building a streaming compression tool with gzip or converting streams to promises? Just ask 😎
