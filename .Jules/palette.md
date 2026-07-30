# Palette's Journal

This journal is a place to document critical UX/accessibility learnings. Entries are only added for major insights, reusable patterns, or significant user behavior discoveries.

## 2026-07-19 - CSS transition from display: none to block
**Learning:** Elements styled with `display: none` cannot have their opacity or transform properties transitioned immediately upon changing to `display: block` because the browser needs a layout cycle (reflow) to recognize the initial state before transitioning.
**Action:** Trigger a DOM reflow using `void element.offsetWidth;` directly after setting `display: block` and before adding the transitioning CSS class (e.g., `.show`) to ensure the transition animates smoothly.

## 2026-07-27 - Preventing Screen Reader Fatigue on Input Character Limits
**Learning:** Announcing the character count on every single keystroke in inputs with character limits can be extremely fatiguing for screen reader users. Keeping the visual count active while restricting live updates to key milestones (e.g., 80%, 90%, 95%, 100%) and when cleared provides excellent feedback without cluttering the audio stream.
**Action:** Hide the visual character count with `aria-hidden="true"`. Create a visually hidden element with `.sr-only`, `role="status"`, and `aria-live="polite"` to announce progress only at milestones (e.g., 80%, 90%, 95%, 100%) and when the input is cleared.

## 2026-07-29 - Global Keyboard Shortcuts for Custom Interactive UI Elements
**Learning:** Adding global keyboard shortcuts (like Ctrl+Z/Cmd+Z) for custom UI widgets can conflict with native browser behavior or confuse screen reader/keyboard users if active when the corresponding visual component is hidden. Detecting the user's operating system dynamically lets you present appropriate hints (e.g., ⌘Z vs. Ctrl+Z), and restricting key interception to only when the component is visible prevents blocking default browser actions.
**Action:** Detect OS using `navigator.platform` to display the matching keyboard key symbol in a `<kbd>` element. In the global `keydown` event listener, always check that the target custom action widget is visible and enabled before calling `preventDefault()` and executing the handler.

## 2026-07-30 - Preventing Focus Loss on Dismissible Status Elements
**Learning:** Dismissing/closing status banners or notifications that contain interactive elements (like a close/dismiss button) will remove them from the document flow or tab order, causing keyboard and screen reader focus to be lost. When focus is lost, modern browsers fall back to the document root (`<body>`), forcing users to navigate through the entire page again. By programmatically restoring focus back to an intuitive context element (e.g., the primary form input), we maintain a seamless tab stream and keyboard continuity.
**Action:** Always capture the element that should receive focus next, or target an intuitive starting element (like the primary text input). In the dismiss event handler, call `.focus()` on that element immediately.
