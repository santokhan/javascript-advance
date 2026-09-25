### Advanced JavaScript concept: `Proxy`

A `Proxy` lets you intercept operations on an object, such as reading or changing a property.

```js
const user = {
  name: "Santo",
  age: 27,
};

const protectedUser = new Proxy(user, {
  set(target, property, value) {
    if (property === "age" && (!Number.isInteger(value) || value < 0)) {
      throw new Error("Age must be a non-negative integer");
    }

    return Reflect.set(target, property, value);
  },
});

protectedUser.age = 28;
console.log(protectedUser.age); // 28

protectedUser.age = -5; // Error
```

When you write `protectedUser.age = 28`, JavaScript calls the proxy’s `set` method first. The method checks the value, then `Reflect.set()` performs the normal assignment.

A `Proxy` can also intercept reads with `get`, deletions with `deleteProperty`, and other operations. Libraries sometimes use proxies to build reactive state, but for ordinary validation, a simple function or class is often easier to maintain.
