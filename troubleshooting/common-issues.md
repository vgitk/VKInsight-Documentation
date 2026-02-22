# Common Issues

![Troubleshooting](https://img.shields.io/badge/type-troubleshooting-yellow)
![Help](https://img.shields.io/badge/category-help-blue)
![Updated](https://img.shields.io/badge/updated-2026--02--20-brightgreen)

> **Solutions to frequently encountered problems - decision trees and step-by-step fixes**

---

## Quick Decision Trees

Use these flowcharts to quickly identify and resolve issues.

### Application Not Working

```
Start
  │
  ▼
Can you access the login page?
  │
  ├─ NO → Check: Is Streamlit running?
  │         │
  │         ├─ NO → Run: streamlit run istioinsight.py
  │         │
  │         └─ YES → Check port 8501 availability
  │                   → Check firewall rules
  │                   → Try different browser
  │
  └─ YES → Can you log in?
            │
            ├─ NO → Check credentials
            │        → Try password recovery
            │        → Contact admin
            │
            └─ YES → Is the app responding?
                      │
                      ├─ NO → Clear browser cache
                      │        → Refresh page
                      │        → Check browser console
                      │
                      └─ YES → Issue resolved ✓
```

### Data Loading Problems

```
Start
  │
  ▼
Are logs visible in file system?
  │
  ├─ NO → Check source path
  │        → Verify file permissions
  │        → Check disk space
  │
  └─ YES → Does VKInsight detect them?
            │
            ├─ NO → Check file naming pattern
            │        → Verify archive format
            │        → Check extraction folder
            │
            └─ YES → Can you select and load?
                      │
                      ├─ NO → Check memory/disk space
                      │        → Try smaller subset
                      │        → Clear existing data first
                      │
                      └─ YES → Data loading ✓
```

### Search Not Working

```
Start
  │
  ▼
Is search returning results?
  │
  ├─ YES but WRONG → Check: Case sensitivity?
  │                   → Check: Time range correct?
  │                   → Check: Pattern syntax?
  │
  └─ NO results → Is data loaded?
                   │
                   ├─ NO → Load data first
                   │
                   └─ YES → Check exclude patterns
                             │
                             ├─ Has excludes → Clear excludes, retry
                             │
                             └─ No excludes → Expand time range
                                              → Simplify pattern
                                              → Check logs exist
```

### Performance Issues

```
Start
  │
  ▼
What is slow?
  │
  ├─ Initial load → Reduce pod count
  │                  → Narrow time range
  │                  → Check disk I/O
  │
  ├─ Search → Install ripgrep (Linux)
  │            → Add more filters
  │            → Use specific patterns
  │
  ├─ UI/Scrolling → Enable Smart Squash
  │                  → Reduce visible lines
  │                  → Clear bookmarks
  │
  └─ Everything → Check memory usage
                  → Restart session
                  → Increase server resources
```

### AI Analysis Issues

```
Start
  │
  ▼
Is AI provider configured?
  │
  ├─ NO → Configure API key in Profile
  │        → Or set environment variable
  │
  └─ YES → Does analysis run?
            │
            ├─ NO → Check API key validity
            │        → Check network connectivity
            │        → Try different provider
            │
            └─ YES but unhelpful → Select more context
                                    → Use specific analysis type
                                    → Try custom prompt
```

---

## Detailed Solutions

## Application Issues

### App Won't Start

**Symptoms:**
- Streamlit error on startup
- Browser shows blank page
- "Module not found" errors

**Solutions:**

1. **Check Python version**
   ```bash
   python --version  # Should be 3.11+
   ```

2. **Reinstall dependencies**
   ```bash
   pip install -r requirements.txt --force-reinstall
   ```

3. **Clear cache**
   ```bash
   streamlit cache clear
   ```

4. **Check port availability**
   ```bash
   # Default port is 8501
   netstat -an | grep 8501
   ```

---

### Blank Screen After Login

**Symptoms:**
- Login succeeds but no content
- Spinner never stops

**Solutions:**

1. Clear browser cache
2. Try incognito/private window
3. Check browser console for errors
4. Refresh page

---

## Data Loading Issues

### Logs Not Loading

**Symptoms:**
- "No pods found" message
- Empty pod list
- Load button does nothing

**Solutions:**

1. **Verify path exists**
   ```bash
   ls -la /path/to/logs
   ```

2. **Check file permissions**
   ```bash
   chmod -R 644 /path/to/logs/*.log
   ```

3. **Verify naming pattern**
   - Files should be `*-logs.log` or `pod-*.log`

4. **Check disk space**
   ```bash
   df -h
   ```

---

### Archive Extraction Fails

**Symptoms:**
- "Cannot extract archive" error
- Extraction hangs

**Solutions:**

1. **Verify archive integrity**
   ```bash
   tar -tzf archive.tar.gz  # List contents
   ```

2. **Check archive format**
   - Supported: `.tar.gz`, `.zip`, `.7z`

3. **Check disk space**
   - Extraction needs 2-3x archive size

4. **For 7z files**
   ```bash
   pip install py7zr
   ```

---

## Search Issues

### Search is Slow

**Symptoms:**
- Search takes >30 seconds
- Progress bar stalls

**Solutions:**

1. **Install ripgrep** (Linux)
   ```bash
   apt install ripgrep  # 6-8x faster
   ```

2. **Narrow time range**
   - Set specific start/end times

3. **Use more specific patterns**
   - Add service filter
   - Use exact phrases

4. **Reduce pod count**
   - Filter to relevant services

---

### Search Returns Nothing

**Symptoms:**
- No matches found
- Expected results missing

**Solutions:**

1. **Check case sensitivity**
   - Try case-insensitive search

2. **Verify pattern syntax**
   - Test with plain text first

3. **Check time range**
   - Expand range
   - Verify logs exist in range

4. **Check filters**
   - Clear exclude patterns
   - Remove log level filter

---

## Memory Issues

### Out of Memory

**Symptoms:**
- Browser crash
- "Memory allocation failed"
- Slow performance

**Solutions:**

1. **Reduce data size**
   - Load fewer pods
   - Narrow time range
   - Clear old data

2. **Clear cache**
   - Click "Clear All Data"
   - Refresh page

3. **Increase browser memory**
   - Close other tabs
   - Restart browser

4. **Use server deployment**
   - More RAM available
   - Docker with limits

---

### Browser Becomes Slow

**Symptoms:**
- UI lag
- Scroll stuttering
- Input delay

**Solutions:**

1. **Reduce visible lines**
   - Use time filter
   - Apply search filter

2. **Enable Smart Squash**
   - Collapses repeating lines

3. **Clear bookmarks**
   - Large bookmark lists slow UI

4. **Restart session**
   - Logout and login

---

## Connection Issues

### Cannot Connect to Server

**Symptoms:**
- "Connection refused"
- Timeout errors

**Solutions:**

1. **Check network**
   ```bash
   ping server.example.com
   ```

2. **Verify VPN**
   - Connect to VPN if required

3. **Check firewall**
   - Port 22 (SSH) must be open

4. **Verify credentials**
   - Test with SSH directly

---

### ISDE Connection Fails

**Symptoms:**
- "Authentication failed"
- "SR not found"

**Solutions:**

1. **Verify VPN connection**
   - Must be on Oracle VPN

2. **Check credentials**
   - Use ISDE username/password

3. **Verify SR number**
   - Format: `3-12345678901`

4. **Try alternate server**
   - Switch to secondary ISDE

---

## AI Analysis Issues

### AI Not Working

**Symptoms:**
- "API key invalid"
- "Service unavailable"
- No response

**Solutions:**

1. **Check API key**
   - Verify key in Profile → AI Settings
   - Or check `OCA_API_KEY` env var

2. **Test connectivity**
   - Verify can reach OCA endpoint

3. **Reduce context**
   - Select fewer lines
   - Narrow filters

4. **Try later**
   - Service may be temporarily down

---

### AI Response Unhelpful

**Symptoms:**
- Generic responses
- Missing details
- Irrelevant suggestions

**Solutions:**

1. **Provide more context**
   - Include error messages
   - Add surrounding logs

2. **Use specific analysis type**
   - Select appropriate type
   - Or use custom prompt

3. **Include relevant info**
   - Stack traces
   - Timestamps
   - Service names

---

## Authentication Issues

### Forgot Password

**Solutions:**

1. **Use password recovery**
   - Click "Forgot Password" on login
   - Answer security questions

2. **Contact administrator**
   - Request password reset

---

### 2FA Problems

**Symptoms:**
- Code rejected
- "Invalid code" message

**Solutions:**

1. **Check time sync**
   - Device time must be accurate

2. **Use backup code**
   - One-time use codes

3. **Contact admin**
   - Reset 2FA enrollment

---

## Quick Fixes

| Problem | Quick Fix |
|---------|-----------|
| Slow UI | Refresh page |
| No results | Clear filters |
| Login fails | Check caps lock |
| Stuck loading | Refresh + retry |
| Memory issues | Clear data, reload |

---

## Related

- [Performance Tips](performance.md) - Optimization
- [Error Messages](../reference/error-messages.md) - Error codes
- [Installation](../getting-started/installation.md) - Setup

---

*If issues persist, contact administrator or report a bug.*

---

*Last Updated: 2026-02-20*
