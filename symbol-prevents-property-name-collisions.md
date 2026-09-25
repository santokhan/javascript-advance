### Advanced JavaScript concept: `Symbol` prevents property-name collisions

Suppose two parts of an app need to attach internal data to the same object. If both choose a property called `id`, one may overwrite the other. A `Symbol` gives each part a unique property key.

```js
const internalId = Symbol("internalId");

const user = {
  id: 42,
  name: "Santo",
};

user[internalId] = "session-abc";

console.log(user.id);          // 42
console.log(user[internalId]); // "session-abc"
```

The text `"internalId"` is only a description. Creating another symbol with the same description still gives you a different key:

```js
const anotherId = Symbol("internalId");

console.log(internalId === anotherId); // false
console.log(user[anotherId]);          // undefined
```

You’ve likely used symbols indirectly: `Symbol.iterator` is the special key JavaScript checks when you use `for...of` on an object.
