## Drop Node.js 16 support in your projects

- Now: October 2023, we have Node.js 18.18.0 LTS and 20.7.0 (current)
- Going to drop Node.js 16 support before its end-of-file 2023-09-11 in Metarhia codebase, all projects, and course examples
- Now we can rely on Node.js 18.18.0 capabilities
- See release schedule: https://github.com/nodejs/release#release-schedule

## Important notes

- Before this one see also previous checklist "Drop Node.js 14": https://github.com/tshemsedinov/Drop-Nodejs14
- New node.js uses `OpenSSL 3` instead of `OpenSSL 1.1.1`. This led to an early end of support for Node.js 16 LST: September 11th, 2023. See details: https://nodejs.org/en/blog/announcements/nodejs16-eol

### Refactoring checklist as of October 2023

- Due to the move from `npm v9` or later version, convert `package_lock.json` to `lockfileVersion 3` by command: `npm i --lockfile-version 3`
- Use native [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) instead of polyfill like `undici` or `node-fetch`. Now you can avoid `axios` and `request()` from `node:http`.
- You can use [Web Streams API](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API) to be compatible with browser API in server-side rendering or so.
- Use `Buffer` method `.subarray(start, end)` instead of deprecated `.slice(start, end)`
- Stop using deprecated `url.parse`
- Stop using deprecated `Thenable` in streams
- Use http events: `dropRequest` and `drop`
- Use `server.closeAllConnections()` and `server.closeIdleConnections()`
- Use `module.isBuiltin(moduleName)`
- Serializer `v8.serialize` has changed (No compatible with earlier versions of Node.js)
- Now we can use new `V8` features:
  - [`Promise.any()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/any)
  - [`Array.prototype.findLast()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast)
  - [`Array.prototype.findLastIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLastIndex)
- Use promise-based `node:readline` API, example: `const name = await rl.question('Name:');` and new methods: `clearLine`,  `commit` and `rollback`, `cursorTo`, `moveCursor`, class `Interface`

### Explore new features

- Autorestart on imported files changes with `- watch` flag
- Single executable applications
- Class: `v8.GCProfiler`
- Now `child_process.fork` supports `file:` protocol
- Improvements to the Intl API
- Classes `Blob` and `File`
- Class `BrodcastChannel`
- Stable WebCrypto: `globalThis.crypto` or `require('node:crypto').webcrypto`
- Global function `structuredClone`: https://developer.mozilla.org/en-US/docs/Web/API/structuredClone

### Note that you can't freely use

- Now we have [native test runner module: `node:test`](https://nodejs.org/api/test.html) but it is not completely ready in all aspects. By the way `node:test` is a first module available just with `node:` prefix, it means: you can't access it by `require('test')`

### Use node.js features instead of dependencies

- Use native fetch API instead of npm modules `undici`, `request`, `axios`, `node-fetch`
