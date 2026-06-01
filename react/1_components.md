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

---

## 2. JSX (JavaScript XML)

In React, we don't write HTML in one file and JS in another. We use **JSX**, which allows us to write HTML-like code directly inside our JavaScript. Under the hood, a compiler (like Babel) translates this JSX into standard JavaScript function calls.

Because JSX is JavaScript and not pure HTML, there are a few important rules:

1. **The Rule of One:** A component must return a **single** parent element. If you have two `<h1>` tags, wrap them in a `<div>` or a React Fragment `<>...</>`.
2. **The Power of Braces:** You can jump back into "JavaScript mode" inside your JSX by using curly braces `{}`.
3. **camelCase Attributes:** HTML attributes are written in camelCase in JSX (e.g., `onclick` becomes `onClick`, `tabindex` becomes `tabIndex`).
4. **Reserved Words:** Since JSX is JavaScript, some reserved words are renamed (e.g., `class` becomes `className`, and `for` becomes `htmlFor`).
5. **Self-Closing Tags:** All tags that do not have children must be closed with a slash (e.g., `<img />`, `<br />`, `<input />`).
6. **JSX Comments:** You write comments inside curly braces using standard block comment syntax: `{/* This is a comment in JSX */}`.

### Syntax Example:

```javascript
function UserProfile() {
  const username = "Shaheem";
  const avatarUrl = "https://placehold.co/100";
  
  return (
    <div className="profile-card">
      <h2>User: {username}</h2>
      <img src={avatarUrl} alt={username} />
      {/* This is a paragraph comment */}
      <p>Welcome to the dashboard.</p>
    </div>
  );
}
```

---

## 3. The Virtual DOM (Simplified)

You don't need to know the complex math, but you should know the concept: React keeps a lightweight copy of the UI in memory called the **Virtual DOM**. When something changes, React compares the copy to the real page and _only_ updates the specific part that changed. This is why React apps feel so fast.

---

## 4. Exercises & Projects

### 🏋️ Micro-Exercise: The Greeting

**1. Setup:**
Create a new file named `Greeting.jsx` and import it into your main `App.jsx` file.

**2. Your Task:**
- Write a functional component called `Greeting`.
- Inside the function, create a variable called `timeOfDay` (e.g., "Morning", "Afternoon", or "Evening").
- Return a Fragment containing:
  - An `<h1>` that says "Good {timeOfDay}!"
  - A `<p>` tag with a welcoming sentence.
- Render `<Greeting />` inside your `App` component's return statement.

**3. Expected Outcome:**
When running the app, the browser should display the greeting header and welcome paragraph without any page errors.

---

## ⚠️ Common Pitfalls

1. **Returning Multiple Root Elements:**
   ```javascript
   // ❌ ERROR! Must have one root element
   return (
     <h1>Hello</h1>
     <p>Welcome</p>
   );

   //  Correct (Wrapped in a Fragment)
   return (
     <>
       <h1>Hello</h1>
       <p>Welcome</p>
     </>
   );
   ```
2. **Using standard HTML `class` attribute:**
   ```javascript
   // ❌ Incorrect
   return <div class="card">Card</div>;

   //  Correct
   return <div className="card">Card</div>;
   ```
3. **Forgetting to close self-closing tags:**
   ```javascript
   // ❌ Syntax Error
   return <img src="image.png">

   //  Correct
   return <img src="image.png" />;
   ```

---

## 🧠 Brain Teasers & Concept Checks

Predict if the following JSX structures are valid or invalid. If invalid, explain why:

1. What is wrong with this component?
   ```javascript
   function ImageCard() {
     return (
       <h2>My Image</h2>
       <img src="photo.jpg">
     );
   }
   ```
2. What does this output?
   ```javascript
   function Calculation() {
     const value = 5 + 5;
     return <p>The result is: {value}</p>;
   }
   ```
3. Is this component valid JSX?
   ```javascript
   function Title() {
     return <h1 className="main-title">Hello World</h1>;
   }
   ```

---

## 🚀 Stage 1 Project: The Digital Business Card

**The Goal:** Build a static profile card for a team member to understand component nesting and JSX styling.

**1. Starter Setup:**
Create a new directory or files inside your project for components: `Avatar.jsx`, `Info.jsx`, `SocialLinks.jsx`, and `BusinessCard.jsx`.

**2. Your Task:**
- Create the following individual components:
  - `Avatar`: Renders an `<img>` tag with a profile picture url (make sure to close the tag!).
  - `Info`: Renders the name (in an `<h2>`) and a short bio (in a `<p>`).
  - `SocialLinks`: Renders a list of links (Twitter, GitHub, etc.) inside a `<ul>` list.
- Create a `BusinessCard` parent component that imports and nests all three components above inside a wrapper `<div>`.
- Apply some inline CSS styles or classNames (e.g., using `className="card"`) to give the card a border, padding, and centered text.
- Render the `BusinessCard` in your `App.jsx`.

**3. Expected Outcome:**
A visually styled card on the page containing the profile picture, bio info, and list of social links, properly structured as separate, nested components.
