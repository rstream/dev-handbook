# ES version history

[← back](index.md)

ECMAScript (ES) is the language standard behind JavaScript, published as ECMA-262.
Each edition builds on the previous one. The tables below list the main additions, rather than every specification change.

## Version names

There are two naming schemes for the same releases:

- **Edition number:** ES6 means the 6th edition of ECMA-262.
- **Year:** ES2015 means ECMAScript 2015, the same release as ES6.

**ES6 = ES2015**, **ES7 = ES2016**, **ES8 = ES2017**, and so on.
For releases from 2015 onward, the edition number equals the year minus 2009.
Year-based names are the usual names for newer releases; names such as ES11 or ES17 refer to their edition numbers.
The yearly release cycle began with ES2016.

**ES6+** and **ESNext** do not identify a single edition:

- **ES6+** usually means ES2015 and later features.
- **ESNext** refers to upcoming language features; its meaning changes over time.

## Early editions

| Edition | Year | Main additions / changes |
| --- | --- | --- |
| ES1 | 1997 | First standardized version: variables, functions, objects, arrays, prototype-based inheritance, and basic control flow. |
| ES2 | 1998 | Editorial changes to align with the ISO standard; no new language features. |
| ES3 | 1999 | Regular expressions, `try` / `catch`, `throw`, `do...while`, `switch`, and improvements to strings and error handling. |
| ES4 | — | Never published. Work on this edition was abandoned; some ideas later influenced ES6. |
| ES5 | 2009 | Strict mode (`'use strict'`), `JSON.parse()` / `JSON.stringify()`, array methods such as `map()`, `filter()`, `reduce()`, and `forEach()`, `Function.prototype.bind()`, getters/setters, `Object.create()`, and property descriptors. |
| ES5.1 | 2011 | Corrections and alignment with ISO/IEC 16262:2011; no major new features. |

