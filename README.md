# Markdown Notes (iOS-friendly PWA)

A lightweight, offline-first Markdown note app designed to work well on iOS Safari and as a “Add to Home Screen” web app.

## Features

- **Offline support**
  - Works fully offline after first load.
  - Notes are stored in browser `localStorage` on device only.
  - No cloud sync, no backend.

- **Multiple notes with sidebar**
  - Sidebar note list with titles and last-updated sorting.
  - Create new notes from:
    - `Add` button in the toolbar.
    - `+ New` button in the sidebar.
  - Delete notes with the `×` button in the list.
  - Switching notes updates the editor content instantly.

- **Single-pane editor**
  - Main area is a single Markdown editor (no split view).
  - Optimized for small screens (iPhone).
  - Monospace font for code-like editing experience.

- **Edit mode toggle**
  - `Done` / `Edit` button:
    - **Done**: editor is editable (`readOnly = false`).
    - **Edit**: editor becomes read-only for viewing only.
  - Helpful to prevent accidental edits while reading.

- **Preview popup**
  - `Preview` button opens a modal overlay.
  - Uses `marked` to render Markdown to HTML.
  - Close via `Close` button or tapping the dimmed background.

- **Import / Load Markdown**
  - `Load` button opens the system file picker.
  - Supports `.md`, `text/markdown`, and `text/plain`.
  - Selected file content is loaded into the current note and saved to `localStorage`.

- **Export / Download Markdown**
  - `Download` button downloads the current note as a `.md` file.
  - Filename is based on the note title (sanitized).

- **Share via system share sheet**
  - `Share` button uses the Web Share API (where supported).
  - Shares the note title and raw Markdown text to other apps.

- **Clear current note**
  - `Clear` button wipes the current note content after confirmation.
  - Updates the note and saves the empty state.

- **Responsive layout**
  - Desktop:
    - Sidebar and editor shown side by side.
  - Mobile (iOS):
    - Sidebar behaves like a drawer:
      - `☰` button toggles show/hide.
      - Auto-hides after selecting a note.
    - Editor fills most of the screen.

## How it works

- **Storage**
  - All notes are stored as an array in `localStorage` under key `md-notes`.
  - Each note: `{ id, title, content, updatedAt }`.
  - Title is automatically inferred from the first line of the content (fallback to previous title or `"Untitled"`).

- **Offline / PWA**
  - Designed to be hosted on a static site (e.g., GitHub Pages).
  - Combined with a service worker and `manifest.json`, it can be installed to home screen on iOS as a pseudo-native app.

## Usage (iOS)

1. Open the site in Safari.
2. Tap the share icon → **Add to Home Screen**.
3. Launch from the home screen icon for an app-like experience.
4. Use:
   - `Add` / `+ New` to create notes.
   - `Edit` / `Done` to toggle edit mode.
   - `Preview` to view rendered Markdown.
   - `Load` to import `.md` files from Files.
   - `Download` to export notes as `.md`.
   - `Share` to send Markdown to other apps.

## Tech stack

- Pure HTML + CSS + JavaScript.
- `localStorage` for persistence.
- [`marked`](https://marked.js.org/) for Markdown parsing.
- Web Share API for sharing (where supported by the browser).
- Service worker + web manifest for offline/PWA behavior.
