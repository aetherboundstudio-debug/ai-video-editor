# Palette's Journal

This journal is a place to document critical UX/accessibility learnings. Entries are only added for major insights, reusable patterns, or significant user behavior discoveries.

## 2026-07-19 - CSS transition from display: none to block
**Learning:** Elements styled with `display: none` cannot have their opacity or transform properties transitioned immediately upon changing to `display: block` because the browser needs a layout cycle (reflow) to recognize the initial state before transitioning.
**Action:** Trigger a DOM reflow using `void element.offsetWidth;` directly after setting `display: block` and before adding the transitioning CSS class (e.g., `.show`) to ensure the transition animates smoothly.

## 2026-07-26 - Conditional Keyboard Shortcuts for Custom Interactive Elements
**Learning:** Adding global keyboard shortcuts (like Ctrl+Z or Cmd+Z) for custom undo/redo actions can conflict with native browser controls. To make them accessible and intuitive without causing unexpected side-effects, they must be registered conditionally only when the relevant interactive container/element is active and visible (e.g., checking that its display style is active), and they should utilize dynamic OS platform detection to display the correct platform-specific modifier key (⌘ for Mac, Ctrl for Windows/Linux).
**Action:** Detect the OS dynamically using regex on `navigator.platform` or `navigator.userAgent`, show the appropriate modifier symbol/label in `<kbd>` elements, and restrict the shortcut listener to only execute when the corresponding component is active and visible to prevent interference with other input fields or native actions.
