# Bookmarks Feature Roadmap

![Roadmap](https://img.shields.io/badge/type-roadmap-lightgrey)
![Feature](https://img.shields.io/badge/feature-bookmarks-blue)
![Status](https://img.shields.io/badge/status-planning-yellow)
![Updated](https://img.shields.io/badge/updated-2026--02--20-brightgreen)

> **Planned bookmark enhancements - persistence, export/import, keyboard shortcuts, and tagging**

---

## Overview

This document outlines planned enhancements to the Bookmarks feature. These features are under consideration and may change based on user feedback and priorities.

---

## Planned Features

### 1. Keyboard Shortcut

**Priority:** Medium | **Effort:** Low

Add keyboard shortcut `B` for quick bookmark toggling:
- Focus on log line
- Press `B` to toggle bookmark
- Visual feedback on action

---

### 2. Export Bookmarks

**Priority:** High | **Effort:** Medium

Full export functionality for bookmark preservation and sharing.

**Export Formats:**

| Format | Best For |
|--------|----------|
| JSON | Programmatic use, import/export |
| CSV | Spreadsheet analysis |
| Markdown | Documentation, incident reports |
| Text | Simple sharing |

**Export Workflow:**
1. Go to Bookmarks panel
2. Click **Export**
3. Choose format
4. Download file

**Export Content:**
- All bookmark fields (line, timestamp, pod, container)
- User notes
- Context lines (optional)
- Session metadata

---

### 3. Import Bookmarks

**Priority:** Medium | **Effort:** Medium

Import bookmarks from exported files for cross-session continuity.

**Import Workflow:**
1. Go to Bookmarks panel
2. Click **Import**
3. Select file (JSON/CSV)
4. Review and confirm

**Merge Behavior:**
- New bookmarks added to existing
- Duplicates detected by content hash
- Option to overwrite or skip duplicates

---

### 4. Bookmark Categories and Tagging

**Priority:** Medium | **Effort:** High

Organize bookmarks with custom tags and categories.

**Tagging Workflow:**
1. Click bookmark
2. Click **Add Tag**
3. Enter tag name (or select existing)
4. Save

**Suggested Tag Patterns:**

| Tag | Use For |
|-----|---------|
| `error` | Error findings |
| `root-cause` | Root cause evidence |
| `investigation` | Lines requiring follow-up |
| `share` | Lines to share with team |
| `regression` | Regression evidence |

**Filter by Tag:**
1. In Bookmarks panel
2. Select tag filter dropdown
3. View matching bookmarks
4. Multi-select tags for AND/OR filtering

---

### 5. Cross-Session Persistence

**Priority:** High | **Effort:** Medium

Browser storage for automatic bookmark persistence across sessions.

**Implementation Options:**

| Storage | Pros | Cons |
|---------|------|------|
| LocalStorage | Simple, no server needed | Browser-specific |
| IndexedDB | Large capacity, structured | More complex |
| Server-side | Cross-device sync | Requires backend |

**Proposed Behavior:**
- Automatic save to browser storage
- Restore on page load
- Optional: Sync with user account

---

## Implementation Priority

| Priority | Feature | Effort | Impact |
|----------|---------|--------|--------|
| 1 | Export Bookmarks | Medium | High |
| 2 | Cross-Session Persistence | Medium | High |
| 3 | Keyboard Shortcut | Low | Medium |
| 4 | Import Bookmarks | Medium | Medium |
| 5 | Categories/Tagging | High | Medium |

---

## Feedback

If you have feedback on these planned features or want to request other bookmark enhancements, please:
- Open a GitHub Issue with the `enhancement` label
- Include your use case and expected workflow

---

## Related

- [Bookmarks Documentation](../core-features/bookmarks.md) - Current functionality
- [Enhancement Roadmap](../../ENHANCEMENT_ROADMAP.md) - Full feature roadmap

---

*Last Updated: 2026-02-20*
