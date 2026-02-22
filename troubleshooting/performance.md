# Performance Tips

![Troubleshooting](https://img.shields.io/badge/type-troubleshooting-yellow)
![Performance](https://img.shields.io/badge/category-performance-green)
![Updated](https://img.shields.io/badge/updated-2026--02--20-brightgreen)

> **Optimize VKInsight for best performance - 20-35x faster with time filtering, 6-8x faster with ripgrep**

---

## Quick Wins

### Top 5 Performance Tips

| Tip | Impact | Effort |
|-----|--------|--------|
| 1. Use time filters | High | Low |
| 2. Install ripgrep | High | Low |
| 3. Filter to service | Medium | Low |
| 4. Clear old data | Medium | Low |
| 5. Enable squash | Medium | Low |

---

## Data Loading

### Reduce Load Time

1. **Load only needed pods**
   - Select specific services
   - Use time range

2. **Use compressed archives**
   - `.tar.gz` smaller than extracted

3. **Pre-filter data**
   - Remove unneeded files before loading

### Optimal Data Size

| Pods | Lines | Expected Load Time |
|------|-------|-------------------|
| <10 | <100K | <5 seconds |
| 10-50 | 100K-1M | 5-30 seconds |
| 50-100 | 1M-5M | 30-120 seconds |
| >100 | >5M | Consider filtering |

---

## Search Performance

### Use Time Filtering First

DuckDB time filtering: **20-35x faster**

1. Set narrow time range
2. Then apply search pattern
3. DuckDB queries metadata first

### Install ripgrep (Linux)

ripgrep search: **6-8x faster**

```bash
# Ubuntu/Debian
sudo apt install ripgrep

# macOS
brew install ripgrep

# Verify
rg --version
```

### Search Pattern Tips

| Pattern | Speed |
|---------|-------|
| `ERROR` (literal) | Fast |
| `error.*timeout` | Medium |
| `.*error.*` | Slow |
| `^.*pattern` | Very slow |

**Recommendations:**
- Avoid `.*` at start
- Use specific patterns
- Literal text is fastest

---

## Memory Management

### Monitor Memory Usage

Browser memory indicators:
- Slow scrolling = high memory
- Tab crash = memory exceeded

### Reduce Memory Usage

1. **Limit loaded pods**
   - Load 10-20 at a time
   - Filter by service

2. **Use time windows**
   - 1-hour windows
   - Narrow to incident

3. **Clear data regularly**
   - Click "Clear All Data"
   - Before loading new data

4. **Minimize bookmarks**
   - Export and clear old bookmarks

### Memory Guidelines

| RAM | Recommended Max Data |
|-----|----------------------|
| 4 GB | 500K lines |
| 8 GB | 2M lines |
| 16 GB | 5M lines |
| 32 GB | 10M+ lines |

---

## UI Performance

### Enable Smart Squash

Reduces DOM elements:
- Collapses repetitive lines
- Faster scrolling
- Lower memory

### Reduce Visible Lines

- Use pagination
- Set lines per page to 100
- Virtual scrolling handles the rest

### Close Unused Tabs

- Each tab uses memory
- Close analysis tabs when done
- Focus on active investigation

---

## Search Optimization

### Filter Order (Fastest)

1. **Time range** (narrowest)
2. **Service filter**
3. **Log level**
4. **Search pattern**
5. **Exclude patterns**

### Query Optimization

| Approach | Speed |
|----------|-------|
| Time + Service + Pattern | Fastest |
| Pattern only | Slower |
| Regex pattern | Slowest |

### Cross-Pod Search

1. **Filter services first**
   - Select 5-10 services max

2. **Set time window**
   - 15 min windows ideal

3. **Specific patterns**
   - Include service/error type

---

## Backend Optimization

### DuckDB Time Filtering

Automatic when:
- Time range specified
- Multiple pods loaded
- DuckDB installed

Performance: **20-35x faster** for time queries

### ripgrep Backend

Automatic on Linux when:
- ripgrep installed
- Cross-pod search used
- Multiple files searched

Performance: **6-8x faster** for content search

### Parallel Processing

- 4 parallel workers (default)
- Adjustable in config
- Match to CPU cores

---

## Server Deployment

### Production Settings

```toml
# .streamlit/config.toml
[server]
maxUploadSize = 2000
runOnSave = false

[browser]
gatherUsageStats = false
```

### Docker Resources

```yaml
# docker-compose.yml
services:
  istioinsight:
    deploy:
      resources:
        limits:
          memory: 8G
          cpus: '4'
```

### System Tuning

```bash
# Increase file descriptors
ulimit -n 65535

# Increase memory for large files
# /etc/sysctl.conf
vm.max_map_count=262144
```

---

## Performance Checklist

### Before Loading

- [ ] Have time range ready
- [ ] Know relevant services
- [ ] Cleared old data

### During Analysis

- [ ] Time filter applied
- [ ] Service filter active
- [ ] Using specific patterns
- [ ] Squash enabled (if repetitive)

### After Analysis

- [ ] Export findings
- [ ] Clear data
- [ ] Close tabs

---

## Benchmarks

### Search Speed (100K lines)

| Backend | Time | Notes |
|---------|------|-------|
| Python (no filter) | 2.1s | Baseline |
| Python + time | 0.8s | 60% faster |
| ripgrep | 0.35s | 6x faster |
| ripgrep + time | 0.1s | 20x faster |

### Load Speed (50 pods)

| Method | Time |
|--------|------|
| All lines | 45s |
| Time filtered | 12s |
| Service filtered | 8s |
| Both filters | 3s |

---

## When to Scale

### Signs You Need More Resources

- Load times >2 minutes
- Search times >30 seconds
- Memory warnings
- UI unresponsive

### Scaling Options

1. **Vertical** - More RAM/CPU
2. **Filter** - Load less data
3. **Archive** - Pre-process data

---

## Related

- [Common Issues](common-issues.md) - Troubleshooting
- [Configuration](../reference/configuration.md) - Settings
- [Installation](../getting-started/installation.md) - Setup

---

*Performance depends on data size, system resources, and search complexity.*

---

*Last Updated: 2026-02-20*
