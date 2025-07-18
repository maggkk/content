---
title: Atomics.notify()
short-title: notify()
slug: Web/JavaScript/Reference/Global_Objects/Atomics/notify
page-type: javascript-static-method
browser-compat: javascript.builtins.Atomics.notify
sidebar: jsref
---

The **`Atomics.notify()`** static
method notifies up some agents that are sleeping in the wait queue.

> [!NOTE]
> This operation only works with an {{jsxref("Int32Array")}} or {{jsxref("BigInt64Array")}} that views a {{jsxref("SharedArrayBuffer")}}.
> It will return `0` on non-shared `ArrayBuffer` objects.

## Syntax

```js-nolint
Atomics.notify(typedArray, index, count)
```

### Parameters

- `typedArray`
  - : An {{jsxref("Int32Array")}} or {{jsxref("BigInt64Array")}} that views a {{jsxref("SharedArrayBuffer")}}.
- `index`
  - : The position in the `typedArray` to wake up on.
- `count` {{optional_inline}}
  - : The number of sleeping agents to notify. Defaults to {{jsxref("Infinity")}}.

### Return value

Returns the number of woken up agents, or `0` if `typedArray` is a view on a non-shared {{jsxref("ArrayBuffer")}}.

### Exceptions

- {{jsxref("TypeError")}}
  - : Thrown if `typedArray` is not an {{jsxref("Int32Array")}} or {{jsxref("BigInt64Array")}}.
- {{jsxref("RangeError")}}
  - : Thrown if `index` is out of bounds in the `typedArray`.

## Examples

### Using `notify`

Given a shared `Int32Array`:

```js
const sab = new SharedArrayBuffer(1024);
const int32 = new Int32Array(sab);
```

A reading thread is sleeping and waiting on location 0 because the provided `value` matches what is stored at the provided `index`.
The reading thread will not move on until the writing thread has called `Atomics.notify()` on position 0 of the provided `typedArray`.
Note that if, after being woken up, the value of location 0 has not been changed by the writing thread, the reading thread will **not** go back to sleep, but will continue on.

```js
Atomics.wait(int32, 0, 0);
console.log(int32[0]); // 123
```

A writing thread stores a new value and notifies the waiting thread once it has
written:

```js
console.log(int32[0]); // 0;
Atomics.store(int32, 0, 123);
Atomics.notify(int32, 0, 1);
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{jsxref("Atomics")}}
- {{jsxref("Atomics.wait()")}}
- {{jsxref("Atomics.waitAsync()")}}
