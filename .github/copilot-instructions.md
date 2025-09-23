# Copilot Instructions for book-list-vue

## Project Overview
This is a Vue 3 Single Page Application (SPA) for managing a personal book list. The project uses Vite for fast development and build tooling. All logic is contained in the frontend; there is no backend or API integration.

## Architecture & Data Flow
- **Main entry:** `src/App.vue` manages the global state (`books` array) and controls which view is shown (book list or add book form).
- **Components:**
  - `Books.vue`: Displays the list of books and allows toggling their read status.
  - `AddBook.vue`: Form for adding a new book. Emits `addBook` event with the new book object.
  - `BookProgress.vue`: Shows reading progress based on the number of books marked as read.
- **State Management:** Uses Vue's `reactive` and `ref` for local state. No Vuex or external state management.
- **Event Communication:** Components communicate via custom events (`@addBook`, `@toggleIsRead`, `@closeAddBook`).
- **Images:** Book covers are referenced from `public/images/` using relative paths (e.g., `/images/book1.jpg`).

## Developer Workflows
- **Start Dev Server:**
  ```powershell
  npm install # if dependencies are missing
  npm run dev
  ```
- **Build for Production:**
  ```powershell
  npm run build
  ```
- **Preview Production Build:**
  ```powershell
  npm run preview
  ```
- **No tests or linting configured by default.**

## Project-Specific Patterns
- **Book IDs:** New books are assigned an incremented `id` based on the current max in the array.
- **Book covers:** Users must provide a valid image URL or use an existing image from `public/images/`.
- **Read status:** Toggled via button in `Books.vue`, updates the `isRead` property.
- **Progress bar:** Computed in `BookProgress.vue` using the number of books marked as read.

## Key Files & Directories
- `src/App.vue`: Main logic, state, and routing between views.
- `src/components/Books.vue`: Book list UI and read toggle.
- `src/components/AddBook.vue`: Add book form and event emission.
- `src/components/BookProgress.vue`: Progress bar and message.
- `public/images/`: Book cover images.

## External Dependencies
- Vue 3
- Vite
- Font Awesome (for icons, assumed via CDN or external link in `index.html`)

## Conventions
- Use `<script setup>` syntax for all Vue SFCs.
- All state is local to `App.vue` and passed as props/events.
- No backend, API, or persistent storage.

---

If any section is unclear or missing important details, please provide feedback so this guide can be improved.
