### Advanced JavaScript concept: The event loop

JavaScript runs synchronous code first. When asynchronous work finishes, its callback waits until JavaScript can run it.

Try predicting the output:

```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

Promise.resolve().then(() => {
  console.log("C");
});

console.log("D");
```

The output is:

```text
A
D
C
B
```

Here’s the order:

1. `A` and `D` run immediately.
2. The Promise callback runs next. Promise callbacks go into the **microtask queue**.
3. The timer callback runs afterward. `setTimeout(..., 0)` means “run when eligible,” not “run right now.”

This matters when you mix `async/await`, Promises, timers, and ordinary code.
