# Palette's Journal

This journal is a place to document critical UX/accessibility learnings. Entries are only added for major insights, reusable patterns, or significant user behavior discoveries.

## 2026-08-11 - Preventing Focus Resets on Banner Dismissal
**Learning:** Programmatically hiding or dismissing a status banner with focusable elements (such as a close/dismiss button) resets keyboard and screen reader focus to the document body. This interrupts screen reader flow and frustrates keyboard-only users.
**Action:** When a dismiss/close button within a temporary notification or status banner is triggered, programmatically restore focus back to an intuitive context element (such as the main prompt input field) to maintain a seamless keyboard navigation path.
