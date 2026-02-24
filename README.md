# 🚀 VKInsight User Guide

Complete documentation for VKInsight - the Kubernetes Pod Log Analyzer.

![Version](https://img.shields.io/badge/version-2.7.0-blue)
![Python](https://img.shields.io/badge/python-3.11+-green)
![Streamlit](https://img.shields.io/badge/streamlit-1.51.0-red)
![Docs](https://img.shields.io/badge/docs-48%2B%20pages-brightgreen)

---

## 📑 Table of Contents

- [Quick Start](#-quick-start)
- [Documentation](#-documentation)
- [Key Features](#-key-features)
- [Getting Help](#-getting-help)

---

## 🚀 Quick Start

| I want to... | Go to... |
|--------------|----------|
| **Get started quickly** | [Quick Start Guide](getting-started/quick-start.md) |
| **Install VKInsight** | [Installation Guide](getting-started/installation.md) |
| **Learn core features** | [Core Features](core-features/) |
| **Use advanced features** | [Advanced Features](advanced/) |
| **Find keyboard shortcuts** | [Keyboard Shortcuts](reference/keyboard-shortcuts.md) |

---

## 📚 Documentation

### **Getting Started** (7 guides)
New to VKInsight? Start here:
- [Quick Start](getting-started/quick-start.md) - Get analyzing in 15 minutes
- [Installation](getting-started/installation.md) - System requirements and setup
- [First Login](getting-started/first-login.md) - Authentication and initial configuration
- [Loading Data](getting-started/loading-data.md) - Import logs from various sources

### **Core Features** (12 guides)
Essential log analysis capabilities:
- [Dashboard](core-features/dashboard.md) - Overview metrics and KPIs
- [Log Viewing](core-features/log-viewing.md) - Browse and inspect logs
- [Search & Filtering](core-features/search-filtering.md) - Find what you need
- [Cross-Pod Search](core-features/cross-pod-search.md) - Search across all pods
- [Smart Squash](core-features/smart-squash.md) - Collapse repetitive lines
- [Bookmarks](core-features/bookmarks.md) - Save important findings

### **Advanced Features** (7 guides)
Power user capabilities:
- [Pattern Clustering](advanced/pattern-clustering.md) - Auto-group similar logs
- [AI Analysis](advanced/ai-analysis.md) - Intelligent log insights
- [Pipe Commands](advanced/pipe-commands.md) - Unix-style processing (grep, awk, jq)
- [SQL Playground](advanced/sql-playground.md) - Query with DuckDB
- [Trace Visualization](advanced/trace-visualization.md) - Request flow diagrams

### **Enterprise Features** (5 guides)
Production deployment capabilities:
- [ISDE Fetcher](enterprise/isde-fetcher.md) - Fetch Oracle debug data
- [Server Browser](enterprise/server-browser.md) - Remote file access
- [Resource Inspector](enterprise/resource-inspector.md) - Kubernetes resource analysis

### **Administration** (4 guides)
For system administrators:
- [Admin Dashboard](admin/dashboard.md) - System health overview
- [User Management](admin/user-management.md) - Manage users and roles
- [Security Setup](admin/security-setup.md) - 2FA and backup codes

### **Reference** (7 guides)
Quick lookup:
- [Keyboard Shortcuts](reference/keyboard-shortcuts.md) - Speed up your workflow
- [Pipe Commands](reference/pipe-command-ref.md) - grep, awk, jq syntax
- [Configuration](reference/configuration.md) - App settings
- [Quick Filters](reference/quick-filters.md) - Pre-configured patterns

### **Troubleshooting** (2 guides)
- [Common Issues](troubleshooting/common-issues.md) - Frequent problems and solutions
- [Performance](troubleshooting/performance.md) - Optimization tips

---

## ⚡ Key Features

| Feature | Description |
|---------|-------------|
| 🔍 **Cross-Pod Search** | Search all pods simultaneously with DuckDB speed |
| 🤖 **AI Analysis** | Intelligent root cause detection with OCA/Ollama |
| 📊 **Pattern Clustering** | Auto-group similar log messages using Drain3 |
| ⭐ **Bookmarks** | Save important findings with pod context |
| 🔧 **Pipe Commands** | Unix-style processing (grep, awk, jq, stats) |
| 📈 **SQL Playground** | Query logs with DuckDB SQL |
| 🔄 **Smart Squash** | Collapse repetitive lines with time tracking |
| 🌐 **Trace Visualization** | Service-to-service request flow diagrams |

---

## 🆘 Getting Help

| Need | Where to Go |
|------|-------------|
| **Common problems** | [Troubleshooting](troubleshooting/common-issues.md) |
| **Performance issues** | [Performance Guide](troubleshooting/performance.md) |
| **Feature request** | [GitHub Issues](https://github.com/vgitk/VKInsight-Documentation/issues) |

---

## 📋 Documentation Info

| Attribute | Value |
|-----------|-------|
| **Version** | 2.7.0 |
| **Total Pages** | 48+ |
| **Last Updated** | 2026-02-23 |
| **Compatibility** | Python 3.11+, Streamlit 1.51+ |

---

*For the complete documentation index, see [index.md](index.md)*
