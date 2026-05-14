# Stage 5: Lifting State & Context API

In Stage 4, we learned how to bring data into our components from the outside world. Now, we need to learn what to do when multiple components need to share the same "memory" or state.

---

## 1. Lifting State Up

Sometimes, two components that are "siblings" need to share the same information. For example, a search bar needs to tell a list which items to show. In React, data only flows **down** (unidirectional data flow).

To share data between siblings, you must **"Lift State Up"** to their closest common parent. The parent then passes that state down to both children as props.

---

## 2. The Problem: Prop Drilling

Lifting state up works great for small apps. But what if you have a piece of state—like a "Dark Mode" theme or the logged-in user's data—that needs to be accessed by almost every component in your app?

If you lift that state to the very top (`App`), you end up having to pass it down through dozens of intermediary components that don't even use the state, just so they can pass it to the child that does. This is called **Prop Drilling**, and it makes code messy and hard to maintain.

---

## 3. The Solution: Context API

The **Context API** solves Prop Drilling by allowing you to "teleport" data directly to the components that need it, without having to pass it manually via props at every level.

**How it works:**
1. **Create the Context:** `const ThemeContext = createContext();`
2. **Provide the Context:** Wrap your app (or a section of it) in a Provider and pass it the value.
   ```javascript
   <ThemeContext.Provider value="dark">
     <App />
   </ThemeContext.Provider>
   ```
3. **Consume the Context:** Any component inside can grab the value using the `useContext` hook.
   ```javascript
   const theme = useContext(ThemeContext);
   ```

---

### 🏋️ Micro-Exercise: The Theme Toggle

**Goal:** Practice creating and consuming Context.

1. Create a `ThemeContext` using `createContext()`.
2. In your `App` component, create a `theme` state (initialized to "light").
3. Wrap your application in `<ThemeContext.Provider>` and pass both `theme` and `setTheme` as the value (hint: you can pass them as an object).
4. Create a deep child component called `ThemedButton`. Inside it, use `useContext(ThemeContext)` to read the current theme and change its background color, and use `setTheme` to toggle the theme when clicked.

---

## 🚀 Stage 5 Project: The Collaborative To-Do App

**Goal:** Master state management by sharing data between unrelated components.

**Instructions:**

1. **The Parent (`App`):** This component will hold the "Source of Truth"—the `tasks` array state.
2. **Child A (`TaskStats`):** This component receives the `tasks` array as a prop and simply displays the total number of tasks (e.g., "Total Tasks: 5").
3. **Child B (`TaskList`):** This component receives the `tasks` array and a function to delete tasks as props. It maps through the tasks to render them.
4. **The Interaction:** When a user deletes a task in `TaskList`, the total count in `TaskStats` should update automatically because they both rely on the same state in `App`.
