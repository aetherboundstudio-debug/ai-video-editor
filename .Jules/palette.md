# Palette's Journal

This journal is a place to document critical UX/accessibility learnings. Entries are only added for major insights, reusable patterns, or significant user behavior discoveries.

## 2026-08-11 - Preventing Focus Resets on Banner Dismissal
**Learning:** Programmatically hiding or dismissing a status banner with focusable elements (such as a close/dismiss button) resets keyboard and screen reader focus to the document body. This interrupts screen reader flow and frustrates keyboard-only users.
**Action:** When a dismiss/close button within a temporary notification or status banner is triggered, programmatically restore focus back to an intuitive context element (such as the main prompt input field) to maintain a seamless keyboard navigation path.

## 2026-08-14 - Screen Reader Announcements and Focus on Suggestion Pill Application
**Learning:** Dynamic input updates (like suggestion pills or prompt modifiers) are silent for screen readers, meaning assistive tech users won't know the field has been populated. Programmatic focus shifts and live regions are required to guarantee a highly accessible experience.
**Action:** When a suggestion pill is activated, immediately populate the input, shift focus to the input, and dispatch a descriptive status update (e.g., "Applied suggestion: [text]") to an `.sr-only` live-region announcer.
