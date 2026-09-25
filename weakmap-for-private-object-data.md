### Advanced JavaScript concept: `WeakMap` for private object data

A `WeakMap` stores values using **objects as keys**. It’s useful when you want to attach private data to an object without adding a visible property to it.

```js
const balances = new WeakMap();

class Wallet {
  constructor(initialBalance) {
    balances.set(this, initialBalance);
  }

  deposit(amount) {
    const current = balances.get(this);
    balances.set(this, current + amount);
  }

  getBalance() {
    return balances.get(this);
  }
}

const wallet = new Wallet(100);

wallet.deposit(50);
console.log(wallet.getBalance()); // 150
console.log(wallet.balance);      // undefined
```

Here, `this` is the key. Each `Wallet` instance gets its own balance stored outside the instance.

Why **“weak”**? If a wallet object becomes unreachable elsewhere, its entry in the `WeakMap` does not keep it alive just to preserve that balance. JavaScript can clean it up automatically.

One practical limitation: you cannot loop through a `WeakMap` or ask it for its size.
