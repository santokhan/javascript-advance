### Advanced JavaScript concept: `AbortController`

Sometimes a request is no longer useful. For example, a user starts a search, then immediately types a new query. `AbortController` lets you cancel the earlier request.

```js
let currentController;

async function search(query) {
  currentController?.abort(); // Cancel the previous request

  const controller = new AbortController();
  currentController = controller;

  try {
    const response = await fetch(
      `/api/search?q=${encodeURIComponent(query)}`,
      { signal: controller.signal }
    );

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }

    return await response.json();
  } catch (error) {
    if (error.name === "AbortError") {
      return; // Expected when a newer search starts
    }

    throw error;
  }
}

search("rea");
search("react"); // Cancels the "rea" request
```

The `signal` connects the controller to `fetch()`. Calling `abort()` tells `fetch()` to stop waiting for that request. This is useful for search boxes, page changes, and components that unmount while loading data.
