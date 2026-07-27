# Palette's Journal

This journal is a place to document critical UX/accessibility learnings. Entries are only added for major insights, reusable patterns, or significant user behavior discoveries.

## 2026-07-19 - CSS transition from display: none to block
**Learning:** Elements styled with `display: none` cannot have their opacity or transform properties transitioned immediately upon changing to `display: block` because the browser needs a layout cycle (reflow) to recognize the initial state before transitioning.
**Action:** Trigger a DOM reflow using `void element.offsetWidth;` directly after setting `display: block` and before adding the transitioning CSS class (e.g., `.show`) to ensure the transition animates smoothly.

## 2026-07-27 - Preventing Screen Reader Fatigue on Input Character Limits
**Learning:** Announcing the character count on every single keystroke in inputs with character limits can be extremely fatiguing for screen reader users. Keeping the visual count active while restricting live updates to key milestones (e.g., 80%, 90%, 95%, 100%) and when cleared provides excellent feedback without cluttering the audio stream.
**Action:** Hide the visual character count with `aria-hidden="true"`. Create a visually hidden element with `.sr-only`, `role="status"`, and `aria-live="polite"` to announce progress only at milestones (e.g., 80%, 90%, 95%, 100%) and when the input is cleared.
