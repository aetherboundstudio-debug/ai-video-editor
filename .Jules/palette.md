# Palette's Journal

This journal is a place to document critical UX/accessibility learnings. Entries are only added for major insights, reusable patterns, or significant user behavior discoveries.

## 2026-07-19 - CSS transition from display: none to block
**Learning:** Elements styled with `display: none` cannot have their opacity or transform properties transitioned immediately upon changing to `display: block` because the browser needs a layout cycle (reflow) to recognize the initial state before transitioning.
**Action:** Trigger a DOM reflow using `void element.offsetWidth;` directly after setting `display: block` and before adding the transitioning CSS class (e.g., `.show`) to ensure the transition animates smoothly.

## 2026-08-02 - Preventing Screen Reader Fatigue on Character Counters
**Learning:** Setting `aria-live="polite"` on a visual character counter triggers screen readers to announce the character count on every single keystroke. This causes severe screen reader fatigue and disrupts the user's focus.
**Action:** Use a visually hidden element (`.sr-only`) with `role="status"` and `aria-live="polite"` as a screen reader announcer. Update its text content to announce milestones (e.g., 80%, 90%, 95%, 100%) and when cleared, rather than updating on every keystroke.

## 2026-08-03 - Global Shortcuts for Context-Specific Actions
**Learning:** Setting global event listeners for keyboard shortcuts like `Ctrl+Z` or `Cmd+Z` can intercept native browser behaviors or disrupt user typing in unrelated text boxes.
**Action:** Restrict global keyboard shortcut triggers to only execute when the corresponding component or context-specific banner is visible/active. In addition, dynamically detect the user's operating system to display appropriate platform-specific indicators (e.g., `⌘Z` vs `Ctrl+Z`) in `<kbd>` elements.

## 2026-08-04 - Preventing Focus Resets on Banner Dismissal
**Learning:** Programmatically hiding or dismissing a status banner with focusable elements (such as a close/dismiss button) resets keyboard and screen reader focus to the document body. This interrupts screen reader flow and frustrates keyboard-only users.
**Action:** When a dismiss/close button within a temporary notification or status banner is triggered, programmatically restore focus back to an intuitive context element (such as the main prompt input field) to maintain a seamless keyboard navigation path.
