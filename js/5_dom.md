# Stage 5: The Living Document (DOM)

This module focuses on the **Document Object Model (DOM)**: locating elements, responding to user interactions, modifying styles/classes, and dynamically adding new HTML tags.

---

## 1. What is the DOM?

The browser's tree representation of an HTML document, with the root object being `document`.

### 🏋️ Micro-Exercise: The Picker

**1. Setup (HTML):**
```html
<h1>Hello World</h1>
```

**2. Your Task:**
- Use `document.querySelector("h1")` to select the header element.
- Change its `.innerText` property to `"DOM Mastered!"`.

**3. Expected DOM Result:**
The text of the heading on the screen changes from "Hello World" to **"DOM Mastered!"**.

---

## 2. Selecting Elements

Locate specific HTML elements using CSS selectors or IDs:

- `document.getElementById("id")` -> Selects one element by its ID.
- `document.querySelector(".class")` -> Selects the **first** matching element.
- `document.querySelectorAll(".class")` -> Returns a NodeList (list-like object) of **all** matching elements.

```javascript
const title = document.getElementById("title");
const firstBtn = document.querySelector(".btn");
const allItems = document.querySelectorAll("li");
```

### 🏋️ Micro-Exercise: The Selector

**1. Setup (HTML):**
```html
<ul>
  <li class="item">A</li>
  <li class="item">B</li>
  <li class="item">C</li>
</ul>
```

**2. Your Task:**
- Use `document.querySelectorAll(".item")` to select all list items and store them in a constant named `allItems`.
- Log `allItems` to your console.
- Print `allItems.length` to the console.

**3. Expected Console Output:**
```text
NodeList(3) [li.item, li.item, li.item] (or similar browser structure)
3
```

---

## 3. Event Listeners

Wait for user actions (like clicks, keypresses) and execute a callback function in response.

```javascript
const btn = document.querySelector("#myButton");

// Syntax: element.addEventListener("event", callback)
btn.addEventListener("click", () => {
  console.log("Button was clicked!");
});
```

### 🏋️ Micro-Exercise: The Clicker

**1. Setup (HTML):**
```html
<button id="alert-btn">Click Me</button>
```

**2. Your Task:**
- Select the button using `document.querySelector("#alert-btn")`.
- Add a click event listener using `.addEventListener()`.
- Inside the event listener callback function, trigger a browser alert with the message `"You clicked me!"`.

**3. Expected DOM Result:**
An alert dialog pops up with the message **"You clicked me!"** when the button is clicked.

---

## 4. Modifying Content, Styles, and Classes

Update selected elements dynamically:

- **Text Content:** `.innerText` or `.innerHTML`.
- **CSS Styles:** `.style.propertyName` (uses camelCase for property names).
- **CSS Classes:** `.classList.add()`, `.remove()`, or `.toggle()`.

```javascript
const box = document.querySelector(".box");

box.innerText = "Updated text!";
box.style.backgroundColor = "blue"; // camelCase!
box.classList.toggle("active");
```

### Reading Custom Data Attributes (`data-*`)

Store extra metadata on HTML elements using `data-attributeName` and read them in JS using `.dataset.attributeName`.

HTML:
```html
<div class="user" data-id="123" data-role="admin">Alex</div>
```
JavaScript:
```javascript
const user = document.querySelector(".user");
console.log(user.dataset.id); // "123"
console.log(user.dataset.role); // "admin"
```

### 🏋️ Micro-Exercise: The Toggler

**1. Setup (HTML & CSS):**
```html
<div class="box"></div>
```
```css
.box { width: 100px; height: 100px; background-color: gray; }
.active { background-color: green; }
```

**2. Your Task:**
- Select the box element using `document.querySelector(".box")`.
- Add a click event listener to the box.
- Inside the event listener, use `.classList.toggle("active")` to toggle the green class.

**3. Expected DOM Result:**
Clicking the box visually toggles its background color between gray and green.

---

## 5. Creating and Appending Elements

Dynamically build and insert new HTML tags:

- **Create:** `document.createElement("tagName")`
- **Insert:** `parentElement.appendChild(newChild)`

