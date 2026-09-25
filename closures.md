### Advanced JavaScript concept: Closures

A **closure** happens when a function remembers variables from the place where it was created, even after the outer function has finished running.

```js
function createCounter() {
  let count = 0;

  return function () {
    count += 1;
    return count;
  };
}

const counter = createCounter();

console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

When `createCounter()` runs, it creates `count` and returns the inner function. Although `createCounter()` has finished, that inner function still has access to its `count`.

Each call to `createCounter()` creates a separate counter:

```js
const first = createCounter();
const second = createCounter();

console.log(first());  // 1
console.log(first());  // 2
console.log(second()); // 1
```

You’ll see closures in callbacks, event handlers, and functions that keep private state. The key idea is: **a function can carry access to variables from where it was created.**
