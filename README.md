# 🧠 LLM-Enhanced Threat Intelligence Correlation Automation

<div align="center">

[![n8n](https://img.shields.io/badge/n8n-FF6D5A?style=for-the-badge\&logo=n8n\&logoColor=white)](https://n8n.io)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge\&logo=docker\&logoColor=white)](https://docker.com)
[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge\&logo=telegram\&logoColor=white)](https://telegram.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

**Automated Multi-Source Threat Intelligence, IOC Enrichment & Reporting Pipeline**

*40-node n8n workflow • 6 threat intelligence sources • Automated OSINT collection • Real-time reporting*

[Getting Started](#-getting-started) • [Architecture](#-architecture) • [My Contribution](#-my-individual-contribution) • [Report Format](#-output-report-format) • [Configuration](#-configuration) • [Data Flow](#-data-flow)

</div>

---

## 🎯 Project Overview

This project develops an **automated threat intelligence and reporting pipeline** using **n8n**, integrating multiple security and threat intelligence platforms into a single end-to-end workflow.

The system uses **Perplexity AI for OSINT collection and threat analysis**, extracts and enriches **Indicators of Compromise (IOCs)** such as CVEs, IP addresses, domains, and file hashes, and uses security intelligence platforms including **VirusTotal, AbuseIPDB, Hybrid Analysis, CISA KEV, and AlienVault OTX** to provide additional context.

Threat intelligence is automatically correlated and transformed into a structured, actionable report that is delivered through **Telegram for real-time alerting**.

### Key Objectives

* Automate repetitive threat intelligence collection and analysis
* Integrate multiple security APIs into a unified workflow
* Extract and enrich IOCs from threat intelligence sources
* Correlate information from multiple independent sources
* Use AI-assisted analysis to summarize threat activity and risk
* Deliver structured threat intelligence reports in real time
* Reduce manual effort and accelerate threat investigation and response

---

## 🚀 What It Does

Instead of manually searching multiple threat intelligence platforms, an analyst can send a single request through Telegram:

```text
analyze latest threat intel on Microsoft Exchange Server 2019
```

The n8n workflow automatically:

```text
User Query
    ↓
Natural Language Parsing
    ↓
Threat Intelligence Collection
    ↓
OSINT Research
    ↓
IOC Extraction
    ↓
IOC Enrichment
    ↓
Multi-Source Correlation
    ↓
AI-Assisted Threat Analysis
    ↓
Report Formatting
    ↓
Real-Time Telegram Alert
```

The resulting report provides information about:

* Known vulnerabilities and CVEs
* Active exploitation and attack activity
* Indicators of Compromise
* IP and domain reputation
* Malware-related indicators
* Overall threat level
* Risk assessment
* Recommended mitigation actions
* Supporting source citations

The workflow is designed to produce a comprehensive report within approximately **30–60 seconds**, depending on API response times and external service availability.

---

# 🏗️ Architecture

## Pipeline Overview

![Pipeline Architecture](assets/images/architecture.svg)

## n8n Workflow

![Workflow Overview](assets/images/workflow-overview.svg)

## Pipeline Stages

| Stage  | Component       | Sources / Tools                        | Description                                                   |
| ------ | --------------- | -------------------------------------- | ------------------------------------------------------------- |
| **01** | **Input**       | Telegram                               | Receives and parses the analyst's natural-language request    |
| **02** | **Research**    | CISA KEV, OTX, Perplexity AI           | Collects vulnerability and threat intelligence data           |
| **03** | **Extraction**  | Citation URLs                          | Scrapes referenced sources and extracts relevant IOCs         |
| **04** | **Enrichment**  | VirusTotal, AbuseIPDB, Hybrid Analysis | Enriches indicators with reputation and malware-analysis data |
| **05** | **Correlation** | n8n workflow                           | Groups and aggregates findings from multiple sources          |
| **06** | **Analysis**    | Perplexity AI                          | Generates AI-assisted threat analysis and risk context        |
| **07** | **Reporting**   | Telegram                               | Formats and delivers the final intelligence report            |

---

# 👩‍💻 My Individual Contribution

## Role: API Integration & System Architecture

My primary responsibility was to **design and implement the API integrations and orchestrate the overall system architecture** for the automated threat intelligence pipeline.

I focused on connecting the individual threat intelligence services into a cohesive workflow and ensuring that security data could move reliably between collection, extraction, enrichment, correlation, analysis, and reporting stages.

### Key Responsibilities

* Designed the **overall architecture and data flow** of the automated threat intelligence pipeline.
* Implemented **API integrations** with external threat intelligence and security platforms.
* Integrated **Perplexity AI** to support OSINT collection and AI-assisted threat analysis.
* Connected **VirusTotal, AbuseIPDB, and Hybrid Analysis** for automated IOC enrichment.
* Integrated **Telegram** for real-time threat intelligence alerts and report delivery.
* Orchestrated the workflow using **n8n**, connecting multiple API-driven processing stages.
* Supported automated processing of **CVEs, IP addresses, domains, and other IOCs**.
* Designed the workflow to automatically move intelligence from collection through enrichment and correlation to final reporting.
* Focused on creating a reliable, automated data pipeline that reduced repetitive manual threat intelligence tasks.

---

## 🔗 How My Work Was Integrated into the Project

My contribution acted as the **integration and orchestration layer** that connected the project's different threat intelligence components.

Rather than treating each security platform as an independent tool, I integrated them into a coordinated workflow where the output from one stage could become the input for the next.

```text
                         ┌─────────────────────┐
                         │   Telegram Input    │
                         │  Analyst Threat     │
                         │      Query          │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   n8n Orchestration │
                         │   Query Parsing     │
                         └──────────┬──────────┘
                                    │
                                    ▼
              ┌─────────────────────────────────────────┐
              │       Threat Intelligence Collection    │
              │                                         │
              │  CISA KEV │ OTX │ Perplexity AI        │
              └──────────────────────┬──────────────────┘
                                     │
                                     ▼
                         ┌─────────────────────┐
                         │    IOC Extraction   │
                         │                     │
                         │ CVEs • IPs • Domains│
                         │      • Hashes       │
                         └──────────┬──────────┘
                                    │
                                    ▼
              ┌─────────────────────────────────────────┐
              │             IOC Enrichment              │
              │                                         │
              │ VirusTotal │ AbuseIPDB │ Hybrid Analysis│
              └──────────────────────┬──────────────────┘
                                     │
                                     ▼
                         ┌─────────────────────┐
                         │ Correlation &       │
                         │ Data Aggregation    │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │  Perplexity AI      │
                         │ Threat Analysis &   │
                         │ Report Generation   │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ Report Formatting   │
                         │ & Validation        │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ Telegram Real-Time  │
                         │ Alert & Report      │
                         └─────────────────────┘
```

### Integration Flow

The API integrations I implemented enabled the following workflow:

**1. Threat Intelligence Collection**

The system receives an analyst's request through Telegram and uses n8n to initiate parallel threat intelligence searches across multiple sources.

**2. Data Processing**

Collected information is processed and relevant indicators such as CVEs, IP addresses, domains, and file hashes are identified.

**3. IOC Enrichment**

Extracted indicators are sent to external security platforms such as VirusTotal, AbuseIPDB, and Hybrid Analysis to obtain additional reputation and analysis data.

**4. Correlation**

The workflow combines findings from the different sources, allowing related intelligence to be grouped and analyzed together rather than viewed independently.

**5. AI-Assisted Analysis**

Perplexity AI processes the correlated intelligence and generates contextual analysis covering vulnerabilities, active threats, risk, and recommended actions.

**6. Automated Reporting**

The final intelligence is formatted into a concise, structured report and delivered to the analyst through Telegram.

---

# 📋 Output Report Format

The output is designed as a **structured, analyst-friendly threat intelligence report** that consolidates information from multiple sources into a single response.

![Report Format Components](assets/images/report-format.svg)

## Report Components

### ① Header

Provides the product, version, and analysis context extracted from the analyst's request.

```text
Product: Microsoft Exchange Server 2019
Version: 2019 (CU14)
```

---

### ② Threat Level

The overall threat level is classified based on the available intelligence and AI-assisted analysis.

| Indicator     | Meaning                                                       |
| ------------- | ------------------------------------------------------------- |
| 🔴 **High**   | Critical vulnerabilities or evidence of active exploitation   |
| 🟠 **Medium** | Moderate security risk or vulnerabilities requiring attention |
| 🟢 **Low**    | Lower-severity issues or limited observed exposure            |
| ⚪ **Unknown** | Insufficient information for reliable classification          |

---

### ③ Key Vulnerabilities

The report summarizes relevant CVEs and vulnerability information, including:

* CVE identifier
* Vulnerability type
* Severity information
* Patch or mitigation information
* Disclosure information
* Supporting intelligence sources

Example:

```text
• CVE-2025-53786 — EoP, CVSS 8.0, KB5063221
• CVE-2025-25005 — Tampering
• CVE-2025-25006 — Spoofing
```

---

### ④ Active Threats & Exploits

Perplexity AI analyzes the collected intelligence to identify relevant attack techniques, exploitation activity, and threat context.

Example:

```text
• Web shell deployment in OWA directories
• NTLM relay and Adversary-in-the-Middle activity
• Scanning for ProxyShell-vulnerable servers
• Mail flow rule manipulation through EWS
```

---

### ⑤ IOC Indicator Summary

The workflow aggregates extracted and enriched indicators into a concise summary.

```text
• CVEs: 16 identified
• Malicious IPs: 3
• Suspicious Domains: 5
• File Hashes: 2
```

IOC enrichment includes:

* **AbuseIPDB** → IP reputation and confidence scoring
* **VirusTotal** → Domain and file-hash detection information
* **Hybrid Analysis** → Malware analysis and sandbox verdicts

---

### ⑥ Risk Assessment

The system provides an AI-assisted assessment of the overall threat posture based on the correlated intelligence.

Example:

```text
No active IOCs detected in the environment.
Unpatched systems may remain vulnerable to identified
security issues. Patch priority: CRITICAL.
```

---

### ⑦ Recommendations

The report provides prioritized actions based on the identified vulnerabilities and threat activity.

Example:

```text
1. Apply the recommended security update.
2. Enable additional authentication protections.
3. Monitor suspicious OWA requests.
4. Verify affected software versions and configurations.
```

---

### ⑧ Source Citations

The report includes supporting sources so analysts can validate findings and perform additional investigation.

```text
📎 CISA
   Microsoft Security Blog
   Kaspersky
   Dark Reading
   OTX
   VirusTotal
   AbuseIPDB
```

---

# 🧹 Report Formatting Pipeline

Before the final message is delivered through Telegram, the raw AI-generated output passes through a formatting process.

| Stage                | Transformation                                                                  |
| -------------------- | ------------------------------------------------------------------------------- |
| **Remove Markdown**  | Removes unnecessary Markdown formatting for cleaner Telegram output             |
| **Tables → Bullets** | Converts complex tables into readable bullet points                             |
| **Section Spacing**  | Adds spacing between report sections                                            |
| **Length Control**   | Limits the message to approximately 4,000 characters for Telegram compatibility |

This produces a **clean, readable, analyst-friendly report** without exposing raw JSON, API artifacts, or unnecessary formatting.

---

# 📁 Repository Structure

```text
llm-threat-intel-n8n/
│
├── README.md
├── LICENSE
├── .env.example
├── .gitignore
├── docker-compose.yml
│
├── assets/
│   └── images/
│       ├── architecture.svg
│       ├── workflow-overview.svg
│       ├── report-format.svg
│       └── sample-output.svg
│
├── docs/
│   └── ARCHITECTURE.md
│
├── n8n/
│   ├── workflows/
│   │   └── threat-intel-workflow.json
│   │
│   └── credentials/
│       └── credentials-template.json
│
└── scripts/
    └── setup.sh
```

---

# 🚀 Getting Started

## Prerequisites

* [Docker](https://docs.docker.com/get-docker/)
* Docker Compose
* n8n
* API credentials for the required threat intelligence services

---

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/Malaiyappan-STUX05/llm-threat-intel-n8n.git
cd llm-threat-intel-n8n
```

### 2. Configure environment variables

```bash
cp .env.example .env
```

Add the required API credentials to `.env`.

### 3. Start n8n

```bash
docker-compose up -d
```

### 4. Open n8n

Navigate to:

```text
http://localhost:5678
```

### 5. Import the workflow

Import:

```text
n8n/workflows/threat-intel-workflow.json
```

### 6. Configure credentials

Add the required API credentials within n8n.

### 7. Activate and test

Send a request to the configured Telegram bot and verify that the threat intelligence report is generated.

---

# 🔑 API Integrations

The project integrates multiple APIs and external platforms to support different stages of the intelligence pipeline.

| Service              | Purpose                                          |
| -------------------- | ------------------------------------------------ |
| **Telegram Bot API** | User input and real-time report delivery         |
| **Perplexity AI**    | OSINT collection and AI-assisted threat analysis |
| **AlienVault OTX**   | Threat intelligence and IOC information          |
| **CISA KEV**         | Known exploited vulnerability intelligence       |
| **VirusTotal**       | IOC reputation and detection analysis            |
| **AbuseIPDB**        | IP reputation and abuse confidence information   |
| **Hybrid Analysis**  | Malware and file analysis                        |

---

# ⚙️ Configuring Credentials in n8n

Open:

```text
n8n → Settings → Credentials → Add Credential
```

Configure the required services.

| Credential       | Type             | Purpose                |
| ---------------- | ---------------- | ---------------------- |
| Telegram Bot API | `telegramApi`    | Telegram communication |
| Perplexity AI    | `httpHeaderAuth` | AI/OSINT API requests  |
| VirusTotal       | `httpHeaderAuth` | IOC enrichment         |
| AbuseIPDB        | `httpHeaderAuth` | IP reputation          |
| Hybrid Analysis  | `httpHeaderAuth` | Malware analysis       |

> ⚠️ Never commit API keys or other secrets to the GitHub repository.

---

# 📡 Telegram Webhook Setup

After activating the workflow, obtain the webhook URL from the Telegram Trigger node.

Register the webhook using:

```bash
curl -X POST "https://api.telegram.org/bot<YOUR_BOT_TOKEN>/setWebhook?url=<WEBHOOK_URL>"
```

---

# 🧪 Testing

Send a message to the configured Telegram bot:

```text
analyze latest threat intel on Microsoft Exchange Server 2019
```

The workflow processes the request and returns a structured threat intelligence report.

Example processing flow:

```text
Telegram Request
       ↓
Query Parsing
       ↓
Threat Intelligence Search
       ↓
IOC Extraction
       ↓
IOC Enrichment
       ↓
Correlation
       ↓
AI Analysis
       ↓
Report Generation
       ↓
Telegram Response
```

---

# 🔧 Configuration

## Input Format

```text
analyze latest threat intel on <product> <version>
```

### Examples

```text
analyze latest threat intel on Apache Tomcat 9.0

analyze latest threat intel on Microsoft Exchange Server 2019

analyze latest threat intel on Nginx 1.24

analyze latest threat intel on WordPress 6.4

analyze latest threat intel on OpenSSL 3.0
```

---

## Customization

| Setting               | Location               | Default                                                |
| --------------------- | ---------------------- | ------------------------------------------------------ |
| Search Keywords       | Input validation node  | `CVE`, `Vulnerability`, `Exploit`, `Threat`, `Malware` |
| OTX Result Limit      | OTX search node        | `5` per keyword                                        |
| Perplexity Max Tokens | Perplexity API node    | `500`                                                  |
| Telegram Output Limit | Report formatting node | `4000` characters                                      |

---

# 📊 Data Flow

```text
┌─────────────┐
│  Telegram   │
│   Request   │
└──────┬──────┘
       │
       ▼
┌──────────────────┐
│  Query Parsing   │
│   & Validation   │
└────────┬─────────┘
         │
         ▼
┌───────────────────────────────┐
│ Threat Intelligence Research │
│                               │
│ CISA KEV │ OTX │ Perplexity  │
└───────────────┬───────────────┘
                │
                ▼
       ┌─────────────────┐
       │  IOC Extraction │
       │                 │
       │ CVE/IP/Domain/  │
       │ Hash Extraction │
       └────────┬────────┘
                │
                ▼
┌────────────────────────────────────┐
│          IOC Enrichment            │
│                                    │
│ VirusTotal │ AbuseIPDB │ Hybrid    │
│                         │ Analysis │
└────────────────┬───────────────────┘
                 │
                 ▼
       ┌─────────────────────┐
       │ Correlation &       │
       │ Data Aggregation    │
       └──────────┬──────────┘
                  │
                  ▼
       ┌─────────────────────┐
       │   Perplexity AI     │
       │ Threat Analysis &   │
       │ Report Generation   │
       └──────────┬──────────┘
                  │
                  ▼
       ┌─────────────────────┐
       │ Report Formatting   │
       │ & Length Control    │
       └──────────┬──────────┘
                  │
                  ▼
       ┌─────────────────────┐
       │ Telegram Alert &    │
       │ Report Delivery     │
       └─────────────────────┘
```

---

# 🛡️ Security Considerations

Security was considered throughout the API-driven workflow.

### Protect Credentials

Never commit `.env` files, API keys, bot tokens, or authentication credentials to GitHub.

```text
.env
credentials.json
*.key
*.pem
```

should remain excluded from version control.

### API Rate Limits

External intelligence platforms may enforce request limits depending on the account or API plan.

The workflow should therefore be configured with appropriate request handling and limits.

### Webhook Security

Telegram webhooks should be configured carefully and protected from unauthorized access.

### Credential Management

n8n credentials should be stored using n8n's credential-management functionality rather than hardcoding secrets into workflow nodes whenever possible.

---

# 💡 Project Impact

The project demonstrates how **security automation, API integration, OSINT, IOC enrichment, and AI-assisted analysis** can be combined into a practical threat intelligence workflow.

### Key Benefits

* ⚡ **Faster Intelligence Gathering** — Automates repetitive searches across multiple sources.
* 🔗 **Multi-Source Correlation** — Combines intelligence from several security platforms.
* 🔍 **Automated IOC Enrichment** — Adds reputation and analysis context to extracted indicators.
* 🤖 **AI-Assisted Analysis** — Uses Perplexity AI to summarize and contextualize collected intelligence.
* 📡 **Real-Time Alerts** — Delivers reports directly through Telegram.
* 🛠️ **Reduced Manual Effort** — Automates multiple investigation and reporting steps.
* 📊 **Structured Reporting** — Converts raw intelligence into an analyst-friendly format.

---

# 🧠 Technical Skills Demonstrated

### Cybersecurity

* Threat Intelligence
* OSINT
* Indicators of Compromise (IOCs)
* Vulnerability Intelligence
* CVE Analysis
* IOC Enrichment
* Threat Correlation
* Security Automation

### Engineering

* API Integration
* Workflow Orchestration
* Data Pipeline Design
* REST APIs
* JSON Data Processing
* Regex-Based Extraction
* Automated Reporting
* Webhook Integration

### Tools & Technologies

* **n8n**
* **Perplexity AI**
* **VirusTotal**
* **AbuseIPDB**
* **Hybrid Analysis**
* **AlienVault OTX**
* **CISA KEV**
* **Telegram Bot API**
* **Docker**

---

# 🎯 Why This Project Matters

Traditional threat intelligence workflows often require analysts to manually search multiple sources, collect indicators, validate findings, and create reports.

This project demonstrates an alternative approach:

```text
Manual Investigation
       ↓
Multiple Platforms
       ↓
Manual IOC Collection
       ↓
Manual Correlation
       ↓
Manual Report Writing
```

is transformed into:

```text
Single Analyst Query
       ↓
Automated API Collection
       ↓
IOC Extraction & Enrichment
       ↓
Multi-Source Correlation
       ↓
AI-Assisted Analysis
       ↓
Automated Report
       ↓
Real-Time Alert
```

The result is a more **efficient, repeatable, and scalable threat intelligence workflow** that demonstrates practical application of cybersecurity automation and API-driven security operations.

---

# 📄 License

This project is licensed under the MIT License.

See [`LICENSE`](LICENSE) for details.

---

<div align="center">

**Built with n8n • Threat Intelligence APIs • AI-Assisted Analysis • Security Automation**

</div>
