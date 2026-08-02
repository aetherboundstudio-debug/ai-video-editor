# Palette's Journal

This journal is a place to document critical UX/accessibility learnings. Entries are only added for major insights, reusable patterns, or significant user behavior discoveries.

## 2026-07-19 - CSS transition from display: none to block
**Learning:** Elements styled with `display: none` cannot have their opacity or transform properties transitioned immediately upon changing to `display: block` because the browser needs a layout cycle (reflow) to recognize the initial state before transitioning.
**Action:** Trigger a DOM reflow using `void element.offsetWidth;` directly after setting `display: block` and before adding the transitioning CSS class (e.g., `.show`) to ensure the transition animates smoothly.

## 2026-08-02 - Preventing Screen Reader Fatigue on Character Counters
**Learning:** Setting `aria-live="polite"` on a visual character counter triggers screen readers to announce the character count on every single keystroke. This causes severe screen reader fatigue and disrupts the user's focus.
**Action:** Use a visually hidden element (`.sr-only`) with `role="status"` and `aria-live="polite"` as a screen reader announcer. Update its text content to announce milestones (e.g., 80%, 90%, 95%, 100%) and when cleared, rather than updating on every keystroke.
