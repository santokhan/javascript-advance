### Advanced JavaScript concept: Async generators

An async generator produces values **one at a time**, and it can wait for asynchronous work between values.

```js
async function* getPages() {
  for (let page = 1; page <= 3; page++) {
    const response = await fetch(`/api/posts?page=${page}`);

    if (!response.ok) {
      throw new Error(`Page ${page} failed`);
    }

    yield await response.json();
  }
}

for await (const posts of getPages()) {
  console.log("Received a page:", posts);
}
```

The `*` makes `getPages` a **generator**. Each `yield` sends one result to the `for await` loop. When the loop requests the next result, the function resumes where it stopped.

Think of it as a function that can say: “Here is one page. Ask me again when you’re ready for the next.” This is useful for paginated APIs, file streams, and processing large amounts of data without loading everything at once.
