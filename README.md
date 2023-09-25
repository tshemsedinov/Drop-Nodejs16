## Drop Node.js 16 support in your projects

- Now: October 2023, we have Node.js 18.18.0 LTS and 20.7.0 (current)
- Going to drop Node.js 16 support before its end-of-file 2023-09-11 in all HowProgrammingWorks and Node.js courses, Metarhia codebase
- Now we can rely on Node.js 18.18.0 capabilities
- See release schedule: https://github.com/nodejs/release#release-schedule

See also previous checklist [Drop Node.js 14](https://github.com/tshemsedinov/Drop-Nodejs14)

### Refactoring checklist as of October 2023

- New node.js uses `OpenSSL 3` instead of `OpenSSL 1.1.1`. This led to an early end of support for Node.js 16 LST: September 11th, 2023. See details: https://nodejs.org/en/blog/announcements/nodejs16-eol
- Due to the move from `npm v9` or later version, convert `package_lock.json` to `lockfileVersion 3` by command: `npm i --lockfile-version 3`
- Promise-based `node:readline` API looks like `const name = await rl.question('Name:');`
- [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
- [Native test runner module: `node:test`](https://nodejs.org/api/test.html)
- Autorestart on imported files changes with `- watch` flag
- [Web Streams API](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API)
- The data format of the v8.serialize function has changed (No compatible with earlier versions of Node.js.)
- Now we can use new `V8` features:
  - [`Promise.any()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/any)
  - [`Array.prototype.findLast()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast)
  - [`Array.prototype.findLastIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLastIndex)
- Improvements to the Intl API

### Explore new features

### Note that you can't freely use

### Use node.js features instead of dependencies
