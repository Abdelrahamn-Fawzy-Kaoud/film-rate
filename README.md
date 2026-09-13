# 🍿 usePopcorn (Film Rate) — Movie Tracking & Rating Application

[![React](https://img.shields.io/badge/React-18.2.0-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![OMDb API](https://img.shields.io/badge/API-OMDb%20REST%20API-yellow?logo=imdb&logoColor=black)](https://www.omdbapi.com/)
[![CSS3](https://img.shields.io/badge/CSS3-Modern%20UI-1572B6?logo=css3&logoColor=white)](https://www.w3.org/Style/CSS/)

A complete, feature-rich movie search, details explorer, and watchlist rating application built with **React**. Developed to master component composition, custom reusable hooks, asynchronous data fetching with HTTP abort controllers, side-effect cleanups, DOM refs, and browser storage synchronization.

---

## ✨ Key Features

- **🔍 Live Movie Search:** Search millions of movies via the OMDb API with real-time feedback.
- **⏱️ Request Cancellation (AbortController):** Automatically aborts in-flight network requests on rapid keystrokes to eliminate race conditions and reduce API load.
- **⭐ Interactive Star Rating Primitive:** A standalone, fully customizable star-rating component with hover previews and dynamic rating messages.
- **📄 Detailed Movie Inspector:** View cast, directors, genres, release dates, plot summaries, and IMDb scores.
- **⌨️ Keyboard Shortcuts:**
  - Press `Enter` from anywhere to focus the search bar.
  - Press `Escape` to close the active movie details panel.
- **💾 LocalStorage Synchronization:** Automatically persists your watched list and ratings across browser reloads.
- **📊 Real-time Watched Summary:** Dynamically calculates total movies watched, average IMDb score, average personal rating, and total viewing duration.
- **🎨 Custom Sleek Scrollbars:** Styled modern scrollbars matching the dark theme without intrusive browser defaults.

---

## 🧠 Advanced React Patterns & Technical Deep Dive

### 1. Custom Reusable Hooks Architecture

- **`useMovies(query)`**: Encapsulates data fetching, loading spinners, and error handling. Utilizes `AbortController` in the `useEffect` cleanup function to prevent memory leaks and outdated responses.
- **`useLocalStorageState(initialState, key)`**: A persistent state hook with lazy initial state evaluation (`useState(() => ...)`) that syncs changes directly with `localStorage`.
- **`useKey(key, action)`**: Attaches DOM `keydown` event listeners to the `document` with automatic listener cleanup on unmount.

### 2. Component Composition & "Children" Prop
- Solves prop drilling by using layout shells that accept `children` (`NavBar`, `Main`, `Box`).
- Rather than passing state through 3 layers, components are nested declaratively:
  ```jsx
  <Main>
    <Box>
      {isLoading && <Loader />}
      {!isLoading && !error && <MovieList movies={movies} />}
      {error && <ErrorMessage message={error} />}
    </Box>
    <Box>
      {selectedId ? <MovieDetails ... /> : <WatchedSummary ... />}
    </Box>
  </Main>
  ```

### 3. DOM Refs & Persistent Variables without Re-renders (`useRef`)
- **Focusing Elements:** Focuses the search input imperatively using `inputEl.current.focus()` on keyboard triggers.
- **Non-rendering Persistent State:** Tracks how many times a user changed their star rating before finally adding the movie, persisting the count across renders without causing extra re-renders.

### 4. Side Effect Cleanups & Dynamic Page Titles
- Updates `document.title` to the currently inspected movie title and restores the original title (`usePopcorn`) when navigating away via the cleanup function.

---

## 🛠️ Technology Stack

| Domain | Technology |
| :--- | :--- |
| **Framework** | React 18 (Create React App) |
| **Data Source** | OMDb REST API |
| **Styling** | Modern Vanilla CSS (Custom Design System with CSS variables) |
| **Storage** | Browser LocalStorage API |

---

## 📁 Project Structure

```text
src/
├── App.js                 # Main application container & state orchestration
├── StarRating.js          # Standalone, reusable star-rating component
├── useMovies.js           # Custom hook for OMDb API data fetching & aborting
├── useLocalStorageState.js# Custom hook for persistent state
├── useKey.js              # Custom hook for global keyboard event listeners
├── index.css              # Dark theme styling, layout tokens, and sleek scrollbars
└── index.js               # Application entrypoint
```

---

## 🚀 Getting Started Locally

### Prerequisites
- Node.js (v16.0.0 or higher)
- npm or yarn

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Abdelrahamn-Fawzy-Kaoud/film-rate.git
   cd film-rate
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Start the development server:**
   ```bash
   npm start
   ```
   Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 👨‍💻 Author

**Abdelrahman Fawzy**
- GitHub: [@Abdelrahamn-Fawzy-Kaoud](https://github.com/Abdelrahamn-Fawzy-Kaoud)

*Built as part of Jonas Schmedtmann's Ultimate React Course curriculum, customized with custom UI styles, enhanced hooks, and production deployment configurations.*
