
# 📦 Node.js Utility Modules – Cheat Sheet with Examples

Node.js includes several built-in modules for performing system, network, and utility operations. These don't require installation via npm.

---

## 🔧 1. OS Module – System Info

```js
const os = require('os');

console.log("Hostname:", os.hostname());
console.log("OS Type:", os.type());
console.log("Free Memory (MB):", os.freemem() / 1024 / 1024);
console.log("User Info:", os.userInfo());
```

---

## 📁 2. Path Module – File/Directory Paths

```js
const path = require('path');

console.log("Filename:", path.basename(__filename));
console.log("Directory:", path.dirname(__filename));
console.log("Joined Path:", path.join(__dirname, 'folder', 'file.txt'));
```

---

## 🌐 3. URL Module – URL Parsing

```js
const { URL } = require('url');

const myUrl = new URL('https://example.com:8080/path?name=neo');
console.log(myUrl.hostname); // example.com
console.log(myUrl.port);     // 8080
console.log(myUrl.searchParams.get('name')); // neo
```

---

## 🔍 4. Query String Module – Parse Query Params

```js
const qs = require('querystring');

const parsed = qs.parse('name=neo&age=30');
console.log(parsed.name); // neo

const stringified = qs.stringify({ topic: 'node', level: 'easy' });
console.log(stringified); // topic=node&level=easy
```

---

## 🌐 5. Net Module – TCP Networking

```js
const net = require('net');

const server = net.createServer(socket => {
    socket.write('Hello client!\n');
    socket.on('data', data => console.log('Received:', data.toString()));
});

server.listen(3000, () => console.log('TCP server running on port 3000'));
```

---

## 🌐 6. DNS Module – Domain Lookups

```js
const dns = require('dns');

dns.lookup('google.com', (err, address, family) => {
    console.log('IP Address:', address);
});
```

---

## 🔐 7. Domain Module (⚠️ Deprecated)

Used for scoped error handling – now replaced by better patterns like `try/catch` and `async_hooks`.

---

## 🧪 8. Util Module – Utility Functions

```js
const util = require('util');

const asyncTimeout = util.promisify(setTimeout);
asyncTimeout(1000).then(() => console.log('Waited 1 second'));

console.log(util.format('%s scored %d%% in %s', 'Neo', 98, 'Node.js'));
```

---

## 🗃️ 9. Events Module – EventEmitter

```js
const EventEmitter = require('events');

const emitter = new EventEmitter();
emitter.on('message', data => console.log('Got:', data));

emitter.emit('message', 'Hello World!');
```

---

## ⏱️ 10. Timers Module – (Used Implicitly)

```js
setTimeout(() => console.log('After 1 second'), 1000);
setInterval(() => console.log('Every second'), 1000);
```

---

## ⚙️ 11. Process Module – System Process Info

```js
console.log('Process ID:', process.pid);
console.log('Platform:', process.platform);
console.log('Node Version:', process.version);
```

---

## ✅ Summary Table

| Module        | Purpose                             |
|---------------|-------------------------------------|
| `os`          | System info                         |
| `path`        | File paths                          |
| `url`         | URL parsing                         |
| `querystring` | Handle query params                 |
| `net`         | TCP networking                      |
| `dns`         | Domain lookups                      |
| `domain`      | ⚠️ Deprecated error handling         |
| `util`        | Utility tools (promisify, format)   |
| `events`      | Event system                        |
| `timers`      | Timeout and interval functionality  |
| `process`     | Process-level info (PID, memory)    |

---

> 🚀 You can use these in any Node.js app without installation. Just `require()` and go!
