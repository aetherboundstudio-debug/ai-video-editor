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

## 2026-08-05 - Multi-sensory Feedback on Character Overfill and Tactile Button Presses
**Learning:** Preventing user input is an effective strategy to enforce character constraints, but without strong visual and auditory warnings, users might assume the app is frozen or broken when their typing suddenly stops working. Incorporating an immediate, subtle physical shake alongside screen-reader alerts clearly communicates constraint boundaries. Additionally, styling buttons with active scale transforms provides an extremely satisfying tactile click response.
**Action:** Always complement text input length boundaries with a CSS shake animation to visually hint at the limit, while immediately updating a screen reader announcer with an explicit warning. Implement `:active` transform scale reductions on interactive elements to give a premium physical "press" feel.

## 2026-09-11 - Dynamic Live Region Announcements for Inline Toggle and Undo Actions
**Learning:** When suggestion pills or undo action bars dynamically modify form text inputs, screen reader users miss key contextual changes if announcements rely solely on aria-pressed attribute toggles or focus shifts.
**Action:** Immediately update a dedicated screen reader live region (such as `srCharAnnouncer`) with non-blocking status messages whenever suggestion pills are applied/removed or actions are undone.

## 2026-09-14 - Multi-sensory Feedback on Paste Truncation
**Learning:** Native `maxlength` attributes silently truncate pasted content without notifying users, leaving keyboard, screen reader, and mouse users unaware that their pasted text was cut off at the character limit.
**Action:** Intercept `paste` events on character-limited inputs to check if incoming text exceeds remaining capacity, triggering visual feedback (shake animation) and explicit screen-reader live announcements ("Pasted text truncated to 100 character limit").

## 2026-10-07 - Keyboard Shortcut Tag Contrast and Disabled Action Parity
**Learning:** Keyboard shortcut `<kbd>` tags inside secondary hint text often inherit subdued text colors, causing contrast ratios to fall below WCAG 2.1 AA standards (4.5:1) when rendered on light badge backgrounds. Furthermore, action buttons disabled during async processes can retain active visual affordances (like underlines or pointers) if `:disabled` CSS rules are missing.
**Action:** Always specify explicit high-contrast text colors (`#1f2937`) with subtle keycap borders (`1px solid #d1d5db`) for `<kbd>` elements, and define `.btn-undo:disabled` (or equivalent) styling to ensure clear disabled visual affordances across all interactive form controls.

## 2026-11-12 - Preventing Event Bubbling Conflicts on Multi-level Escape Shortcuts
**Learning:** When pressing Escape inside an input control triggers a local clear action while simultaneously displaying a document-level notification bar with its own Escape dismissal listener, event bubbling causes the single Escape keypress to perform both actions instantly.
**Action:** Always call `e.stopPropagation()` in addition to `e.preventDefault()` when consuming keyboard shortcuts locally on input fields to prevent event bubbling from immediately triggering document-level overlay or notification dismissal handlers.
