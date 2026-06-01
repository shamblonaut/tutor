# The Final Boss Project: The Personal Developer Dashboard

This project is the ultimate test of your React journey. Instead of a single-feature app, you will build a multi-page, data-driven dashboard that mimics a professional developer's workspace. It combines every concept from the initial component mental model to complex asynchronous data flow.

---

## Project Overview

The developer dashboard consists of four main modules:
1. **A Real-time Weather & Greeting Header** (Stages 1 & 4)
2. **A Pomodoro Focus Timer** (Stage 3)
3. **A Persistent Notes Manager** (Stages 2 & 5)
4. **A "Tech News" Feed** (Stages 4 & 6)

---

## 1. Starter Setup

Ensure you have a React project initialized. Install `react-router-dom` for navigation:
```bash
npm install react-router-dom
```
Create a clean directory structure containing a `components/` folder for UI segments, a `context/` folder for state context providers, and a `pages/` folder for routing targets (`Dashboard.jsx`, `Settings.jsx`).

---

## 2. Your Task

Implement the developer dashboard step-by-step:

### Step 1: Architecture & Routing (Stage 6)
- Set up `<BrowserRouter>` at the root of your application.
- Define two primary routes: `/dashboard` (rendering the main `<Dashboard />` page) and `/settings` (rendering the `<Settings />` page).
- Create a persistent sidebar component using `<NavLink>` tags to switch pages.

### Step 2: The Header & Weather (Stages 1 & 4)
- Create a `<Header />` component that receives the user's name via props and displays a personalized greeting.
- Use `useEffect` with an empty dependency array to fetch current weather data from a free weather API (e.g., OpenWeatherMap or wttr.in).
- Implement conditional rendering to display a "Loading..." message or spinner while data is being fetched, transitioning to display the temperature and description once loaded.

### Step 3: The Pomodoro Timer (Stage 3)
- Create a `<Timer />` component.
- Maintain `secondsRemaining` in state (initialized to `1500` for 25 minutes) alongside an `isActive` boolean state.
- Add "Start", "Pause", and "Reset" buttons.
- Use `useEffect` to manage a `setInterval` that decrements `secondsRemaining` every second *only* when `isActive` is true. Ensure you return a cleanup function to clear the interval when paused, unmounted, or reset!

### Step 4: The Notes Manager (Stage 5)
- In `<Dashboard />`, maintain a state array of notes (each note object having a unique, stable `id` and a `text` string).
- Create a `<NoteForm />` component to add new notes (using controlled input).
- Create a `<NoteList />` component to render the notes, passing a function callback to handle note deletion.
- Map the notes to list items using the stable note `id` as the `key`.

### Step 5: Settings & Global Theme (Stage 5)
- Create a `ThemeContext` and export a custom `useTheme` hook.
- Implement a `ThemeProvider` component managing the `isDarkMode` state. Wrap your entire application in the provider.
- In your `<Settings />` page, render a checkbox or button that toggles `isDarkMode` using the context value.
- Style your dashboard and page elements to adapt their colors dynamically depending on the global theme.

---

## 3. Expected Outcome

A responsive, fully interactive dashboard with:
- Fluid navigation between the Dashboard and Settings pages with zero page reloads.
- A functional Pomodoro timer that counts down smoothly without memory leaks.
- A fully active Notes manager that lets you add and delete notes, immediately updating the UI.
- A global Dark Mode switch on the Settings page that instantly updates the styles across all pages.
- Clean console logs with no unique key warning messages or React render-phase state updates warnings.
