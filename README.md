# Cybersecurity Intelligence Platform
An automated multi-agent system that scans for real-time cybersecurity threats (CVEs) from live APIs, generates specific mitigation plans, and automatically writes professional intelligence reports in both Markdown and PDF formats.

## Core Features

Multi-Agent System: A 4-agent factory-style pipeline (Gatherer, Researcher, Manager, Scribe) that ensures a clean, sequential workflow.

Real-Time Threat Data: Connects directly to the official NIST National Vulnerability Database (NVD) API to fetch live threat data.

Automated Threat-to-Action Analysis: The system automatically links active threats and vulnerabilities directly to a list of specific, actionable mitigation steps.

Dual Report Generation: Automatically creates a comprehensive intelligence report in two formats:

Markdown (.md): For easy reading and version control.

PDF (.pdf): For professional distribution and archiving.

Rule-Based Logic: Uses a fast, reliable, and offline internal rules engine to generate analysis (no LLM/GPU required for this version).

LLM-Ready: The project is pre-built to be easily upgradeable to use a local Large Language Model (like Llama 3 or Phi-3) for more dynamic AI-based analysis.

cd CyberSecurity Intelligence Platform
2. Create a Virtual EnvironmentIt's highly recommended to use a virtual environment to manage dependencies.# Create the environment
python -m venv venv

## Activate it
## On Windows (PowerShell):
.\venv\Scripts\activate

## CYBERSECURITY INTELLIGENCE PLATFORM

Analysis Date: 2025-10-23 11:08:00
Lookback Period: 7 days
NVD API Key: Loaded
AI Engine: ⚙️ Rule-Based System (Local LLM Disabled)

[Agent 1] 🔍 Threat Intelligence Analyst: Gathering threat data...
  → Fetching from NVD database...
  ✓ Retrieved 4 threats from NVD
  ... Waiting 1s for NVD API rate limit ...
  → Augmenting with sample threat intelligence...
[Agent 1] ✅ Identified 6 active threats

[Agent 2] 🔬 Vulnerability Researcher: Analyzing CVE database...
  → Querying CVE database for HIGH/CRITICAL CVEs...
  ✓ Found 10 high-severity CVEs
  ... Waiting 1s for NVD API rate limit ...
[Agent 2] ✅ Analyzed 10 vulnerabilities

[Agent 3] 🛡️ Incident Response Advisor: Generating mitigation strategies...
  → Using rule-based logic (USE_LOCAL_LLM=False).
[Agent 3] ✅ Generated 9 mitigation strategies

[Agent 4] 📝 Report Writer: Compiling intelligence report...
[Agent 4] ✅ Markdown Report saved to: ./reports/cyber_intel_report_20251023_110005.md
[Agent 4] ✅ PDF Report saved to: ./reports/cyber_intel_report_20251023_110005.pdf

======================================================================
📊 ANALYSIS COMPLETE
======================================================================
✓ Threats Analyzed: 6
✓ Vulnerabilities Identified: 10
✓ Mitigations Recommended: 9
✓ Reports Generated in: ./reports
======================================================================
Example Report OutputAfter the script runs, check the /reports folder. You will find your new .md and .pdf files, which will look like this:# Cybersecurity Intelligence Report
**Generated:** 2025-10-23 11:00:05  
**Analysis Period:** Last 7 days  
**Report Classification:** CONFIDENTIAL

---

## Executive Summary
...

---

## 1. Active Threat Analysis & Response
This section links active threats directly to their recommended mitigation strategies.

### 1.1 Threat: Ransomware Campaign Targeting Healthcare Sector

**Severity:** 🔴 CRITICAL  
**Date:** 2025-10-22  
**Source:** Simulated Threat Intel  
**Description:** New ransomware variant 'BlackCat 2.0' actively targeting...

**🔵 RECOMMENDED ACTION:**

**Priority:** CRITICAL
**Recommendations:**
- Implement robust backup and recovery procedures (3-2-1 rule)
- Deploy endpoint detection and response (EDR) solutions

**Implementation Steps:**
- Verify all critical data backups are offline and immutable
- Configure EDR to block common ransomware behaviors

---
🚀 Future Enhancements: How to Upgrade to AI AnalysisThis project is built to be easily upgraded to use a real AI model on your local GPU (like an RTX 2050).Install Ollama: Download and install Ollama.Pull a Model: Download a small, fast model.# We recommend Phi-3 Mini (2.2 GB) or Gemma 2 (1.6 GB)
ollama pull llama:3b
Install the Library:pip install ollama
Edit the Config: In cyber_platform.py, change two lines in the Config class:# Set this to True to enable the AI agent
USE_LOCAL_LLM: bool = True
