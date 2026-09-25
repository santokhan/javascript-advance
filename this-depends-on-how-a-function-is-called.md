### Advanced JavaScript concept: `this` depends on how a function is called

A regular function’s `this` is determined when you **call** it, not when you define it.

```js
"use strict";

const user = {
  name: "Santo",

  sayName() {
    return this.name;
  },
};

console.log(user.sayName()); // "Santo"

const detached = user.sayName;
console.log(detached()); // TypeError: this is undefined
```

In `user.sayName()`, the object before the dot becomes `this`. In `detached()`, there is no object before the call, so `this` is `undefined` in strict mode.

You can explicitly bind the function to the object:

```js
const boundSayName = user.sayName.bind(user);

console.log(boundSayName()); // "Santo"
```

**Arrow functions behave differently:** they take `this` from their surrounding scope. That makes them useful inside callbacks, but usually a poor choice for an object method that needs `this` to refer to the object.
