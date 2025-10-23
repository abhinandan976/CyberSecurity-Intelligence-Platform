Cybersecurity Intelligence PlatformAn automated multi-agent system that scans for real-time cybersecurity threats (CVEs) from live APIs, generates specific mitigation plans, and automatically writes professional intelligence reports in both Markdown and PDF formats.Core FeaturesMulti-Agent System: A 4-agent factory-style pipeline (Gatherer, Researcher, Manager, Scribe) that ensures a clean, sequential workflow.Real-Time Threat Data: Connects directly to the official NIST National Vulnerability Database (NVD) API to fetch live threat data.Automated Threat-to-Action Analysis: The system automatically links active threats and vulnerabilities directly to a list of specific, actionable mitigation steps.Dual Report Generation: Automatically creates a comprehensive intelligence report in two formats:Markdown (.md): For easy reading and version control.PDF (.pdf): For professional distribution and archiving.Rule-Based Logic: Uses a fast, reliable, and offline internal rules engine to generate analysis (no LLM/GPU required for this version).LLM-Ready: The project is pre-built to be easily upgradeable to use a local Large Language Model (like Llama 3 or Phi-3) for more dynamic AI-based analysis.How It Works: The 4-Agent ArchitectureThis project is built as an "assembly line" of four distinct agents. Each agent has one specific job and passes its work to the next agent in the sequence.Agent 1: ThreatIntelligenceAgent (The Lookout)Job: Scans the NVD API for newly reported, active, CRITICAL threats.Output: A list of urgent, "on-fire" problems.Agent 2: VulnerabilityResearchAgent (The Researcher)Job: Performs a broader scan of the NVD API for all HIGH and CRITICAL vulnerabilities from the past 7 days.Output: A complete list of all known weaknesses that need patching.Agent 3: IncidentResponseAgent (The Manager)Job: The "brain" of the operation. It takes the data from Agent 1 and Agent 2 and uses its internal rule engine (_analyze_with_rules) to create a specific mitigation plan for each item.Output: A structured list of "Threat-to-Action" plans.Agent 4: ReportWriterAgent (The Scribe)Job: The "packaging" department. It takes the organized plan from Agent 3 and formats it into a professional, human-readable report.Output: The final .md and .pdf files, saved in the /reports directory.Setup and InstallationFollow these steps to get the platform running on your local machine.1. Clone the Repositorygit clone [https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git)
cd CyberSecurity Intelligence Platform
2. Create a Virtual EnvironmentIt's highly recommended to use a virtual environment to manage dependencies.# Create the environment
python -m venv venv

# Activate it
# On Windows (PowerShell):
.\venv\Scripts\activate

# On Mac/Linux (Bash):
source venv/bin/activate
3. Install DependenciesThis project uses a few external Python libraries. The requirements.txt file installs them all.pip install -r requirements.txt
Configuration (Required Step)Before you can run the script, you must configure your NVD API key.1. Get a Free NVD API KeyThe NVD API is a free service, but it requires an API key for faster access. Without a key, you will be severely rate-limited.Go to the NVD API key request page: https://nvd.nist.gov/developers/request-an-api-keyFill out the form and get your key (it's sent via email instantly).2. Add the Key to the ScriptOpen the cyber_platform.py file in your code editor.Go to the Config class (around line 27).Find the NVD_API_KEY variable and paste your API key as a string.Before:@dataclass
class Config:
    ...
    NVD_API_KEY: str = None  # Set your API key here
    ...
After:@dataclass
class Config:
    ...
    NVD_API_KEY: str = "YOUR-API-KEY-GOES-HERE-12345-ABCDE"
    ...
How to Run the PlatformOnce you have installed the requirements and set your API key, you can run the platform with a single command:python cyber_platform.py
Example Console OutputYou will see the agents execute in real-time in your terminal:(venv) PS C:\Projects\CyberPlatform> python cyber_platform.py

======================================================================
🔐 CYBERSECURITY INTELLIGENCE PLATFORM
======================================================================
Analysis Date: 2025-10-23 11:08:00
Lookback Period: 7 days
NVD API Key: Loaded
AI Engine: ⚙️ Rule-Based System (Local LLM Disabled)
======================================================================

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
ollama pull phi3:mini
Install the Library:pip install ollama
Edit the Config: In cyber_platform.py, change two lines in the Config class:# Set this to True to enable the AI agent
USE_LOCAL_LLM: bool = True

# Tell the script which model you downloaded
LLM_MODEL: str = "phi3:mini" 
When you run the script now, Agent 3 will automatically skip the rule-based logic and instead send all the threat data to your local AI. The AI will then generate the mitigation steps dynamically.
