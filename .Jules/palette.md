# Palette's Journal

This journal is a place to document critical UX/accessibility learnings. Entries are only added for major insights, reusable patterns, or significant user behavior discoveries.

## 2026-07-31 - Dismissible Status Banners and Programmatic Focus Restoration
**Learning:** When dismissing or hiding a status banner containing focusable elements (like a close/dismiss button), programmatically restore focus to an intuitive context element (such as the primary input field) to prevent keyboard/screen reader focus from resetting to the document body.
**Action:** Always bind a click handler on close/dismiss buttons in transient notification banners that programmatically focuses the main active form field or the action button that triggered the alert. This maintains keyboard focus context and provides a seamless non-disruptive keyboard flow.
