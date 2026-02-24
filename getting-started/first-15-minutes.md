# Your First 15 Minutes with VKInsight

Get from login to your first insight in 15 minutes or less.

![Time](https://img.shields.io/badge/time-15%20minutes-blue)
![Difficulty](https://img.shields.io/badge/difficulty-beginner-green)

---

## Overview

This guide walks you through your first VKInsight session. By the end, you'll have:
- Logged in and set up your profile
- Loaded a pod log snapshot
- Performed your first cross-pod search
- Found and bookmarked an error

**Prerequisites:**
- VKInsight URL from your administrator
- Login credentials (username and password)
- A pod snapshot archive (`.tar.gz` or `.7z` file)

---

## Minute 0-3: Login and Setup

### Step 1: Access VKInsight

1. Open your browser and navigate to your VKInsight URL
2. You'll see the login screen with the VKInsight logo

### Step 2: Enter Credentials

1. Enter your **username** (provided by your admin)
2. Enter your **password**
3. Click **Login**

### Step 3: First-Time Setup (if prompted)

If this is your first login, you may be asked to:
- **Change your password** - Choose a strong password (12+ characters recommended)
- **Set up 2FA** - Scan the QR code with your authenticator app (Google Authenticator, Authy, etc.)
- **Save backup codes** - Store these securely for account recovery

> **Tip:** If 2FA is enabled, you'll need your authenticator app for future logins.

---

## Minute 3-8: Load Your First Log Bundle

### Step 4: Navigate to Dashboard

After login, you'll land on the **Dashboard**. This is your home base.

### Step 5: Upload a Pod Snapshot

1. Look for the **Upload** section on the dashboard
2. Click **Browse Files** or drag-and-drop your archive
3. Supported formats:
   - `.tar.gz` - Standard Kubernetes pod snapshots
   - `.7z` - Compressed archives
   - `.zip` - Zip archives

### Step 6: Wait for Extraction

- A progress bar shows extraction status
- Large archives (1GB+) may take 1-2 minutes
- You'll see a success message when complete

### What's Inside a Pod Snapshot?

A typical pod snapshot contains:
```
pod_snapshot/
├── pod1-abc123/
│   ├── container1.log      # Application logs
│   └── istio-proxy.log     # Envoy sidecar logs
├── pod2-def456/
│   ├── container1.log
│   └── istio-proxy.log
└── ...
```

---

## Minute 8-12: Your First Search

### Step 7: Open Cross-Pod Search

1. Click **Cross-Pod Search** in the sidebar (or use keyboard shortcut)
2. This is VKInsight's most powerful feature

### Step 8: Search for Errors

1. In the search box, type: `ERROR`
2. Press **Enter** or click **Search**
3. Results appear instantly (powered by DuckDB + ripgrep)

### Step 9: Understand the Results

| Column | Meaning |
|--------|---------|
| **Pod** | Which pod the log came from |
| **Container** | Which container (app or istio-proxy) |
| **Timestamp** | When the log was written |
| **Message** | The log line content |

### Step 10: Click to Explore

1. Click any result row to see **context** (lines before/after)
2. Use **Single Pod View** to dive deeper into one pod

---

## Minute 12-15: Save Your Findings

### Step 11: Bookmark Important Lines

1. Find an interesting error or pattern
2. Right-click on the log line
3. Select **Add Bookmark**
4. Add a note (e.g., "Root cause of timeout issue")

### Step 12: Try Pattern Clustering

1. Navigate to **Pattern Analysis** tab
2. Click **Analyze Patterns**
3. VKInsight automatically groups similar log messages
4. See which errors are most frequent

---

## What's Next?

Now that you've completed your first session, explore these features:

| Feature | Use Case | Guide |
|---------|----------|-------|
| **Smart Squash** | Collapse repetitive logs | [Smart Squash](../core-features/smart-squash.md) |
| **Pipe Commands** | Unix-style filtering (`grep`, `awk`) | [Pipe Commands](../advanced/pipe-commands.md) |
| **SQL Playground** | Query logs with SQL | [SQL Playground](../advanced/sql-playground.md) |
| **AI Analysis** | Get AI-powered insights | [AI Analysis](../advanced/ai-analysis.md) |
| **Trace Visualization** | See request flows | [Trace Visualization](../advanced/trace-visualization.md) |

---

## Quick Reference

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+F` | Focus search input |
| `Ctrl+R` | Reload data |
| `Ctrl+Scroll` | Zoom log viewer |
| `Right-click` | Context menu |

### Common Search Patterns

```bash
# Find all errors
ERROR

# Find errors in specific pod
ERROR pod:my-service

# Find exceptions with stack traces
Exception

# Find slow requests (>1000ms)
duration.*[0-9]{4,}ms
```

---

## Troubleshooting First Session

| Problem | Solution |
|---------|----------|
| Can't login | Check caps lock, verify credentials with admin |
| 2FA code rejected | Ensure phone time is synced (use automatic time) |
| Upload fails | Check file format (.tar.gz, .7z, .zip supported) |
| No results found | Try broader search term, check time filter |
| Slow performance | Large archives take time; wait for extraction to complete |

---

## Getting Help

- **In-app help:** Click the **?** icon in the top navigation
- **Documentation:** [Full User Guide](../README.md)
- **Common Issues:** [Troubleshooting Guide](../troubleshooting/common-issues.md)
- **Contact:** Your VKInsight administrator

---

*Time to complete: ~15 minutes | Last updated: 2026-02-23*
