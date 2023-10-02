## Drop Node.js 16 support in your projects

- Now: October 2023, we have Node.js 18.18.0 LTS and 20.7.0 (current)
- Going to drop Node.js 16 support before its end-of-file 2023-09-11 in Metarhia codebase, all projects, and course examples
- Now we can rely on Node.js 18.18.0 capabilities
- See release schedule: [github.com/nodejs/release#release-schedule](https://github.com/nodejs/release#release-schedule)

## Important notes

- Before this one see also previous checklist "Drop Node.js 14": [github.com/tshemsedinov/Drop-Nodejs14](https://github.com/tshemsedinov/Drop-Nodejs14)
- New node.js uses `OpenSSL 3` instead of `OpenSSL 1.1.1`. This led to an early end of support for Node.js 16 LST: September 11th, 2023. See details: [nodejs.org/en/blog/announcements/nodejs16-eol](https://nodejs.org/en/blog/announcements/nodejs16-eol)

### Refactoring checklist as of October 2023

- Due to the move from `npm v9` or later version, convert `package_lock.json` to `lockfileVersion 3` by command: `npm i --lockfile-version 3`
- Run your project with flag `--pending-deprecation` to see deprecation warnings and then with flag `--throw-deprecation` to exit with non-zero on deprecated API calls
- Use native [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) instead of polyfill like `undici` or `node-fetch`. Now you can avoid `axios` and `request()` from `node:http`
- You can use [Web Streams API](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API) to be compatible with browser API in server-side rendering or so
- Use `Buffer` method `.subarray(start, end)` instead of deprecated `.slice(start, end)`: [see Buffer docs](https://nodejs.org/api/buffer.html#blobslicestart-end-type)
- Stop using deprecated `url.parse`: [see DEP0169 docs](https://nodejs.org/api/deprecations.html#DEP0169)
- Stop using deprecated `Thenable` in streams: [see DEP0157 docs](https://nodejs.org/api/deprecations.html#DEP0157)
- Use http events: `dropRequest` and `drop`: [see http docs](https://nodejs.org/api/http.html#event-droprequest)
- Use `server.closeAllConnections()` and `server.closeIdleConnections()`: [see http docs](https://nodejs.org/api/http.html#servercloseallconnections)
- Use `module.isBuiltin(moduleName)`: [see module docs](https://nodejs.org/api/module.html#moduleisbuiltinmodulename)
- Now we can use new `V8` features:
  - [`Promise.any()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/any)
  - [`Array.prototype.findLast()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast)
  - [`Array.prototype.findLastIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLastIndex)
- Use promise-based [`node:readline` API](https://nodejs.org/api/readline.html), example: `const name = await rl.question('Name:');` and new methods: `clearLine`,  `commit` and `rollback`, `cursorTo`, `moveCursor`, class `Interface`
- Do not use [`node:async_hooks`](https://nodejs.org/api/async_hooks.html) API like `createHook` and `AsyncHook` as non-stable, except stable classes `AsyncLocalStorage` and `AsyncResource`, see docs in a separate article ["async context tracking"](https://nodejs.org/api/async_context.html)

### Explore new features

- Stable [Web Crypto API](https://nodejs.org/api/webcrypto.html) (`globalThis.crypto` or `require('node:crypto').webcrypto`)
- Improvements to the [Intl API](https://nodejs.org/api/intl.html)
- Class [`Blob`](https://nodejs.org/api/buffer.html#class-blob) from `node:buffer`
- Class [`BrodcastChannel`](https://nodejs.org/api/worker_threads.html#class-broadcastchannel-extends-eventtarget) from `node:worker_threads`
- Global function [`structuredClone`](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone)
- Class [`v8.GCProfiler`](https://nodejs.org/api/v8.html#class-v8gcprofiler)
- Now [`child_process.fork`](https://nodejs.org/api/child_process.html#child_processforkmodulepath-args-options) supports `file:` protocol

### Note that you can't freely use

- Now we have [native test runner module: `node:test`](https://nodejs.org/api/test.html) but it is not completely ready in all aspects. By the way `node:test` is a first module available just with `node:` prefix, it means: you can't access it by `require('test')`
- [Single executable](https://nodejs.org/api/single-executable-applications.html) applications
- Both experimental module-based and process-based [permission model](https://nodejs.org/api/permissions.html)
- Experimental `--watch` flag to enable [auto-restarn on changes](https://nodejs.org/api/cli.html#--watch)
- Experimental [Web Sreams API](https://nodejs.org/api/webstreams.html)
- Experimental method [subprocess[Symbol.dispose]](https://nodejs.org/api/child_process.html#subprocesssymboldispose) added in node.js 20.5.0 to send `SIGTERM` to spawned child process
- Experimental class [`File`](https://nodejs.org/api/buffer.html#class-file)
- Experimental classes `TracingChannel`, `CustomEvent`, `CompressionStream`, `CustomEvent`

### Use node.js features instead of dependencies

- Use native fetch API instead of npm modules `undici`, `request`, `axios`, `node-fetch`
