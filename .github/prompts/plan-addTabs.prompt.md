## Plan: Add Tabs for Session and History

TL;DR: Convert the single-page layout into a two-tab interface with one tab for the current/new session area and another tab for session history. Keep the summary modal intact and update the JavaScript to switch tabs and render history without using a modal overlay.

**Steps**
1. Add a tab bar inside `index.html` above the main content area with two tab buttons: `Session` and `History`.
2. Wrap the existing welcome screen and current session section in a new container element for the session tab, e.g. `id="session-tab"`.
3. Convert the history modal markup into an inline history tab section, e.g. `id="history-tab"`, and remove the full-screen modal overlay styles for history.
4. Update the `showHistory()` function to populate the history list and activate the history tab instead of opening a modal.
5. Add a new `showTab(tab)` helper in the script to toggle `session-tab` and `history-tab` visibility and manage active tab styles.
6. Adjust `hideHistory()` or create a `showSessionTab()` call to return to the session tab and preserve the current session state.
7. Ensure initial load uses the session tab, showing the welcome screen if no unfinished session exists.
8. Keep the summary modal unchanged as a separate overlay; only history is converted to tabbed page content.

**Relevant files**
- `c:\Users\Administrator\Desktop\Billiards\BilliardsScoreTracker\index.html` — update HTML structure, CSS classes, and JavaScript tab switching logic.

**Verification**
1. Load the app and confirm there are two tabs visible: `Session` and `History`.
2. Confirm the `Session` tab shows the welcome screen when no session exists, or the current session UI when a session is active.
3. Confirm the `History` tab shows the completed sessions list and the existing share/delete actions.
4. Confirm the summary modal still appears and functions when ending a session.

**Decisions**
- Use only one file (`index.html`) for the update.
- Convert history into a tab panel instead of a modal, while leaving the summary modal separate.
- Keep the new session and current session contents under the same session tab.
