# Stage 5: The Living Document (DOM)

This module focuses on the **Document Object Model (DOM)**, which is the browser's representation of an HTML page as a tree of objects that JavaScript can manipulate.

---

## 1. What is the DOM?

The DOM acts as a model created by the browser when an HTML file is loaded. It organizes elements into a hierarchy (like a family tree) where the `document` serves as the root.

- **Micro-Exercise (The Picker):** Create an HTML file with an `<h1>Hello World</h1>` tag, use `document.querySelector("h1")` to select it, and change the `innerText` to "DOM Mastered!".

---

## 2. Selecting Elements

To manipulate the page, you must first locate specific elements using JavaScript methods:

- `document.getElementById("id-name")`: Locates a single element by its unique ID.
- `document.querySelector(".class-name")`: Finds the **first** element matching a CSS selector.
- `document.querySelectorAll(".class-name")`: Returns a list (NodeList) of **all** matching elements.

### Syntax Example:

```javascript
const mainTitle = document.getElementById("title");
const firstButton = document.querySelector(".btn");
const allListItems = document.querySelectorAll("li");
```

---

## 3. Event Listeners

Events are actions that occur on the page, such as clicks or keypresses. **Event Listeners** tell JavaScript to wait for these actions and execute a function in response.

- **Syntax:** `element.addEventListener("event", callbackFunction);`

### Syntax Example:

```javascript
const btn = document.querySelector("#myButton");

btn.addEventListener("click", () => {
  console.log("Button was clicked!");
});
```

- **Micro-Exercise (The Clicker):** Add a button to your HTML and write a script that triggers an `alert("You clicked me!")` upon a click event.

---

## 4. Modifying Content, Styles, and Classes

You can change the appearance and content of elements after selecting them:

- **Content:** Update text via `.innerText` or `.innerHTML`.
- **Styles:** Modify CSS directly through `.style.propertyName` (e.g., `backgroundColor`).
- **Classes:** Use `.classList.add()`, `.remove()`, or `.toggle()`.

### Syntax Example:

```javascript
const box = document.querySelector(".box");

box.innerText = "New Content";
box.style.backgroundColor = "blue";
box.classList.add("active");
```

---

## 5. Creating and Appending Elements

JavaScript can dynamically generate and inject new HTML elements into the page.

- **Creation:** Use `document.createElement("tag")`.
- **Insertion:** Use `.appendChild(newElement)` to add the new element to a parent container.

### Syntax Example:

```javascript
// 1. Create the element
const newPara = document.createElement("p");

// 2. Add some content
newPara.innerText = "I was created by JavaScript!";

// 3. Find a parent and append it
const container = document.querySelector("#container");
container.appendChild(newPara);
```

---

### 🚀 Stage 5 Project: Interactive Drum Kit

**The Goal:** Build a webpage where clicking pads or pressing keys triggers audio files and visual animations.

**1. Starter HTML:**

```html
<div class="drum-container">
  <div class="drum" data-key="A">A</div>
  <div class="drum" data-key="S">S</div>
  <div class="drum" data-key="D">D</div>
</div>
```

**2. JavaScript Logic:**

- Select all elements with the class `.drum`.
- Add a `click` listener to each one.
- Inside the listener:
  - Add a CSS class like `.playing` to the clicked element.
  - Use `setTimeout` to remove the `.playing` class after 100ms.
- **Bonus:** Add a `keydown` listener to the `window` to trigger the drum with keyboard inputs.
