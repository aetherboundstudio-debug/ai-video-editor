# Palette's Journal

This journal is a place to document critical UX/accessibility learnings. Entries are only added for major insights, reusable patterns, or significant user behavior discoveries.

## 2026-07-19 - CSS transition from display: none to block
**Learning:** Elements styled with `display: none` cannot have their opacity or transform properties transitioned immediately upon changing to `display: block` because the browser needs a layout cycle (reflow) to recognize the initial state before transitioning.
**Action:** Trigger a DOM reflow using `void element.offsetWidth;` directly after setting `display: block` and before adding the transitioning CSS class (e.g., `.show`) to ensure the transition animates smoothly.

## 2026-07-28 - Reducing Screen Reader Fatigue on Inputs with Character Limits
**Learning:** Having an `aria-live="polite"` character counter update and read on every single keystroke causes high screen reader fatigue. Instead, hiding the live visual counter with `aria-hidden="true"` and using a visually hidden `.sr-only` element with `aria-live="polite"` and `role="status"` to announce character status only at critical milestones (e.g., empty/cleared, 80%, 90%, 95%, and 100%) provides a much calmer and more accessible editing experience.
**Action:** Use an `.sr-only` container paired with milestone-based announcements in JavaScript to prevent verbose keystroke-by-keystroke reading.
