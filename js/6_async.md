# Stage 6: The Modern Web (Asynchronous JavaScript)

This module covers asynchronous programming: scheduling tasks, managing futures (Promises), querying APIs, and using modern `async`/`await` syntax.

---

## 1. Handling Time (`setTimeout`)

Schedule a callback function to run after a specified delay (in milliseconds). The rest of your code runs without blocking.

```javascript
console.log("Start");

// Syntax: setTimeout(callbackFunction, delayInMs)
setTimeout(() => {
  console.log("Logged after 2 seconds");
}, 2000);

console.log("End"); // Logs immediately after "Start", BEFORE the timeout finishes!
```

### 🏋️ Micro-Exercise: The Delay

**1. Setup:**
None.

**2. Your Task:**
- Log `"Game Loading..."` to the console.
- Use `setTimeout()` to schedule a callback function to run after `3000` milliseconds (3 seconds).
- Inside the callback function, log `"Game Ready!"` to the console.

**3. Expected Console Output:**
```text
Game Loading...
(3-second delay here)
Game Ready!
```

---

## 2. Promises: The "I Owe You"

An object representing the eventual success or failure of an asynchronous task.

- **States:** Pending, Fulfilled (Success), or Rejected (Failure).
- **Handlers:** Use `.then()` for success and `.catch()` for errors.

```javascript
const orderPizza = new Promise((resolve, reject) => {
  let isPizzaReady = true;
  if (isPizzaReady) {
    resolve("Pizza Delivered!");
  } else {
    reject("Order Cancelled.");
  }
});

orderPizza
  .then((message) => console.log(message))
  .catch((error) => console.error(error));
```

### 🏋️ Micro-Exercise: The Coin Flip

**1. Setup:**
None.

**2. Your Task:**
- Create a function called `flipCoin` that returns a `new Promise()`.
- Inside the Promise, generate a random number using `Math.random()`.
- If the number is greater than `0.5`, call `resolve()` with the message `"Heads!"`.
- Otherwise, call `reject()` with the message `"Tails!"`.
- Call your `flipCoin()` function, and handle the result by chaining `.then()` (to log the success message) and `.catch()` (to log the failure message).

**3. Expected Console Output:**
```text
Heads!  (or Tails!, randomly)
```

---

## 3. The Fetch API

Request data from external servers (APIs). `fetch` returns a Promise resolving to a Response object. You must convert the raw response to JSON.

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json()) // 1. Convert raw body to JavaScript object
  .then((data) => console.log(data))   // 2. Use the data
  .catch((err) => console.error("Error:", err));
```

### 🏋️ Micro-Exercise: The Fact Finder

**1. Setup:**
None.

**2. Your Task:**
- Use `fetch()` to make an HTTP request to: `https://jsonplaceholder.typicode.com/posts/1`
- Chain a `.then()` to parse the response using `.json()`.
- Chain another `.then()` that takes the parsed `data` and logs its `title` property (`data.title`) to the console.
- Chain a `.catch()` block to log any network errors.

**3. Expected Console Output:**
```text
sunt aut facere repellat provident occaecati excepturi optio reprehenderit
```

---

## 4. Modern Async (`async` / `await`)

A cleaner syntax to handle Promises synchronously without nesting `.then()` calls.

- **`async`**: Declares that a function returns a Promise and can contain `await`.
- **`await`**: Pauses function execution until a Promise resolves.
- **Error Handling:** Use `try/catch` blocks.

```javascript
async function fetchPost() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
    const data = await response.json(); // Wait for body parsing
    console.log(data);
  } catch (error) {
    console.error("Fetch failed:", error);
  }
}

fetchPost();
```

---

## ⚠️ Common Pitfalls

1.  **Forgetting to parse the response with `.json()`:**
    `fetch()` resolves to a Response wrapper, not the raw data itself. You must parse the body!
    ```javascript
    const response = await fetch("...");
    console.log(response); // ❌ Logs response wrapper metadata, not the JSON content.
    const data = await response.json(); //  Correct
    ```
2.  **Forgetting the `await` keyword:**
    ```javascript
    async function getData() {
      const data = fetch("..."); // ❌ Assigns a Promise (pending state) instead of the actual data.
      const data = await fetch("..."); //  Correct
    }
    ```
3.  **Forgetting `try/catch`:**
    If a fetch request fails (e.g., offline, bad URL), it will throw an unhandled promise rejection error and crash your app unless caught.

---

## 🧠 Brain Teasers & Concept Checks

Predict the outputs and execution sequence:

1.  What is the print order of these logs?
    ```javascript
    console.log("A");
    setTimeout(() => console.log("B"), 0);
    console.log("C");
    ```
2.  What is the value of `result` here?
    ```javascript
    async function getValue() {
      return 42;
    }
    const result = getValue();
    console.log(result); // Is it 42 or something else?
    ```

---

## 🚀 Stage 6 Project: The Random Joke Generator

Build a webpage where clicking a button fetches a random joke from a public API and displays the setup and punchline with a slight delay.

**1. Starter Setup (HTML):**
```html
<button id="joke-btn">Tell me a joke!</button>
<div id="joke-container">
  <p id="setup"></p>
  <p id="punchline" style="font-style: italic; color: gray;"></p>
</div>
```

**2. Your Task (JavaScript):**
1.  **Select DOM Elements:** Select the button (`#joke-btn`), setup paragraph (`#setup`), and punchline paragraph (`#punchline`) and store them in variables.
2.  **Add click listener:** Add a `"click"` event listener to the button.
3.  **Implement asynchronous fetch:** Inside the click callback, write an `async` function (or declare the callback itself as `async`):
    - Inside a `try/catch` block:
      - Clear any existing text inside both the setup and punchline paragraphs (`innerText = ""`).
      - Fetch a random joke: `const response = await fetch("https://official-joke-api.appspot.com/random_joke");`
      - Parse the response: `const data = await response.json();`
      - Display the setup text: Set the setup paragraph's `.innerText` to `data.setup`.
      - Delay the punchline: Use `setTimeout()` to wait `2000` milliseconds (2 seconds), then set the punchline paragraph's `.innerText` to `data.punchline`.
    - In the `catch(error)` block:
      - Log the error to the console.
      - Set the setup paragraph's `.innerText` to `"Oops! Failed to load joke. Try again."`.

**3. Expected DOM Result:**
Clicking the button displays the joke's setup immediately (e.g. `"Why did the programmer quit their job?"`), and then 2 seconds later, the punchline (e.g. `"Because they didn't get arrays."`) fades in.
