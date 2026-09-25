### Advanced JavaScript concept: `Promise.allSettled()`

Earlier, we used `Promise.all()`. It rejects as soon as one task fails. But sometimes you want the result of **every** task, including the failures.

```js
const results = await Promise.allSettled([
  fetch("/api/profile"),
  fetch("/api/notifications"),
]);

console.log(results);
```

Each item has a `status`:

```js
[
  { status: "fulfilled", value: /* profile response */ },
  { status: "rejected", reason: /* error */ }
]
```

You can handle them independently:

```js
const [profileResult, notificationsResult] = results;

if (profileResult.status === "fulfilled") {
  console.log("Profile loaded:", profileResult.value);
}

if (notificationsResult.status === "rejected") {
  console.error("Notifications failed:", notificationsResult.reason);
}
```

Use this when partial success is useful—for example, a dashboard can still show the profile even if notifications fail.
