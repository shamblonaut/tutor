# Stage 1: The Component Mental Model

Welcome to the world of React! Up until now, you’ve been writing JavaScript to manually "grab" parts of the page and change them. In React, we stop thinking about _how_ to change the page and start thinking about _what_ the page should look like based on components.

---

## 1. What is a Component?

A component is a self-contained "Lego brick" of your user interface. It is essentially a JavaScript function that returns a piece of UI. Instead of one massive HTML file, you build many small, reusable components and nest them together.

### Syntax Example:

```javascript
function WelcomeMessage() {
  return <h1>Hello, React!</h1>;
}

export default WelcomeMessage;
```

**Using It Elsewhere:**
To use this component in another file, you must `import` it:

```javascript
import WelcomeMessage from "./WelcomeMessage";

function App() {
  return (
    <div>
      <WelcomeMessage />
    </div>
  );
}
```

## 2. JSX (JavaScript XML)

In React, we don't write HTML in one file and JS in another. We use **JSX**, which allows us to write HTML-like code directly inside our JavaScript.

- **The Rule of One:** A component must return a **single** parent element. If you have two `<h1>` tags, wrap them in a `<div>` or a Fragment `<>...</>`.
- **The Power of Braces:** You can jump back into "JavaScript mode" inside your JSX by using curly braces `{}`.

### Syntax Example:

```javascript
function UserProfile() {
  const username = "Shaheem";
  return (
    <div>
      <h2>User: {username}</h2>
      <p>Welcome to the dashboard.</p>
    </div>
  );
}
```

## 3. The Virtual DOM (Simplified)

You don't need to know the complex math, but you should know the concept: React keeps a lightweight copy of the UI in memory called the **Virtual DOM**. When something changes, React compares the copy to the real page and _only_ updates the specific part that changed. This is why React apps feel so fast.

---

### 🏋️ Micro-Exercise: The Greeting

**Goal:** Create your first functional component.

1. Write a function called `Greeting`.
2. Inside the function, create a variable called `timeOfDay` (e.g., "Morning" or "Evening").
3. Return a `<div>` containing an `<h1>` that says "Good {timeOfDay}!" and a `<p>` tag with a random welcoming sentence.
4. Render it in your `App` component.

---

## 🚀 Stage 1 Project: The Digital Business Card

**Goal:** Build a static profile card for a team member to understand component nesting.

**Instructions:**

1. **Component Breakdown:** Don't build the card in one big chunk. Break it into three separate components:

- `Avatar`: Renders an `<img>` tag with a profile picture.
- `Info`: Renders the name (in an `<h2>`) and a short bio (in a `<p>`).
- `SocialLinks`: Renders a list of links (Twitter, GitHub, etc.).

2. **The Parent Component:** Create a `BusinessCard` component that nests all three of the components above inside a stylized `div`.
3. **Styling:** Use the `className` attribute in JSX (since `class` is a reserved word in JavaScript) to give your card a border, padding, and centered text.