```javascript
const newPara = document.createElement("p");
newPara.innerText = "Created dynamically!";

const container = document.querySelector("#container");
container.appendChild(newPara);
```

### 🏋️ Micro-Exercise: The List Builder

**1. Setup (HTML):**
```html
<ul id="my-list"></ul>
```

**2. Your Task:**
- Use `document.createElement("li")` to create a new list item element.
- Set the `.innerText` of the new list item to `"Dynamic Item"`.
- Select the unordered list using `document.querySelector("#my-list")`.
- Append your new list item element inside the unordered list using `.appendChild()`.

**3. Expected DOM Result:**
A new list item containing the text **"Dynamic Item"** appears on the page under the list.

---

## ⚠️ Common Pitfalls

1.  **Adding Listeners to a NodeList directly:**
    You cannot add an event listener to a NodeList. You must select a single element, or loop through the NodeList to add it to each element.
    ```javascript
    const buttons = document.querySelectorAll(".btn");
    buttons.addEventListener("click", () => {}); // ❌ TypeError: buttons.addEventListener is not a function
    
    //  Correct:
    buttons.forEach((btn) => btn.addEventListener("click", () => {}));
    ```
2.  **Forgetting querySelector Prefixes (`.` or `#`):**
    ```javascript
    const btn = document.querySelector("submit-btn"); // ❌ Tries to select a tag named <submit-btn>
    const btn = document.querySelector("#submit-btn"); //  Selects ID
    ```
3.  **Using Non-camelCase Styles:**
    ```javascript
    box.style.background-color = "red"; // ❌ SyntaxError
    box.style.backgroundColor = "red"; //  Correct
    ```

---

## 🧠 Brain Teasers & Concept Checks

Predict what happens in these scenarios:

1.  What does this log if the container is empty?
    ```javascript
    const div = document.querySelector("#container");
    console.log(div.innerText);
    ```
2.  If an element is `<div data-user-name="Sam"></div>`, how do you access the user name in JavaScript dataset?
3.  What happens to the page when this code runs?
    ```javascript
    const newEl = document.createElement("h1");
    newEl.innerText = "Hello!";
    ```

---

## 🚀 Stage 5 Project: Interactive Drum Kit

**The Goal:** Build a webpage where clicking pads or pressing keys triggers visual animations.

**1. Starter Setup (HTML & CSS):**
```html
<!-- HTML -->
<div class="drum-container">
  <div class="drum" data-key="A">A</div>
  <div class="drum" data-key="S">S</div>
  <div class="drum" data-key="D">D</div>
</div>
```

```css
/* CSS */
.drum {
  width: 80px;
  height: 80px;
  border: 4px solid black;
  display: inline-block;
  text-align: center;
  line-height: 80px;
  font-size: 24px;
  margin: 10px;
  transition: all 0.07s ease;
  cursor: pointer;
}
.playing {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 10px #ffc600;
}
```

**2. Your Task (JavaScript):**
1.  **Select the pads:** Use `document.querySelectorAll(".drum")` to select all drum pad elements and store them in a variable `drums`.
2.  **Add click listeners:** Use `.forEach()` to loop through the `drums` NodeList, and add a `"click"` event listener to each pad.
3.  **Implement animation function:** Inside the listener callback:
    - Add the CSS class `"playing"` to the clicked pad element (`classList.add("playing")`).
    - Use `setTimeout()` to remove the class `"playing"` after `100` milliseconds.
4.  **Bonus (Keyboard support):** Add a `"keydown"` event listener to the `window` object:
    - Check the pressed key value: `const key = event.key.toUpperCase();`.
    - Select the matching drum element using an attribute selector query:
      ```javascript
      const drumElement = document.querySelector(`.drum[data-key="${key}"]`);
      ```
    - If a matching `drumElement` exists, add the `"playing"` class to it, and use `setTimeout()` to remove it after `100` milliseconds.

**3. Expected DOM Result:**
Clicking on a pad or pressing the 'A', 'S', or 'D' keys on your keyboard causes the matching pad to scale up and light up with a yellow border, returning to normal after 100ms.