Release dates and historical context: [Ecma's ECMA-262 archive](https://ecma-international.org/publications-and-standards/standards/ecma-262/) and the [specification introduction](https://262.ecma-international.org/17.0/#sec-intro).

## Yearly editions

The year links open the published specification for that edition.
Method names such as `flat()` refer to prototype methods unless a constructor name is included.

| Year-based name | Edition name | Main additions |
| --- | --- | --- |
| [ES2015](https://262.ecma-international.org/6.0/) | ES6 | `let` / `const`, block scope, arrow functions, default parameters, rest parameters and spread in arrays/calls, destructuring, template literals, classes, modules (`import` / `export`), promises, generators, iterators, `for...of`, `Symbol`, `Map` / `Set` / `WeakMap` / `WeakSet`, `Proxy` / `Reflect`, typed arrays, `Object.assign()`, `Array.from()`, `find()`, and string methods such as `includes()`. |
| [ES2016](https://262.ecma-international.org/7.0/) | ES7 | Exponentiation (`**`, `**=`) and `Array.prototype.includes()`. |
| [ES2017](https://262.ecma-international.org/8.0/) | ES8 | `async` / `await`, `Object.values()` / `Object.entries()` / `Object.getOwnPropertyDescriptors()`, `padStart()` / `padEnd()`, trailing commas in function parameters and calls, `SharedArrayBuffer`, and `Atomics`. |
| [ES2018](https://262.ecma-international.org/9.0/) | ES9 | Object rest/spread (`{ ...obj }`), async iteration (`for await...of`) and async generators, `Promise.prototype.finally()`, RegExp named capture groups, lookbehind, Unicode property escapes, and the `s` (dotAll) flag. |
| [ES2019](https://262.ecma-international.org/10.0/) | ES10 | `flat()` / `flatMap()`, `Object.fromEntries()`, `trimStart()` / `trimEnd()`, optional catch binding (`catch { ... }`), stable array sorting, well-formed `JSON.stringify()`, and more precise `Function.prototype.toString()` output. |
| [ES2020](https://262.ecma-international.org/11.0/) | ES11 | Optional chaining (`?.`), nullish coalescing (`??`), `BigInt`, dynamic `import()`, `import.meta`, `export * as ns`, `Promise.allSettled()`, `globalThis`, and `String.prototype.matchAll()`. |
| [ES2021](https://262.ecma-international.org/12.0/) | ES12 | Logical assignment (`&&=`, `\|\|=`, `??=`), numeric separators (`1_000`), `replaceAll()`, `Promise.any()`, `AggregateError`, `WeakRef`, and `FinalizationRegistry`. |
| [ES2022](https://262.ecma-international.org/13.0/) | ES13 | Top-level `await` in modules; public/private class fields, private methods/accessors, static fields and initialization blocks, private-field checks (`#field in obj`); `at()`, `Object.hasOwn()`, error `cause`, and the RegExp `d` flag for match indices. |
| [ES2023](https://262.ecma-international.org/14.0/) | ES14 | Array copying methods (`toSorted()`, `toReversed()`, `toSpliced()`, `with()`), `findLast()` / `findLastIndex()`, hashbang comments (`#!`), and non-registered symbols in weak collections. Typed arrays also gained these methods except `toSpliced()`. |
| [ES2024](https://262.ecma-international.org/15.0/) | ES15 | `Object.groupBy()` / `Map.groupBy()`, `Promise.withResolvers()`, resizable/transferable `ArrayBuffer`, growable `SharedArrayBuffer`, `Atomics.waitAsync()`, `isWellFormed()` / `toWellFormed()`, and the RegExp `v` flag for Unicode sets. |
| [ES2025](https://262.ecma-international.org/16.0/) | ES16 | Iterator helpers (`Iterator.from()`, `map()`, `filter()`, `take()`, `toArray()`, etc.); set operations (`union()`, `intersection()`, `difference()`, etc.); import attributes and JSON modules; `RegExp.escape()`, inline RegExp modifiers and duplicate named groups in separate alternatives; `Promise.try()`, `Float16Array`, and related float16 methods. |
| [ES2026](https://262.ecma-international.org/17.0/) | ES17 | `Array.fromAsync()`, `Iterator.concat()`, `Map` / `WeakMap` methods `getOrInsert()` and `getOrInsertComputed()`, `Math.sumPrecise()`, `Error.isError()`, `Uint8Array` Base64/hex conversion methods, JSON parse source access (`context.source` in revivers), `JSON.rawJSON()`, and `JSON.isRawJSON()`. |

For proposal-to-release mapping, see TC39's [finished proposals](https://github.com/tc39/proposals/blob/main/finished-proposals.md).
As of November 2026, ES2026 is the latest published edition. The [living specification](https://tc39.es/ecma262/) is already the ES2027 draft and can include features beyond ES2026.

## Common version mix-ups

### Promises, async/await, and top-level await

These arrived in different releases:

```js
// ES2015: promises
Promise.resolve('Ready').then(value => {
    console.log(value);
});

// ES2017: await inside an async function
async function showStatus() {
    const value = await Promise.resolve('Ready');
    console.log(value);
}

// ES2022: await at the top level of an ES module
const value = await Promise.resolve('Ready');
console.log(value);
```

Top-level `await` works in ES modules, for example a browser script loaded with `type="module"`.
It is not allowed at the top level of a classic script or inside an ordinary non-async function.
The containing module waits for the awaited operation before finishing evaluation; modules that depend on it wait for that evaluation to complete.

### Array spread and object spread

```js
// ES2015: spread in arrays and function calls
const numbers = [...[1, 2], 3];
Math.max(...numbers);

// ES2018: spread in object literals
const user = { ...{ name: 'Alice' }, active: true };
```

### Language features and runtime APIs

An ES edition describes the language and its standard built-ins.
Browser APIs such as the DOM, `fetch()`, and `setTimeout()` belong to the host environment and do not have an ES introduction year.
Browser and Node.js support can arrive before or after publication of an edition, so the ES year alone does not guarantee runtime support.
