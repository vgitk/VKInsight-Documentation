# Daily Analysis Workflow

![Workflow](https://img.shields.io/badge/type-workflow-blue)
![SRE](https://img.shields.io/badge/role-SRE--DevOps-green)
![Time](https://img.shields.io/badge/time-15--20%20min-orange)
![Updated](https://img.shields.io/badge/updated-2026--02--20-brightgreen)

> **Routine log monitoring for SREs and DevOps teams - morning health check, trend tracking, and shift handoff**

---

## Overview

This workflow covers:
1. Morning health check
2. Identifying new issues
3. Tracking trends
4. Shift handoff

**Time required:** 15-20 minutes daily

---

## Morning Health Check (5 minutes)

### Step 1: Load Recent Data

1. Open VKInsight
2. Load logs from last 24 hours
3. Or load since last shift ended

### Step 2: Dashboard Review

Go to **Dashboard** tab and check:

| Metric | Healthy | Investigate |
|--------|---------|-------------|
| Error rate | < 1% | > 1% |
| New error types | None | Any new patterns |
| Pod restarts | 0-2 | > 2 |
| Time gaps | None | Missing data |

### Step 3: Quick Error Scan

1. Click total **ERROR** count
2. Scan the error list
3. Note any unfamiliar errors

**Ask yourself:**
- Any new error types since yesterday?
- Any spike in existing errors?
- Any services with unusual activity?

---

## Identify New Issues (5 minutes)

### Pattern Analysis

1. Go to **Pattern Analysis** tab
2. Click **Run Analysis**
3. Review top patterns

**Compare to baseline:**
- New patterns = New issues
- Increased counts = Worsening issues
- Decreased counts = Improvements

### Check Pod Analytics

1. Go to **Pod Analytics** tab
2. View **Volume vs Error** chart
3. Look for outliers:
   - High error, low volume = Failing service
   - High volume, high error = Overloaded service
   - New pods = Recent deployments

### Review Istio Traffic

If using Istio:
1. Filter to **Istio Proxy Only**
2. Check HTTP status distribution:
   - 5xx spike = Server errors
   - 4xx spike = Client/config issues
3. Load time series for detailed view

---

## Track Trends (5 minutes)

### Week-over-Week Comparison

Note these metrics:
- Total error count
- Top 3 error patterns
- Affected services

### Document Changes

```markdown
## Daily Log: 2024-12-24

### Error Summary
- Total errors: 1,247 (↓ 15% from yesterday)
- Top pattern: Connection timeout (523)
- New pattern: Auth token expired (45)

### Services
- payment-service: Normal
- order-service: Elevated warnings
- gateway: Normal

### Actions
- [ ] Investigate auth token errors
- [ ] Monitor order-service warnings
```

### Use AI Summary

1. Select today's error sample
2. Go to **AI Analyst**
3. Choose **Error Summary**
4. Get automated categorization

---

## Shift Handoff (5 minutes)

### Prepare Handoff Notes

1. **Export** filtered error summary
2. Include:
   - Active issues
   - Recent changes
   - Items to watch

### Bookmark Ongoing Investigations

1. Bookmark any lines you're investigating
2. Add notes with context
3. Next shift can continue from bookmarks

### Quick Report Template

```markdown
## Shift Handoff: Morning → Afternoon

### Status: GREEN/YELLOW/RED

### Active Issues
1. Auth token errors (investigating)
2. Order service warnings (monitoring)

### Recent Changes
- Deployed payment-service v2.3.1 at 09:00

### Watch List
- Auth errors - escalate if > 100/hour
- Order warnings - check after 2 PM

### Data Location
- Logs loaded from: /logs/2024-12-24/
- Time range: 00:00 - 12:00 UTC
```

---

## Weekly Deep Dive (30 minutes)

### Trend Analysis

1. Load logs from entire week
2. Run **Pattern Analysis**
3. Compare pattern counts:
   - Growing patterns = Technical debt
   - New patterns = Recent changes
   - Disappearing patterns = Fixes working

### Service Health Report

| Service | Mon | Tue | Wed | Thu | Fri | Trend |
|---------|-----|-----|-----|-----|-----|-------|
| Payment | 50 | 45 | 48 | 120 | 45 | Spike Thu |
| Order | 20 | 25 | 30 | 35 | 40 | Growing |
| Gateway | 10 | 10 | 10 | 10 | 10 | Stable |

### Action Items

- Investigate growing trends
- Document recurring issues
- Plan fixes for next sprint

---

## Automation Tips

### Save Common Filters

For daily checks:
- Time: Last 24 hours
- Levels: ERROR, WARN
- Exclude: Health checks, DEBUG

### Quick Filters

Use **Quick Filters** for common patterns:
- Critical errors
- Security events
- Performance issues

### Routine Checklist

Daily:
- [ ] Check dashboard
- [ ] Review new errors
- [ ] Update handoff notes

Weekly:
- [ ] Trend analysis
- [ ] Pattern comparison
- [ ] Service health report

---

## When to Escalate

### Immediate Escalation

- Error rate > 5%
- Multiple services affected
- Customer-facing impact

### Monitor Closely

- New error patterns
- Gradual increase in errors
- Single service issues

### Track for Trends

- Low-level warnings
- Intermittent issues
- Performance degradation

---

## Related Workflows

- [Incident Investigation](incident-investigation.md) - When issues found
- [Quick Start](../getting-started/quick-start.md) - Basic navigation

---

## Related Features

- [Dashboard](../core-features/dashboard.md) - Health overview
- [Pod Analytics](../core-features/pod-analytics.md) - Service analysis
- [Pattern Clustering](../advanced/pattern-clustering.md) - Trend identification
- [AI Analysis](../advanced/ai-analysis.md) - Error summary

---

*Consistent daily monitoring prevents incidents from becoming outages.*

---

*Last Updated: 2026-02-20*
