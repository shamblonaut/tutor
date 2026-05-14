# The Final Boss Project: The Personal Developer Dashboard

This project is the ultimate test of your friends' React journey. Instead of a single-feature app, they will build a multi-page, data-driven dashboard that mimics a professional developer's workspace. It combines every concept from the initial component mental model to complex asynchronous data flow.

---

## **Project Overview**

The dashboard will consist of four main modules:

1. **A Real-time Weather & Greeting Header** (Stages 1 & 4).

2. **A Pomodoro Focus Timer** (Stage 3).

3. **A Persistent Notes Manager** (Stages 2 & 5).

4. **A "Tech News" Feed** (Stages 4 & 6).

---

## **Step 1: Architecture & Routing (Stage 6)**

First, set up the "house" that holds all the rooms.

- **The Router:** Wrap the app in `<BrowserRouter>` and create two main routes: `/dashboard` and `/settings`.

- **Navigation:** Create a sidebar component using `<Link>` tags to move between pages without refreshing the browser.

## **Step 2: The Header & Weather (Stages 1 & 4)**

- **Greeting:** Use a basic functional component to display a personalized greeting based on the user's name (passed via props).

- **Weather API:** Use `useEffect` with an empty dependency array to fetch local weather data from an API (like OpenWeather).

- **Conditional Rendering:** Show a loading spinner while the data is fetching, then display the temperature and a weather icon.

## **Step 3: The Pomodoro Timer (Stage 3)**

- **Logic:** Create a `useState` variable for `secondsRemaining` (initialized to 1500 for 25 minutes).

- **Interactivity:** Add "Start", "Pause", and "Reset" buttons that update the state.

- **Side Effect:** Use `useEffect` to trigger a `setInterval` that decrements the timer every second only when the timer is active.

## **Step 4: The Notes Manager (Stage 5)**

This is where they practice "Lifting State Up".

- **Source of Truth:** Keep the `notes` array in the main `Dashboard` parent component.

- **Mapping:** Pass the array down to a `NoteList` component to render each note with a unique `key`.

- **Filtering:** Add a "Delete" button to each note that triggers a function in the parent to `.filter()` the array and update state.

## **Step 5: Settings & Global Theme (Stage 5)**

- **Theme Toggle:** In the `/settings` route, create a toggle for "Dark Mode."
- **Shared Context:** Instead of lifting state and prop drilling, use the **Context API** to create a `ThemeContext`. Wrap your app in the provider so both the Dashboard and the Settings page can access and update the `isDarkMode` state directly!

---

## **Final Polish & Submission**

To finish the curriculum, encourage your friends to:

- **Clean Code:** Destructure all props for readability.
- **Deployment:** Host their dashboard on a platform like Vercel or Netlify.
- **Documentation:** Write a `README.md` explaining how they managed the state and which APIs they used.
