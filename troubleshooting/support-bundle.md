# Creating a Support Bundle

![Type](https://img.shields.io/badge/type-guide-blue)
![Audience](https://img.shields.io/badge/audience-all--users-green)

> **How to collect diagnostic information for troubleshooting and support requests**

---

## Overview

When reporting issues to support, a support bundle helps us diagnose problems quickly. This guide explains what to collect and how to create a bundle.

---

## Quick Collection Checklist

For most issues, collect:

- [ ] VKInsight version
- [ ] Error message or screenshot
- [ ] Steps to reproduce
- [ ] Browser console logs (F12 → Console)
- [ ] Server logs (last 100 lines)

For complex issues, also collect:

- [ ] Configuration settings (sanitized)
- [ ] Browser network tab (F12 → Network)
- [ ] Server resource metrics

---

## What to Include

### 1. Version Information

**Required for all issues:**

| Information | How to Find |
|-------------|-------------|
| VKInsight version | Settings page or `About` section |
| Browser & version | Browser menu → About |
| Operating system | System settings |

**Example:**
```
VKInsight: 2.7.0
Browser: Chrome 122.0.6261.94
OS: Windows 11 / Oracle Linux 8.10
```

---

### 2. Error Information

#### Error Messages

If you see an error message:
1. Copy the **exact** error text
2. Note what action triggered it
3. Note if it's reproducible

**Example:**
```
Error: "Connection timeout after 30 seconds"
Action: Clicked "Connect" in Server Browser
Reproducible: Yes, every time
```

#### Screenshots

For UI issues:
1. Capture the full browser window
2. Include any error dialogs
3. Show the problematic state

**Sensitive Data:** Blur or redact any visible passwords, IP addresses, or customer data in screenshots.

---

### 3. Browser Console Logs

Most browser errors are visible in the developer console:

1. Press **F12** to open Developer Tools
2. Click the **Console** tab
3. Reproduce the issue
4. Look for red error messages
5. Right-click → **Save as...** to export

**Important Errors to Look For:**
- JavaScript errors (red text)
- Network failures (CORS, 404, 500)
- WebSocket disconnections

---

### 4. Server Logs

Server-side logs provide backend diagnostics.

#### Systemd Service Logs

If VKInsight runs as a systemd service:

```bash
# Last 100 lines
sudo journalctl -u vkinsight -n 100 --no-pager

# Logs around a specific time
sudo journalctl -u vkinsight --since "2026-02-23 10:00" --until "2026-02-23 10:30"

# Export to file
sudo journalctl -u vkinsight -n 500 --no-pager > vkinsight-logs.txt
```

#### Application Logs

If running directly:

```bash
# Check for log files
ls -la /opt/istioinsight/logs/

# Or check Streamlit output
cat /var/log/vkinsight/app.log
```

---

### 5. Configuration (Sanitized)

**Never include:**
- Passwords
- API keys
- SSH credentials
- Session secrets

**Safe to include:**
- Feature flags
- Port numbers
- Timeout settings
- Enabled/disabled features

**Example sanitized config:**
```bash
# Export environment variables (sanitized)
env | grep -E "^(ISTIOINSIGHT|STREAMLIT)" | sed 's/=.*SECRET.*/=[REDACTED]/' | sed 's/=.*PASSWORD.*/=[REDACTED]/'
```

---

### 6. Network Information

For connection issues:

```bash
# Test connectivity to VKInsight
curl -I http://localhost:8501

# Test DNS resolution
nslookup vkinsight.example.com

# Check listening ports
sudo netstat -tlnp | grep -E "8501|80|443"
```

---

### 7. System Resources

For performance issues:

```bash
# Memory usage
free -h

# Disk usage
df -h

# CPU load
uptime

# Process memory
ps aux | grep -E "streamlit|python" | head -5
```

---

## Creating the Bundle

### Manual Bundle

Create a directory and collect files:

```bash
# Create bundle directory
BUNDLE_DIR="vkinsight-support-$(date +%Y%m%d-%H%M%S)"
mkdir -p "$BUNDLE_DIR"

# Collect version info
echo "VKInsight Support Bundle" > "$BUNDLE_DIR/info.txt"
echo "Created: $(date)" >> "$BUNDLE_DIR/info.txt"
echo "Hostname: $(hostname)" >> "$BUNDLE_DIR/info.txt"

# Collect server logs (last 500 lines)
sudo journalctl -u vkinsight -n 500 --no-pager > "$BUNDLE_DIR/server-logs.txt" 2>/dev/null

# Collect system info
uname -a > "$BUNDLE_DIR/system-info.txt"
free -h >> "$BUNDLE_DIR/system-info.txt"
df -h >> "$BUNDLE_DIR/system-info.txt"

# Collect config (sanitized)
env | grep -E "^(ISTIOINSIGHT|STREAMLIT)" | \
    sed 's/=.*SECRET.*/=[REDACTED]/' | \
    sed 's/=.*PASSWORD.*/=[REDACTED]/' | \
    sed 's/=.*KEY.*/=[REDACTED]/' > "$BUNDLE_DIR/config-sanitized.txt"

# Create archive
tar -czvf "${BUNDLE_DIR}.tar.gz" "$BUNDLE_DIR"

echo "Bundle created: ${BUNDLE_DIR}.tar.gz"
```

### Bundle Contents

A complete bundle should contain:

```
vkinsight-support-20260223-143022/
├── info.txt                 # Basic info and description
├── server-logs.txt          # Application logs
├── system-info.txt          # System resources
├── config-sanitized.txt     # Sanitized configuration
├── browser-console.txt      # Browser console output (copy/paste)
├── screenshot.png           # UI screenshot (if applicable)
└── steps-to-reproduce.txt   # Detailed reproduction steps
```

---

## Privacy Considerations

### What Gets Included

| Data Type | Included | Notes |
|-----------|----------|-------|
| Error messages | Yes | May contain paths |
| Stack traces | Yes | Contains code paths |
| Configuration | Sanitized | Secrets redacted |
| System info | Yes | Hostname, OS |
| Log samples | Selected | Review for PII |

### What to Redact

Before submitting, review and redact:

- [ ] Passwords and credentials
- [ ] API keys and tokens
- [ ] Internal IP addresses (if sensitive)
- [ ] Customer names or identifiers
- [ ] Personal information
- [ ] Proprietary business data

---

## Submitting the Bundle

### For Internal Support

1. Create the support bundle
2. Upload to internal ticket system
3. Reference ticket number in communications

### For External Support

1. Create the support bundle
2. Review for sensitive data
3. Email to support contact
4. Or upload to secure file share

### Information to Include

When submitting:

```
Subject: VKInsight Support - [Brief Description]

Issue Summary:
[1-2 sentence description]

Steps to Reproduce:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Expected Behavior:
[What should happen]

Actual Behavior:
[What actually happens]

Environment:
- VKInsight Version: 2.7.0
- Browser: Chrome 122
- OS: Oracle Linux 8.10

Attached: vkinsight-support-20260223-143022.tar.gz
```

---

## Troubleshooting Common Collection Issues

### Cannot Access Server Logs

If you don't have server access:
- Contact your administrator
- Provide browser-side information only
- Note that server access is unavailable

### Logs Are Too Large

If logs exceed size limits:
```bash
# Get only recent logs
sudo journalctl -u vkinsight --since "1 hour ago" > recent-logs.txt

# Or get around specific time
sudo journalctl -u vkinsight --since "2026-02-23 10:00" --until "2026-02-23 10:30"
```

### Cannot Reproduce Issue

If the issue is intermittent:
- Note approximate frequency
- Note any patterns (time of day, specific actions)
- Enable debug logging if available

---

## Related Documentation

- [Common Issues](common-issues.md) - Check if your issue is already documented
- [Performance](performance.md) - Performance-specific troubleshooting
- [Troubleshooting](../../operations/troubleshooting.md) - Advanced troubleshooting

---

*Last Updated: 2026-02-23*
