# Stage 6: The Modern Web (Asynchronous JavaScript)

Welcome to the final stage! Until now, your code has been "synchronous," meaning it runs one line at a time, waiting for the previous line to finish. But the real web is "asynchronous." When you fetch data from a server, you don't want the browser to freeze while waiting. This stage is about managing time and external data.

---

## 1. Handling Time (`setTimeout`)

JavaScript uses the **Event Loop** to schedule tasks to happen later while the rest of the code continues to run. The `setTimeout` function is the simplest way to see this in action.

### Syntax Example

```javascript
console.log("Step 1");

setTimeout(() => {
  console.log("Step 2 (after 2 seconds)");
}, 2000);

console.log("Step 3");
```

- **Step 1** logs immediately.
- **Step 3** logs immediately after Step 1.
- **Step 2** logs after a 2-second delay because it was "scheduled" for later.

### 🏋️ Micro-Exercise: The Delay

- **Task**: Write a script that logs "Game Loading..."
- **Action**: Use `setTimeout` to wait 3 seconds, then log "Game Ready!"

---

## 2. Promises: The "I Owe You"

A **Promise** represents a value that might be available now, later, or never. It has three states: **Pending**, **Fulfilled** (Success), and **Rejected** (Failure).

### Syntax Example

```javascript
const myPromise = new Promise((resolve, reject) => {
  let success = true;
  if (success) {
    resolve("Operation Successful!");
  } else {
    reject("Operation Failed.");
  }
});

myPromise
  .then((data) => console.log(data)) // Runs on resolve
  .catch((error) => console.error(error)); // Runs on reject
```

### 🏋️ Micro-Exercise: The Coin Flip

- **Task**: Create a function that returns a Promise.
- **Action**: Generate a random number; if it is $> 0.5$, `resolve("Heads!")`, otherwise `reject("Tails!")`.

---

## 3. The Fetch API

The `fetch()` function allows you to request data from external websites (APIs). It returns a Promise that resolves into a Response object.

### Syntax Example

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json()) // Converts the raw data to a JS object
  .then((data) => console.log(data))
  .catch((err) => console.log("Error:", err));
```

### 🏋️ Micro-Exercise: The Fact Finder

- **Task**: Use `fetch()` to get a random activity from a public API.
- **Action**: Log the activity name to the console.

---

## 4. Modern Async (`async` / `await`)

`async` and `await` are modern keywords that make asynchronous code look and read like simple, linear code.

- **`async`**: Declares that a function contains asynchronous operations.
- **`await`**: Pauses the function execution until a Promise is resolved.

### Syntax Example

```javascript
async function getData() {
  try {
    const response = await fetch(
      "https://jsonplaceholder.typicode.com/posts/1",
    );
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.log("Something went wrong:", error);
  }
}

getData();
```

---

## 🚀 Stage 6 Project: The Mood-Based Movie Finder

**The Goal**: Use a real-world API (like TMDB) to display movies based on a "mood" selected by the user.

**Instructions**:

1. **HTML Setup**: Create a `<select>` dropdown with moods (e.g., "Happy", "Scary", "Excited") and a `<div>` for results.
2. **The Logic**: Write an `async` function that fetches movie data from an API based on the selected genre.
3. **Display**: Randomly pick one movie from the results and update the DOM with its title and poster image.
4. **Error Handling**: Include a `try/catch` block to show a user-friendly message if the API is down.
